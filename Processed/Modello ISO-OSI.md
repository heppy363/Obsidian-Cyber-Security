---
aliases:
  - Completate
tags:
  - Completed
  - CompTIAnetwork
  - Certificati
---
--- 
## Nozioni

#### Che cosa e 
Si tratta di uno _standard_ adottato nel 1984 che divide le funzioni di rete per permettere a sistemi _eterogeni_ di comunicare tra di loro, questo viene fatto dividendo la struttura di rete in 7 livelli principali. 
1) Fisico 
2) Collegamento Dati
3) Ntworck 
4) Trasporto 
5) Sessione 
6) Presentazione 
7) Applicazione 
Il funzionamento si basa sul principio che questo sistema riceve i dati dal livello inferiore e li impacchetta per il livello successivo (la stessa cosa avviene anche la contrario), lo si puo vedere da due punti di vista:
- Chi manda i dati chi riceve i dati -> in questo caso partiamo dal basso quindi dal livello 1 fino al livello 7, dato che vogliamo mandare informazioni ad una entita della rete 
- Chi riceve i dati chi manda i dati -> in questo caso lo si vede dal altro dal livello 7 al livello 1 quindi siamo noi a ricevere i dati e li vogliamo "Decifrare"
Il principio base della rete e l' [[Incapsulamento]] 

#### Differenza tra modello ISO OSI e TCP/IP 
Si considera il modello ISO OSI la parte "teorica" di fatto questo e come e stato ipotizzato il trasferimento dei dati da delle entita eterogenee, mentre in un sistema reale ai giorni nostri si considera il modello TCP/IP dove i livelli diventano _4_ al posto _7_
- Network acces layer -> gestisce il collegamento tra le macchine permettendo la mappatura logico fisica 
- Internet Layer -> gestisce l'instradamento dei pacchetti tramite il protocollo IP  
- Transport layer -> gestisce la consegna dei dati alla varie macchina e consente il controllo del flusso come grazie al protocollo TCP 
- Applciation layer -> gesisce la rappresentazione dei dati ad alto livello 



- [[Modello ISO OSI mappa.canvas]]
## Link 
1) 