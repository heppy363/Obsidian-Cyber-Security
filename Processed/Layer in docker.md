---
aliases:
  - Completate
tags:
  - Completed
  - Docker
  - Immagini
---
--- 
## Nozioni
Le immagini Docker sono costruite secondo un modello **a livelli (layered)**.  
Ogni immagine è composta da una serie di **layer**, ossia strati che rappresentano _modifiche_ incrementali al _file system_.  
Ogni layer contiene solo la differenza rispetto a quello precedente (ad esempio, l’aggiunta di un file, una libreria o una configurazione).
Questo sistema consente un’elevata **efficienza nello storage e nel download**:
- se due immagini condividono alcuni layer (ad esempio le stesse librerie di base), questi vengono **scaricati e memorizzati una sola volta**;
- quando si aggiorna un’immagine, Docker scarica solo i **nuovi layer** o quelli modificati, riducendo tempi e consumo di banda;
- in fase di build, i layer già esistenti possono essere **riutilizzati tramite cache**, accelerando la generazione di nuove immagini.
Ogni layer è **immutabile**: se un layer viene modificato, Docker crea un nuovo layer sopra i precedenti, mantenendo intatti quelli sottostanti.  
Questa architettura a strati garantisce coerenza e tracciabilità, oltre a facilitare il versionamento e la distribuzione delle immagini.

## Link 
1) 