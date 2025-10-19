---
aliases:
  - Completate
tags:
  - Completed
  - Docker
---
--- 
## Nozioni
Per controllare che il servizio sia attivo, si utilizza:
```
systemctl status docker --user
```
Esempio di output:
```
● docker.service - Docker Application Container Engine (Rootless)
     Loaded: loaded (/home/user/.config/systemd/user/docker.service; enabled)
     Active: active (running) since Sat 2025-10-18 07:31:26 CEST; 38s ago
       Docs: https://docs.docker.com/go/rootless/
   Main PID: 4419 (rootlesskit)
      Tasks: 43
     Memory: 46.6M
     CPU: 399ms
```
Questo mostra che il **servizio Docker rootless** è in esecuzione come servizio utente (`--user`) e non come servizio di sistema.  
La presenza del processo `rootlesskit` indica che il sistema sta effettivamente utilizzando un livello di virtualizzazione utente per isolare i container.
## Link 
1) 