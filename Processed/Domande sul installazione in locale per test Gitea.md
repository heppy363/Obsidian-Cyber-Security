---
aliases:
  - Completate
tags:
  - Completed
  - progettiPersonali
  - blog
  - CI/CD
---
--- 
## Nozioni
`Domande che mi sono venute in mente durante la configurazione` 

### 1. L'Action si applicherà a tutti i repository?
**No.** Per come l'abbiamo configurata, l'Action vive **solo** dentro quel repository specifico perché il file `.gitea/workflows/deploy.yaml` si trova fisicamente in quella cartella.
- **Se crei un nuovo repository:** Dovrai copiare la cartella `.gitea` nel nuovo progetto.
- **Se vuoi un'Action "globale":** Gitea permette di creare repository di "template" o workflow condivisi, ma per ora la pratica migliore è personalizzare il file `.yaml` per ogni progetto (perché un progetto Flask sarà diverso da uno in Node.js o Go).
- Questo ci fa capire che le action sono baindate al singolo progetto e quindi esso ne definisce la costruzione e come il server buildera il codice finale 




## Possibili migliorie 
- **Aggiungere un Database:** Collegare un container Postgres o MySQL al tuo Flask tramite l'Action.
- **Notifiche:** Far sì che Gitea ti mandi un messaggio (Telegram/Discord) se il deploy fallisce.






## Link 
1) 