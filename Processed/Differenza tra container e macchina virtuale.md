---
aliases:
  - Completate
tags:
  - Completed
  - Docker
  - Macchina/virtuale
  - Container
---
--- 
## Nozioni
Nel contesto della virtualizzazione e della gestione delle risorse di sistema, è importante distinguere tra **macchine virtuali (VM)** e **container**, due approcci che, pur condividendo l’obiettivo di isolare e gestire applicazioni in ambienti controllati, si basano su principi architetturali profondamente diversi.

### Macchine Virtuali
Una **macchina virtuale** è un’istanza software che emula un intero computer fisico. Essa esegue un **sistema operativo completo** (chiamato “guest OS”) sopra un software chiamato **hypervisor**, il quale si interpone tra l’hardware reale e i sistemi operativi virtualizzati.  
L’hypervisor ha il compito di **virtualizzare le risorse fisiche** — CPU, memoria, storage e periferiche — rendendole disponibili a ciascuna macchina virtuale in modo isolato.  
In questo modello, ogni VM dispone di un proprio **kernel**, di un file system indipendente e di un set completo di librerie e servizi di sistema.  
Questo garantisce un **forte isolamento** tra le macchine virtuali, poiché un errore o un attacco in una VM difficilmente può propagarsi alle altre. Tuttavia, l’architettura introduce un notevole **overhead**: ogni livello di astrazione (OS guest → hardware virtuale → hypervisor → hardware reale) aggiunge latenza e consumo di risorse.  
Di conseguenza, le prestazioni complessive risultano inferiori rispetto a un’esecuzione nativa e la gestione delle risorse (come la variazione di RAM o CPU) richiede spesso il riavvio della VM.  
Le macchine virtuali sono ideali per scenari in cui è necessario eseguire **sistemi operativi differenti** sullo stesso host, o quando l’isolamento e la sicurezza sono prioritari rispetto alla leggerezza e alla velocità.

### Container
I **container**, al contrario, rappresentano un approccio di virtualizzazione più leggero e orientato ai processi.  
Invece di emulare un intero sistema operativo, i container **condividono il kernel** del sistema operativo host e si limitano a isolare solo lo spazio utente (user space) di ciascuna applicazione.  
Ogni container contiene solo ciò che è strettamente necessario per eseguire un’applicazione: binari, librerie, dipendenze e configurazioni.  
Questo approccio elimina completamente la necessità di un hypervisor, riducendo drasticamente l’overhead e migliorando le **prestazioni**.  
L’esecuzione dei container è quasi immediata, poiché si tratta di **processi isolati** che il sistema operativo gestisce come qualunque altro processo nativo.  
Tuttavia, questo comporta un **isolamento più debole** rispetto alle macchine virtuali, poiché tutti i container condividono lo stesso kernel: un bug nel kernel dell’host può potenzialmente compromettere tutti i container.  
Un ulteriore vantaggio è la possibilità di **modificare le risorse assegnate** (CPU, memoria, limiti di rete, ecc.) **in tempo reale**, senza interrompere l’esecuzione dei container, cosa molto utile nei contesti cloud-native e DevOps.

### Conclusione
In sintesi, la differenza principale risiede nel **livello di virtualizzazione**:
- Le **macchine virtuali** emulano l’intero hardware e ospitano sistemi operativi completi, offrendo un isolamento totale ma con costi in termini di prestazioni.
- I **container**, invece, condividono il kernel dell’host e isolano solo i processi, ottenendo performance molto più elevate a scapito di un isolamento meno rigoroso.
- Il **container engine** è il componente tecnico che permette ai container di esistere e comunicare con l’host.
- Infine, **Docker** è la piattaforma più diffusa che implementa e semplifica l’uso dei container, diventando di fatto lo standard di riferimento nel campo della containerizzazione moderna.







## Link 
1) 