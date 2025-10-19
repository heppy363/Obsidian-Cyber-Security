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
Docker consente di esplorare la **composizione interna** di un’immagine per comprendere come è stata costruita, layer per layer.  
Questo è particolarmente utile per analizzare immagini di terze parti o ottimizzare le proprie.
```
docker history <nome_immagine>
```
Esempio:
```
docker history ubuntu:22.04
```
Il comando mostra:
- l’elenco dei **layer**,
- la dimensione di ciascuno,
- e il **comando** che ha generato quel layer (ad esempio un’istruzione `RUN` o `COPY` nel Dockerfile).
Questo permette di **verificare l’efficienza** di un’immagine (es. evitare layer duplicati o troppo grandi) e di capire la logica di costruzione.







## Link 
1) 