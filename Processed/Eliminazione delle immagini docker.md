---
aliases:
  - Completate
tags:
  - Completed
  - Docker
---
--- 
## Nozioni
Per rimuovere un’immagine specifica:
```
docker rmi <nome_immagine>:<versione>
```
Esempio: 
```
docker rmi ubuntu:22.04
```
L’immagine può essere rimossa solo se **non è in uso da alcun container**.  
In caso contrario, Docker restituirà un errore che indica quali container stanno ancora utilizzando quella risorsa.
Per forzare la rimozione (inclusi i container associati), si può aggiungere il flag `-f`:
```
docker rmi -f <nome_immagine>
```

## Link 
1) 