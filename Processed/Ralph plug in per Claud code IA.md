---
aliases:
  - Completate
tags:
  - Completed
  - IA
  - progettiPersonali
  - ClaudIA
---
--- 
## Nozioni
Si tratta di un plug in per cloud AI che di fatto esegue questo script:
``` Bash
while ;: do cat PROMPT.md | claude-code; done 
```
quindi di fatto tutto quello che fa queto agente e prendere il nostro prompt e mandarlo dentro cloud di continuo e un sistema a `brutforce` dove col passare del tempo prima o poi l'IA ci dara il risultato che ci aspettiamo.

## Funzionamento del sistema
![[ralphschemadifunzionamento.png]]
1) Si parte dal idea quello che vuoi fare 
2) Dal idea si crea un PRD _prodact requirement documentation_ ovvero un documento che descrive la tua idea in maniera tecnica molto bene strutturata e precisa lo fa sempre l'IA 
3) Dal documento creato si passa a generare le task quindi le funzioni 
4) Poi si passa alle task quindi le operazioni minime delle funzioni 
5) Ralph prende il PRD controlla quale task sono disponibili avvia una nuova sessione pere eliminare la contest whindow si concentra sul completare la prima task libera 
6) Ralph rieseguire il punto 5 prende un altra task crea un nuova sessione completa la task e continua 
il concetto fundamentale e che il plug in reinizzializza tutte le volte un altra sessione questo per evitare il pribblema del _context rot_ ovvero che dalla meta in poi della finestra di contesto le performanc dei nostri modelle deperiscono molto velocemente 
Il file progres.txt tiene traccia di tutto il progresso del proggetto cosi da fare ripartire il sistema nel esatto momento in cui si e fermato 
- 
## Configurazione plug-in 
> prerequisito avere claud terminal sul proprio sistema [[Installare cloud CLI]]
1) Creare nel progetto il file `ralph.sa` lo si trova [qui](https://github.com/snarktank/ralph/blob/main/ralph.sh) 
2) Si devono implementare le skill corrette che sono [[Che cosa sono le skils di cloud IA]]
	1) PRD skill -> crea il documento di produzione 
	2) Ralph skill -> converte il PRD nel formato consono per ralph 
	3) sono entrambe [qui](https://github.com/snarktank/ralph/tree/main/skills) 
![[treeClaud.png]]
3) Ci si posiziona dentro la cartella di lavoro configurata al punto 2 si lancia il comando da terminare `claud` cosi da interagire con la CLI 
4) Controllare che sino presenti le due skills con il comando `/skills` devono essere due PRD e ralph 
5) Come prima cosa si usa la sckils PRD per la generazione del nostro documento di produzione
	1) la si usa facendo `/PRD` 
6) Si procede a descrivere la nostra idea in maniera piu o meno dettagliata 
7) Dal idea si andra a generare il PRD corrispondente e da esso il file `prd.json` e lo stesso file ma in formato consono per ralph 
8) Si lancia il comando `ralph` da li va agenerare il file progres.txt per tenere traccia di tutto il proggetto e il suo stato di avanzmamento 
9) Una volta che sono pronti tutti i file si procede a lanciare il comando `.\ralph.sh` gli si da il numero massimo di interazioni per liminarlo e non farlo andare al infini e lui inizia a lvorare 
	1) lo si esegue da whindwos se si ha ghit cosi `sh ralph.sh --tool claude 10` cambiare 10 con il numero di interazioni 
	2) 

- [[Specifiche file ralph.sh claud code]] 
- [[Risoluzioni problemi Ralph whindows]]

## Link 
1) [Ralph originale](https://github.com/frankbria/ralph-claude-code)