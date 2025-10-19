---
aliases:
  - Completate
tags:
  - Completed
  - Docker
---
--- 
## Nozioni
All’interno di un registro, le **repository** rappresentano le **unità logiche di organizzazione** delle immagini.  
Ogni repository contiene **tutte le versioni di una specifica immagine** di un’applicazione o di un componente software.  
In termini pratici, una repository è simile a un “contenitore di immagini versionate”.
Ad esempio, una repository chiamata `nginx` può contenere le immagini:
- `nginx:1.23`
- `nginx:1.24`
- `nginx:latest`
Dove ogni tag (`1.23`, `1.24`, `latest`) identifica una **versione specifica dell’immagine**.  
Questo meccanismo consente di mantenere la tracciabilità delle varie release di un’applicazione e di poter eseguire rapidamente rollback o test su versioni differenti.
Ogni immagine all’interno di una repository aderisce a un formato standardizzato, in modo che sia **compatibile e interoperabile** con qualunque container engine conforme allo standard.

## Link 
1) 