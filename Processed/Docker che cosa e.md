---
aliases:
  - Completate
tags:
  - Completed
  - Docker
  - Morrolinux
---
--- 
## Nozioni
Docker e un container engine, quindi e lo strumento che utilizziamo per andare a gestire dei container. Tramite esso possiamo _creare_, _amministrare_, _distruggere_ dei container, la sua filosofia e opensorse, per tanto il suo codice sorgente e disponibile a tutti. Possiede le seguenti caratteristiche:
- Un demone centrale che orchestra tutto il lavoro, questo pultroppo genera un unico punto di rottura se cosa lui cadono anche tutti i container in esecuzione. 
- Per impostazione predefinita esegue come _root_ sulla macchina host
- Fa da intermediario tra i container e il sistema oprativo vero e proprio della macchina host, per tanto non usa il kernel dei singoli container dato che non li anno ma usa quello del sistema operativo **host** [[Differenza tra container e macchina virtuale]]

**Docker** è una piattaforma completa basata sul concetto di container e sul proprio container engine.  
Offre non solo gli strumenti necessari per eseguire container, ma anche un intero ecosistema di gestione e distribuzione delle immagini.  
L’architettura di Docker si compone di tre elementi principali:
1. **Docker Engine**, che gestisce l’esecuzione dei container.
2. **Docker CLI e Docker Compose**, che offrono interfacce per definire e orchestrare container multipli.
3. **Docker Hub**, un registro pubblico di immagini preconfigurate pronte all’uso.

Docker ha avuto un enorme impatto sullo sviluppo software moderno, perché ha reso la containerizzazione **accessibile, portabile e standardizzata**.  
Le applicazioni containerizzate possono essere eseguite in modo identico su ambienti diversi (sviluppo, test, produzione), garantendo coerenza e semplificando la distribuzione.  
Sebbene i container non raggiungano il livello di isolamento delle VM, la loro **leggerezza, velocità di avvio e flessibilità** li rendono ideali per l’architettura a microservizi e per i moderni ambienti cloud.

Per poter eseguire e gestire i container, è necessario un componente software chiamato **container engine**.  
Il container engine ha il compito di **creare, avviare, fermare e isolare** i container, traducendo le richieste di questi ultimi in chiamate al kernel dell’host.  
In sostanza, funge da intermediario tra i container e il sistema operativo, gestendo anche la rete virtuale, il file system e l’allocazione delle risorse.  
Esempi di container engine includono **Docker Engine**, **containerd** e **CRI-O**.  
Il container engine si appoggia spesso su un **runtime** (ad esempio _runc_) che si occupa materialmente della creazione e dell’esecuzione dei processi isolati.

- [[Differenze tra Docker e Podman]]
- [[Installazione di docker]]







## Link 
1) 