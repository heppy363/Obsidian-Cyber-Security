---
aliases:
  - Completate
tags:
  - Completed
  - Docker
  - Podman
---
--- 
## Nozioni
Nel panorama della containerizzazione moderna, **Docker** e **Podman** rappresentano due delle piattaforme più diffuse per la gestione dei container.  
Entrambi si basano sugli stessi principi di isolamento e portabilità delle applicazioni, e aderiscono allo [[Lo standard OCI (Open Container Initiative)]], che garantisce la compatibilità tra immagini e runtime.  
Tuttavia, le loro **architetture interne** e i **modelli di esecuzione** presentano differenze significative, soprattutto per quanto riguarda la gestione dei processi, i privilegi di esecuzione e la sicurezza.
### Docker
**Docker** è stato il **pioniere della containerizzazione moderna** e rimane tutt’oggi la piattaforma più diffusa e supportata nel settore.  
Introdotto nel 2013, Docker ha rivoluzionato il modo di distribuire applicazioni grazie alla semplicità con cui consente di creare, eseguire e orchestrare container, rendendo la tecnologia accessibile anche al di fuori dei contesti strettamente sistemistici.
#### Architettura e demone centrale
L’architettura di Docker si basa su un **demone centrale**, chiamato **Docker Daemon** (`dockerd`), che funge da intermediario tra il sistema operativo e i container.  
Tutte le operazioni eseguite tramite la **CLI** (Command Line Interface) o strumenti come **Docker Compose** vengono inoltrate al demone, che gestisce direttamente i container, le immagini, le reti e i volumi.
Questo modello **client-server** implica che:
- tutti i container sono **“figli” del demone centrale**;
- il demone mantiene il controllo e lo stato di ogni container in esecuzione;
- la comunicazione tra la CLI e il demone avviene tramite socket (spesso con privilegi elevati).
#### Privilegi e sicurezza
Un limite strutturale di Docker è che il suo demone deve essere eseguito con **privilegi di root**, poiché gestisce risorse di sistema sensibili come processi, file system e rete.  
Di conseguenza, anche i container lanciati dal demone vengono gestiti indirettamente da un processo con privilegi amministrativi.  
Questo modello ha suscitato alcune preoccupazioni in termini di sicurezza, poiché eventuali vulnerabilità del demone Docker possono potenzialmente compromettere l’intero sistema host.
#### Docker Compose
Un’altra caratteristica distintiva di Docker è **Docker Compose**, uno strumento che consente di **coordinare più container come parte di un unico stack di servizi**.  
Attraverso un semplice file YAML (`docker-compose.yml`), è possibile definire applicazioni multi-contenitore (ad esempio un server web, un database e un cache system) e gestirle come un insieme coerente.  
Compose rappresenta quindi un elemento chiave per la gestione di architetture **multi-servizio**, semplificando lo sviluppo e il deployment.

---

### Podman
**Podman** è una piattaforma di containerizzazione sviluppata da **Red Hat**, nata con l’obiettivo di fornire un’alternativa più **sicura, modulare e conforme agli standard** rispetto a Docker, pur mantenendo una piena compatibilità con esso.  
Podman utilizza le stesse specifiche OCI, quindi può eseguire le stesse immagini Docker senza alcuna modifica.
#### Architettura “daemonless”
A differenza di Docker, Podman adotta un’architettura **senza demone centrale (daemonless)**.  
In questo modello, **ogni container viene eseguito come un processo indipendente**, direttamente avviato e gestito dal kernel attraverso il container runtime (ad esempio `runc`).  
Non esiste un processo unico che controlla tutti i container: ciascun container è autonomo e il suo ciclo di vita è legato al processo che lo ha avviato.
Questo approccio offre diversi vantaggi:
- maggiore **modularità**, poiché non c’è un punto unico di fallimento (come il demone in Docker);
- maggiore **trasparenza**, in quanto ogni container può essere monitorato come un normale processo di sistema;
- possibilità di **esecuzione senza privilegi di root**.
#### Esecuzione rootless
Una delle innovazioni principali di Podman è la modalità di esecuzione **rootless**, cioè senza privilegi di amministratore.  
Podman sfrutta le funzionalità dei **Linux namespaces** per isolare i container anche quando vengono avviati da utenti non root.  
Questo riduce drasticamente i rischi di sicurezza, poiché un container compromesso non può avere accesso diretto al sistema host o ad altri container.
Tuttavia, in alcuni casi la modalità rootless può introdurre leggere limitazioni, ad esempio nella configurazione di reti complesse o nella gestione di alcune risorse del kernel, che richiedono privilegi elevati.
#### Podman Compose
Come Docker, anche Podman dispone di un proprio strumento per la gestione di **stack multi-contenitore**, chiamato **Podman Compose**.  
La sintassi e il funzionamento sono fortemente ispirati a Docker Compose, permettendo di definire e gestire gruppi di container correlati (ad esempio, un’applicazione e i suoi servizi ausiliari) in modo coerente.  
La principale differenza è che, mentre Docker utilizza un unico demone per orchestrare i container, Podman gestisce i processi in modo distribuito, ma garantendo la stessa compatibilità con i file `docker-compose.yml`.

---

### Compatibilità e interoperabilità
Uno degli aspetti più rilevanti di Podman è la sua **compatibilità quasi totale con Docker**.  
Entrambi utilizzano:
- immagini conformi allo **standard OCI**;
- lo stesso formato di **Dockerfile** per la build delle immagini;
- comandi CLI pressoché identici (tanto che il comando `podman` può spesso sostituire `docker` senza modifiche agli script).
In pratica, Podman può essere considerato un **sostituto drop-in** di Docker nella maggior parte dei casi.  
Le differenze emergono solo in aspetti avanzati di gestione, come il comportamento del networking o la gestione dei volumi in modalità rootless.

## Link 
1) 