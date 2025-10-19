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
Un’**immagine Docker** è un **pacchetto immutabile** che contiene tutto ciò che serve per eseguire un’applicazione:
- l’eseguibile principale;
- le librerie e le dipendenze necessarie;
- eventuali strumenti di sistema;
- e una struttura di file system di base (simile a un mini sistema operativo).
A differenza di un semplice file binario o di un archivio, l’immagine Docker non contiene solo l’applicazione, ma **l’intero ambiente in cui essa è in grado di funzionare correttamente**.  
Questo approccio consente di garantire la **portabilità**: un’immagine creata su una macchina può essere eseguita su qualunque host Docker, indipendentemente dal sistema operativo sottostante (purché compatibile con il kernel).
Da una singola immagine è possibile **creare più container contemporaneamente**, ognuno indipendente dagli altri.  
In altre parole, l’immagine funge da modello, mentre i container rappresentano le istanze attive di quel modello.  
Questa caratteristica è cruciale per la scalabilità: si può avviare un numero arbitrario di container identici a partire dalla stessa immagine, permettendo un utilizzo efficiente delle risorse.
Le immagini Docker sono costruite secondo un modello **a livelli (layered)** [[Layer in docker]] a sua volta per creare questi livelli si usa il [[Il Dockerfile]].   
Un immagine docker spesso e compatibile anche con altri container engin questo e possibile grazie a [[Lo standard OCI (Open Container Initiative)]]

## Link 
1) 