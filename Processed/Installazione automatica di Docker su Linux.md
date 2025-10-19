---
aliases:
  - Completate
tags:
  - Completed
  - Docker
  - Linux
---
--- 
## Nozioni
Docker fornisce un **installer universale** che consente di installare il motore Docker su qualsiasi distribuzione Linux in modo automatico.  
Questo installer è rappresentato da uno script shell (`get-docker.sh`), scaricabile direttamente dal sito ufficiale di Docker.  
Il vantaggio di questo approccio è che lo script **rileva automaticamente la distribuzione Linux** in uso (Debian, Ubuntu, Fedora, Arch, CentOS, ecc.) e utilizza il **package manager corretto** (`apt`, `dnf`, `pacman`, ecc.) per installare tutte le dipendenze necessarie.
L’installazione avviene con i seguenti comandi:
```
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh ./get-docker.sh --dry-run
```
#### Analisi del comando
- Il comando `curl` scarica lo script direttamente dal repository ufficiale di Docker, salvandolo in locale come `get-docker.sh`.
- Il comando `sh ./get-docker.sh` avvia lo script di installazione.
- Il **flag** `--dry-run` indica che l’installazione deve essere **simulata**, cioè vengono mostrate tutte le operazioni che verrebbero eseguite, ma senza effettuarle realmente.  
    Questo permette di verificare che non ci siano errori o conflitti prima dell’installazione effettiva.  
    Per installare davvero Docker, è sufficiente **rimuovere il flag `--dry-run`**.

Se tutto va a buon fine il tutto si deve visualizzare [[Output dell’installazione docker linux]]. 



## Link 
1) 