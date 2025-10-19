---
aliases:
  - Completate
tags:
  - Completed
  - Docker
  - Container
---
--- 
## Nozioni
Un **container**, in contrapposizione all’immagine, rappresenta **un’istanza in esecuzione** dell’immagine stessa.  
Mentre l’immagine è statica, il container è dinamico: quando viene avviato, Docker crea un [[Layer in docker]] “in scrittura” sopra tutti i layer immutabili dell’immagine.  
Questo layer temporaneo consente al container di modificare file e dati durante l’esecuzione, senza alterare l’immagine di origine.  
Quando il container viene eliminato, anche questo layer viene distrutto, garantendo che l’immagine rimanga intatta e riutilizzabile per future istanze.
Dal punto di vista del sistema operativo, un container è **un gruppo di processi isolati**, che condividono il kernel dell’host ma non hanno visibilità sull’intero sistema.  
Il container vede solo le risorse che gli vengono assegnate esplicitamente (CPU, memoria, rete, volumi, ecc.), e non può accedere a quelle degli altri container o dell’host, a meno che non sia configurato diversamente.  
Questa forma di isolamento è ottenuta attraverso meccanismi del kernel Linux come **namespaces** (per isolare processi, rete e file system) e **cgroups** (per limitare e monitorare l’uso delle risorse).
Dal punto di vista operativo, un container viene trattato come un normale processo di sistema, ma con uno spazio di esecuzione separato.  
Ciò consente di avviare e arrestare container in pochi istanti, di ridimensionare risorse in tempo reale e di ottenere un comportamento uniforme tra ambienti diversi (sviluppo, test, produzione).

### In sintesi
In conclusione, l’**immagine Docker** può essere vista come la “fotografia” di un ambiente di esecuzione, mentre il **container** rappresenta l’“esecuzione viva” di quella fotografia.  
Grazie all’architettura a **layer** e al meccanismo di build basato sul **Dockerfile**, Docker riesce a garantire efficienza, modularità e portabilità, diventando lo standard de facto per la distribuzione e l’esecuzione di applicazioni moderne in ambienti cloud-native.

## Link 
1) 