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
`Racchiude tutto il sistema di build e deply del intera infrastruttura, senza avere msi deti dow time il tutto in maniera self hosted`

## Flusso del Codice e Deploy (CI/CD)
1) _Sviluppo_ Scrivo il codice nel mio PC personale
2) _Push_: il codice viene caricato sul mio server Gitea locale 
3) _**Automation:** **Gitea Actions**_: rileva il push 
	1) Crea un immagine docker 
	2) la salva nel **Docker Registry** interno 
4) _Update_: La Action esegue un comando di "refresh" sul server di produzione che scarica la nuova immagine e riavvia solo quel container.


## Spiegazione 
Sul mio PC in personale quello che uso per scrivere il codice gira Gitea lancio il push quando o terminato di implemntare quello che stavo facendo, successivamente questo fa svegliare il runner che legge le istruzione nel file `.yaml` esegue le istruzioni che sono:
- Creare una nuova immagine di docker 
Una volta che l'immagine e stata creata viene sotccata nel "Registri il magazino" e poi una volta fatto cio il ranner stesso mi si va a connettere al mio server in produzione e gli fa scaricare la nuova build una nuova immagine docker in sostanza, da li la esegue senz aperdita del servizio e questo come accade non capisco i vari pezzi che sono in gioco  









## Link 
1) [Gitea](https://about.gitea.com/)
2) [[Test del sistema in LOCALE]]