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
Se tutto va a buon fine, al termine dell’installazione Docker mostra un **riepilogo dettagliato** della configurazione del sistema, distinguendo chiaramente tra la parte **client** e la parte **server** del motore Docker.
Esempio di output:

```
Client: Docker Engine - Community
 Version:           28.5.1
 API version:       1.51
 Go version:        go1.24.8
 Git commit:        e180ab8
 Built:             Fri Oct 10 13:04:33 2025
 OS/Arch:           linux/amd64
 Context:           default

Server: Docker Engine - Community
 Engine:
  Version:          28.5.1
  API version:      1.51 (minimum version 1.24)
  Go version:       go1.24.8
  Git commit:       f8215cc
  Built:            Fri Oct 10 13:04:33 2025
  OS/Arch:          linux/amd64
  Experimental:     false
 containerd:
  Version:          v1.7.28
  GitCommit:        b98a3aace656320842a23f4a392a33f46af97866
 runc:
  Version:          1.3.0
  GitCommit:        v1.3.0-0-g4ca628d1
 docker-init:
  Version:          0.19.0
  GitCommit:        de40ad0

```

#### Interpretazione
Questo output può essere suddiviso in due sezioni principali:
1. **Client: Docker Engine - Community**  
    Questa sezione fornisce informazioni sul **client Docker** installato nella macchina locale.  
    Il client è l’interfaccia che permette all’utente di interagire con il demone Docker, inviando comandi e ricevendo risposte tramite API.  
    Include dettagli come la versione, il linguaggio di compilazione (`Go`), l’architettura e il contesto di esecuzione.
2. **Server: Docker Engine - Community**  
    Qui troviamo invece le informazioni relative al **server Docker**, ossia il **demone centrale** (`dockerd`) che gestisce realmente i container.  
    Questa parte mostra la versione del motore Docker, il container runtime utilizzato (`runc`), e i componenti interni come `containerd` e `docker-init`.  
    È la componente che interagisce con il kernel del sistema operativo per creare, isolare e gestire i container.

Se si visualizza correttamente questo output allora si puo procedere con [[Verifica dello stato del servizio Docker]]

## Link 
1) 