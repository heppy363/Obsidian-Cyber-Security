---
aliases:
  - Completate
tags:
  - Completed
  - Docker
---
--- 
## Nozioni
Per creare un’immagine Docker si utilizza un file di configurazione testuale chiamato **Dockerfile**.  
Il Dockerfile descrive, passo per passo, come deve essere costruita l’immagine:  
specifica l’immagine di base da cui partire, i comandi da eseguire, le dipendenze da installare, i file da copiare e il comando principale da avviare.
Ogni istruzione del Dockerfile (come `FROM`, `RUN`, `COPY`, `CMD`) genera un nuovo **layer** dell’immagine.  
Questo meccanismo permette una costruzione modulare e riutilizzabile:  
immagini diverse possono condividere gli stessi layer di base, riducendo la ridondanza.  
Ad esempio, due applicazioni Python possono partire dallo stesso layer `python:3.12`, e Docker scaricherà solo una volta quell’immagine di base, “pagando” in termini di risorse solo la differenza nei layer superiori.

## Link 
1) 