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
Con il tempo, il sistema può accumulare numerose immagini non più utilizzate (ad esempio versioni vecchie o dipendenze di immagini intermedie).  
Per liberare spazio, si può usare:
```
docker image prune
```
Questo comando elimina tutte le immagini **dangling**, ossia non collegate a nessun container attivo o fermo.
Per una pulizia più aggressiva (includendo anche i container e i volumi non in uso):
```
docker system prune
```
Docker chiederà conferma prima di procedere, mostrando la quantità di spazio che verrà liberata.
## Link 
1) 