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
`Si tratta di un test per capire se tutto funziona con il deplay di un singolo micro servizio flask hello word fatto interamente sul mio sistema host NIENTE server mi aiuta ad avere le idee chiare`

> Il test viene fatto con WMwear che sara "Il mio server" configurato con Ubuntu Server 24.04.3 LTS, sopra di esso gireranno tutti i servizi che mi servono al momento della provo lo testo con 8 GB di RAM e 4 core del processo 


## Configurazione macchina virtuale 
1) Scaricare Ubuntu Server 24.04.3 LTS (scelto per la buona compatibiltia con le tecnologie selezionate)
	1) installare il sistema come da documentazione 
	2) nome server = heppy-server001
	3) Username = heppy-server001
	4) Password = 1234
2) Configurare la scheda di rete della macchina virtuale in modalita _Bridge_ questo e fondamentale dato che mi permette di far vedere la macchina come se fosse un _qualunque altro PC_ sulla rete locale (mio pc personale, altri PC sulla rete ecc) 
	1) [[Configurazione di una macchina virtuale in modalita Bridge]]
3) Installare i programmi necessari 
	1) sudo apt update -> aggiorno il sistema 
	2) sudo apt install docker.io docker-compose -y -> installo docker 
	3) sudo usermod -aG docker $USER  -> Per usare docker senza 'sudo'
4) Creare e avviare i servizi doker necessari 
	1) servizio Gitea [[Configurazione di Gitea su macchina virtuale]]
5) configuazione del Runner, arivato a questo punto il servizio e stabile e si deve procedere con il confgurare il Runenr 
	1) Andare in **Pannello di Amministrazione** (clicca sull'icona del tuo profilo in alto a destra, poi su "Amministrazione Sito").
	2) cerca la voce **Actions** e clicca su **Runners**.
	3) Clicca sul pulsante verde **"Crea nuovo Runner"**
	4) Apparita un token del ranner questo va salvato 
6) Ora si deve effetivamente configuare il runner sul server si tratta di fatto di un altro container docker che ha come specifica il file `docker-compose-runner.yml` 
```
services:
  runner:
    image: gitea/act_runner:latest
    container_name: gitea-runner
    restart: always
    networks:
      - cicd_net
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock
      - ./runner_data:/data
    environment:
      - GITEA_INSTANCE_URL=http://gitea:3000
      - GITEA_RUNNER_REGISTRATION_TOKEN=INCOLLA_QUI_IL_TUO_TOKEN
      - GITEA_RUNNER_NAME=vm-runner
```
- Qui andra inserito il token effettivo 
- Per poi eseguirlo con `docker compose -f docker-compose-runner.yml up -d`
- Puo succedere che quando si lancia il servizio si abbia un errore sulla rete quindi in questo caso usare 
```
networks: 
	cicd_net: 
		external: true
```
- Stiamo semplicemente dicendo a docker che esiste gia una rete virtuale di docker e lui deveusare quella
	- _Importante da considerare_ se non si configura una rete doker in automatico da il nome della rete con quella della cartella hospite del file docher compone in questo caso 
		- cicd-setup_cicd_net come si nota e il nome della cartella che ospita il mio sistema 
- La porzione di codice sopra si modifica cosi 
```
networks: 
	cicd_net: external: true 
	name: cicd-setup_cicd_net
```
- Da considerare di cambiare il nome in caso di necessita il nome lo si trova con questo comando 
	- `docker network ls`
- Potrebbe capitare che ci sino dei probblemi con il token 
7)  Alla fine di tutto il sistema deve apparire cosi 
![[GiteaRunner.png]]
- Come si puo notare il "Bollino" idle e verde il ce significa che tutto il sistema e correttamente configurato e prondo ad entrare in azione


## Configurazione PC host 
1) Assicurarsi che sul sistema sia presente Git [da qui]([git-scm.com/download/win](https://git-scm.com/download/win))
	1) vedere se tutto va bene `git --version` se da un numero va bene 
2) Cerare una cartella di lavoro e metterci dentro il codice, necessario per una prova in questo caso userremo Flask pe creare una prova di APP web 
3) Creazione della struturtra 
	1) app.py 
```
from flask import Flask
app = Flask(__name__)

@app.route('/')
def hello():
    return "<h1>Hello World! v1</h1><p>Deploy CI/CD su VMware riuscito con successo!</p>"

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=5000)
```
2) Creazione del  `Dockerfile`
```
FROM python:3.12-slim
WORKDIR /app
RUN pip install --no-cache-dir flask
COPY . .
EXPOSE 5000
CMD ["python", "app.py"]
```
3) Creare la cartella _.gitea_ e dentro la cartella _workflows_ e dentro la cartella mettere il file _deploy.yaml_ questo contiene le specifiche per il deploy 
```
name: Flask-CI-CD
on: [push]

jobs:
  build-and-deploy:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout codice
        uses: actions/checkout@v3

      - name: Build Immagine Docker
        run: docker build -t hello-flask:latest .

      - name: Deploy finale sulla VM
        run: |
          docker stop flask-app || true
          docker rm flask-app || true
          docker run -d --name flask-app -p 80:5000 hello-flask:latest
```
4) Eseguire lo stack di git 
	1) `git init`
	2) `git add .`
	3) `git commit -m "Primo deploy automatico"`
	4) `git remote add origin http://192.168.178.200:3000/heppy/flask-test.git`
		1) sostituire indirizzo e nome della repo a dovere con il progetto creato 
5) Caricato il codice nella repo controllare dalle impostazioni della stessa se la voce `Action` e abilitata 
	1) Si va nella impostazioni chiave inglese a destra 
	2) si trova la voce `Action` si spunta la voce si confermano le modifiche
	3) Ri eseguire un comm it per fare partire le action 
6) e molto prbabile che al primo run appaia questo errore `Could not resolve host: gitea` 
	1) questo avviene perche gitea non sa risolver l'ulteriore runner che si crea pe la generazione del immagine doker nonostante i due container siano sotto la stessa rete 
per fixare questa cosa si deve modificare l'url di base di gite quindi del suo container per tanto 
 7)  si entra dentro il container `sudo docker exec -it gitea /bin/bash`
 8) si modifica il fine _app.ini_ della macchina 
	 1) vi /data/gitea/conf/app.ini
9) e si modifica la variabile `ROOT_URL` con -> http://localhost:3000/ o http://gitea:3000/
10) Poi si modfica nel `docker-compose-runner.yml`
	1) `extra_hosts: - "gitea:192.168.178.200" # Sostituisci con l'IP della VM
	2) aggiunger anche `network_mode: host` -> fa si che doker veda la rete esattemante come la tua macchina virtuale 
	

## Link 
1) 