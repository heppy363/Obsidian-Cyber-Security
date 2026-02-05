---
aliases:
  - Completate
tags:
  - Completed
  - H-net
  - IA
---
--- 
## Nozioni
## Guida all'assemblaggio "Critico"
### Il Cablaggio (Il punto dove si rischia il fumo)
Le Tesla P40 hanno un connettore femmina a 8 pin che è **meccanicamente ed elettricamente diverso** dalle schede gaming.
- **Errore comune:** Usare un cavo PCIe 8-pin dell'alimentatore. La forma dei quadratini è diversa e, se forzato, mandi i 12V dove dovrebbe esserci la terra.
- **Soluzione:** Devi usare il cavo sdoppiatore che spesso viene fornito con le Tesla (2x PCIe 8-pin femmina → 1x Tesla 8-pin maschio). Assicurati che ogni P40 riceva alimentazione da **due cavi separati** provenienti dall'alimentatore per evitare di sciogliere i connettori.
### Flusso d'aria
Le P40 sono "passive". Devi costruire o stampare in 3D dei convogliatori (shroud) che si incastrano sul retro della scheda, dove attaccherai le ventole Delta ad alta pressione. Senza questo, le schede andranno in _thermal throttling_ in meno di 60 secondi.

## Link 
1) 