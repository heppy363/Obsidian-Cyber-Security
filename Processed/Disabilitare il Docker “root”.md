---
aliases:
  - Completate
tags:
  - Completed
  - Docker
---
--- 
## Nozioni
Poiché il Docker rootless è completamente indipendente dal Docker classico, è consigliabile **disattivare il servizio principale** per evitare conflitti:
```
sudo systemctl disable --now docker
```
Dopo aver disabilitato il servizio tradizionale, è possibile eseguire di nuovo:
```
docker run hello-world
```
Questa volta, il comando verrà eseguito **senza privilegi di amministratore**, utilizzando la versione rootless di Docker.  
Il funzionamento sarà identico, ma con un livello di sicurezza superiore, poiché eventuali vulnerabilità nel container non potranno compromettere il sistema host.

## Link 
1) 