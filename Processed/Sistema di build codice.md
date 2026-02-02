---
aliases:
  - Completate
tags:
  - Completed
  - progettiPersonali
  - blog
  - CI/CD
---
--- 
## Nozioni
`Questo sistema gestisce l'intero ciclo di vita del software: dalla scrittura del codice al rilascio in produzione. L'obiettivo è automatizzare il build e il deploy in modo che ogni modifica sia testata e pubblicata istantaneamente su infrastruttura self-hosted, eliminando i tempi di inattività (Zero Downtime).`

## Flusso del Codice e Deploy (CI/CD)
1. **Sviluppo (PC Host - Windows 11):** Lo sviluppatore scrive il codice e i file di configurazione (`Dockerfile` e `workflow.yaml`).
2. **Push (Git):** Tramite il comando `git push`, il codice viene inviato al server **Gitea** (il cervello) sulla VM.
3. **Trigger (Automazione):** Gitea rileva il file in `.gitea/workflows/`, capisce che c'è del lavoro da fare e sveglia l'**Act Runner**.
4. **Pipeline (Build & Registry):** Il Runner esegue le istruzioni:
    - Costruisce l'immagine Docker (impacchetta l'app).
    - Esegue il tag dell'immagine per il **Docker Registry** (il magazzino).
5. **Deploy (Produzione):** Il Runner aggiorna il container sulla VM sostituendo la vecchia versione con la nuova.

## I Componenti in Gioco (I "Perché")
Per capire come tutto ciò avvenga senza interruzioni, ecco i ruoli dei protagonisti:
### 1. Gitea (L'Orchestratore)
È il server Git. Non solo conserva il codice, ma funge da **pannello di controllo**. Decide quando far partire un'automazione e monitora lo stato di salute dei Runner.
### 2. Gitea Act Runner (L'Esecutore)
È il braccio destro di Gitea. È un container che "ascolta" Gitea. Quando c'è un push, lui usa il file **`docker.sock`** della VM per parlare con il motore Docker e dirgli: _"Crea questa immagine e lanciala"_
### 3. Docker & Docker Registry (Il Magazzino)
- **Docker:** Permette di creare "bolle" isolate (container).
- **Registry:** È un archivio dove vengono salvate le versioni finite dell'immagine. Questo è fondamentale per il "rollback": se la versione nuova ha un bug, posso riprendere quella vecchia dal magazzino in un secondo.
#### Spiegazione 
Sul mio PC in personale quello che uso per scrivere il codice gira Gitea lancio il push quando o terminato di implemntare quello che stavo facendo, successivamente questo fa svegliare il runner che legge le istruzione nel file `.yaml` esegue le istruzioni che sono:
- Creare una nuova immagine di docker 
Una volta che l'immagine e stata creata viene sotccata nel "Registri il magazino" e poi una volta fatto cio il ranner stesso mi si va a connettere al mio server in produzione e gli fa scaricare la nuova build una nuova immagine docker in sostanza, da li la esegue senz aperdita del servizio e questo come accade non capisco i vari pezzi che sono in gioco  

## Come avviene il deploy senza perdita di servizio?
Questa è la parte che ti mancava. Il "segreto" risiede nella sequenza di comandi nel file `.yaml`:
1. **Build:** La nuova immagine viene costruita _mentre_ quella vecchia è ancora online.
2. **Stop & Clean:** Il comando `docker stop flask-app || true` ferma il vecchio container solo quando la nuova immagine è già pronta sul disco.
3. **Start:** Il nuovo container parte in pochi millisecondi (`docker run`).
**Perché non c'è downtime?** Perché Docker è velocissimo a distruggere e ricreare. Il tempo in cui la porta 80 rimane "vuota" è solitamente inferiore a 1 secondo, impercettibile per l'utente finale. In sistemi più grandi, si usano due container (uno blu e uno verde) per avere zero millisecondi di distacco, ma per il nostro laboratorio, la sostituzione rapida è perfetta.




## Link 
1) **Core:** [Gitea Documentation](https://docs.gitea.com/) - Guida ufficiale.
2) **Runner:** [Gitea Act Runner](https://gitea.com/gitea/act_runner) - Come funziona l'esecutore.
3) **Docker:** [Dockerfile Reference](https://docs.docker.com/engine/reference/builder/) - Guida alla scrittura delle immagini.
4) [[Test del sistema in LOCALE]]
5) [[Domande sul installazione in locale per test Gitea]]