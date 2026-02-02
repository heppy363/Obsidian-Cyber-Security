---
aliases:
  - Completate
tags:
  - Completed
  - blog
  - progettiPersonali
  - CI/CD
---
--- 
## Nozioni
### 1. Il `Dockerfile`

**Cos'è:** È la ricetta per creare l'ambiente isolato (il container). Invece di installare manualmente Python sul server, diciamo a Docker come "impacchettare" tutto.
```
FROM python:3.12-slim
```
- **Significato:** Sceglie l'immagine di base. `slim` indica una versione leggerissima di Debian con Python 3.12 già installato. Serve a rendere l'immagine piccola e veloce.
```
WORKDIR /app
```
- **Significato:** Crea una cartella `/app` dentro il container e ci entra. Da qui in poi, tutti i comandi avverranno lì dentro.
```

RUN pip install --no-cache-dir flask
```
- **Significato:** Installa le dipendenze. `--no-cache-dir` serve a non sprecare spazio con file temporanei di installazione, mantenendo l'immagine pulita.
```
COPY . .
```
- **Significato:** Copia tutto il contenuto della tua cartella locale (Windows) dentro la cartella `/app` del container.
```
CMD ["python", "app.py"]
```
- **Significato:** È il comando finale. Dice al container: "Appena ti avvii, lancia il server Python".

---

### 1. Il container di Gitea: Il "Cervello"
Gitea non è solo un posto dove salvare i file (come una chiavetta USB), ma è un **Server di Automazione**. Quando riceve un `git push`, Gitea fa tre cose fondamentali:
1. **Analizza il contenuto:** Cerca se dentro il tuo codice esiste la cartella `.gitea/workflows/`.
2. **Pianifica il lavoro:** Se trova un file `.yaml`, crea un "Task" (un compito) nel suo database.
3. **Chiama il Runner:** Avvisa il Runner (che è sempre in ascolto) dicendo: _"Ehi, c'è del lavoro per te! Ecco le istruzioni"_.
### 2. Analisi del file `docker-compose.yml` (di Gitea)
Questo è il file che abbiamo configurato all'inizio nella cartella `cicd-setup`. Vediamo le parti chiave che permettono tutto questo:
```
services:
  server:
    image: gitea/gitea:latest
    container_name: gitea
    environment:
      - GITEA__actions__ENABLED=true  # <-- L'INTERRUTTORE FONDAMENTALE
```
- **Significato:** Questa riga dice a Gitea di attivare il suo motore interno per le "Actions". Senza questa, Gitea ignorerebbe i tuoi file `.yaml`.
```
ports:
      - "3000:3000"  # Interfaccia Web e Git
      - "222:22"     # Accesso SSH
```
- **Significato:** La porta **3000** è quella che usi su Windows per vedere il sito e quella che Git usa per fare il `push`.
```
networks:
      - cicd_net
```
- **Significato:** Gitea vive in una rete chiamata `cicd_net`. È il "recinto" in cui Gitea parla con il suo database (Postgres o MySQL).
### 3. Il "Triangolo" della CI/CD (Come comunicano)
Immagina questa scena:
1. **TU (Windows 11):** Fai il `git push`. Il codice viaggia verso l'IP della VM sulla porta **3000**.
2. **GITEA (Container):** Riceve il codice. Legge il file `deploy.yaml`. Vede che hai chiesto di usare `ubuntu-latest`.
3. **IL RUNNER (Container):** È collegato a Gitea tramite l'URL `http://192.168.178.200:3000`. Sente che c'è un nuovo Task.
4. **L'ESECUZIONE:** Gitea invia il codice al Runner. Il Runner (grazie al `docker.sock`) crea un **terzo container temporaneo** sulla tua VM per compilare l'app Flask.
5. **IL RISULTATO:** Una volta finito, il Runner distrugge il container temporaneo e lascia attivo solo `flask-app`.
### 4. Configurazione Interna (`app.ini`)
C'è un cuore dentro il cuore. Dentro il container di Gitea c'è un file chiamato `app.ini`. La riga più importante che abbiamo sistemato è:
```
ROOT_URL = http://192.168.178.200:3000/
```
**Perché è vitale?** Perché Gitea la usa per generare i link. Quando Gitea dice al Runner: _"Scarica il codice qui"_, usa questo URL. Se ci fosse scritto `localhost`, il Runner cercherebbe il codice dentro se stesso e fallirebbe. Usando l'IP della VM, la comunicazione è perfetta.

--- 
6. Il Docker Compose (`docker-compose-runner.yml`)
**Cos'è:** È il supervisore. Gestisce il ciclo di vita del Runner che comunica con Gitea.
```
network_mode: host
```
- **Il pezzo chiave:** Dice al Runner di non stare dentro una rete isolata di Docker, ma di usare la stessa rete del server Ubuntu. Questo ha risolto il problema di comunicazione con Gitea (IP `192.168.178.200`).
```
volumes:
  - /var/run/docker.sock:/var/run/docker.sock
```
- **La magia:** Questo permette al Runner di "comandare" Docker. In pratica, il Runner (che è un container) può creare altri container sulla tua VM. Senza questo, il Runner non potrebbe fare il `docker build`.
```
environment:
  - GITEA_INSTANCE_URL=http://192.168.178.200:3000
```
- **Significato:** Indica al Runner l'indirizzo esatto dove andare a "prendere ordini".

---
3. Il Workflow Gitea (`deploy.yaml`)
**Cos'è:** È il "direttore d'orchestra" (CI/CD). Definisce cosa deve succedere ogni volta che fai un `git push`.
```
on: [push]
```
- **Significato:** L'evento scatenante. Appena carichi codice sulla branca `master`, la procedura parte.
```
runs-on: ubuntu-latest
```
- **Significato:** Seleziona l'operaio. Dice a Gitea: "Cerca un Runner che abbia questa etichetta (Label)".
```
steps:
  - name: Checkout codice
    uses: actions/checkout@v3
```
- **Significato:** Il Runner scarica il tuo codice sorgente dentro se stesso per poterlo lavorare.
```
- name: Build Immagine Docker
    run: docker build -t hello-flask:latest .
```
- **Significato:** Il Runner esegue il `Dockerfile` analizzato sopra e crea un'immagine chiamata `hello-flask`.
```
- name: Deploy finale sulla VM
    run: |
      docker stop flask-app || true
      docker rm flask-app || true
      docker run -d --name flask-app -p 80:5000 hello-flask:latest
```
- **Significato:** La fase critica. `|| true` serve a ignorare l'errore se il container non esiste ancora. Poi, lancia la nuova versione dell'app sulla porta 80.



## Link 
1) 