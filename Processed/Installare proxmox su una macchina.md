---
tipo: nota_lezione
corso: Proxmox
tags:
  - progetto
  - proxmox
  - Completed
  - H-net
creato: 2026-02-19 09:50
---

# 📝 Lezione: Installare proxmox su una macchina
**Corso:** [[Proxmox]]

---
## Contenuto
### Che cosa e 
Si tratta di un sistema operativo hyper vison, basato su linux quindi un sistema operativo che ti permette in maniera nativa di creare macchine virtuale [[Processed/Container]], il tutto lo fa grazie alla tecnologia di [[hyper-V]] i vantaggi essenziali sono che posso avere molteplici sistemi operativi o appunto container sul mio PC senza dover avere del HW aggiuntivo. 


### Installazione 
Si parte scaricando la ISO del sistema operativo, da li l'installazione la si puo eseguire in maniera praticamente standard senza troppa differenza rispetto ad un sistema operativo "Tradizionale", si puo instllare il tutto da UI o da terminale o anche via rete quindi con ETH.
- Si consideri che durante la instalazione il sistema operativo ricerca in maneira automatica se la nostra macchina supporta il sistema di virtualizzazione quindi parliamo proprio della tecnologia del nostro processore se questo ultimo puo supportare la accellerazione HW della virtualizzazione non si tratta di una prerogativa ma se lo abbiamo e bene attivarlo da BIOS dato che le prestazioni genrali delle macchine aumentano molto.
Un concetto fondamentale e quello dei discki e la loro gestione di fatto proxmox consnete di usare molti tipi di file sistem, per una situazione di test o non eccessivamente utilizzata va bene [[Processed/EXT4]] per una situazione piu prodaction ready meglio [[Processed/EXT4]]. 
1) Il punto fondamentale di questo sistema, e la sua interfaccia Web che la si ottiene post installazione accedendo al indirizzo IP che abbiamo configurato per la nostra macchina. 
2) Proxmox permette di avere piu macchina nello stesso datacente che i scambiano informazioni tra di loro.

---
## Collegamenti
- Torna al corso: [[Proxmox]]
- In questo video ti viene anche detto come risolvere gli errori [qui](https://www.youtube.com/watch?v=WGPGVoFcqmM)