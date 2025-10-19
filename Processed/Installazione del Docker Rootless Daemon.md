---
aliases:
  - Completate
tags:
  - Completed
  - Docker
---
--- 
## Nozioni
Docker fornisce uno script dedicato per abilitare questa modalità:
```
dockerd-rootless-setuptool.sh install
```
Questo comando configura un ambiente Docker isolato per l’utente corrente, impostando i permessi necessari all’interno della propria **home directory** (senza scrivere nulla nelle directory di sistema).  
In particolare, viene installata una versione del demone Docker che utilizza i **user namespaces** del kernel Linux per simulare un ambiente “root” virtuale, mantenendo tuttavia la sicurezza dell’utente non privilegiato.
- [[Verifica del servizio Rootless docker]]
- 

## Link 
1) 