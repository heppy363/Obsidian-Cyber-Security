---
tipo: nota_lezione
corso: "Dashboard CompTIA Network+"
tags: [progetto, CompTIANetwork, certificazioni, Completed]
creato: 2026-02-19 15:42
---

# 📝 Lezione: MAC livello 2 ISO OSI
**Corso:** [[Dashboard CompTIA Network+]]

---
## Contenuto
`Si tratta della parte piu bassa del livello 2 che comunica a stretto contatto con il livello 1`

### Scopo
Inserisce nel Fraim (PDU livello 2) l'indirizzo MAC del destinatario, ogni NIC ha un indirizzo MAC a 48 bit questo deve essere inserito in coda al fraim per identificare a quale host della rete il messaggio e destinato.
1) Regole di accesso al mezzo: stabilisce in una rete quale dispositivo puo o meno inviare informazioni, di base ci sono due principali metodologie 
	1) CSMA/CD = questo viene usato nelle reti cablate, le macchine ascolta se in quel cavo si ha o meno la possibiltia di parlare, in caso di due macchine che parlano contemporaneamente, si interrompe la comunicazione e si attende un _lasso di tempo causale_ per ritentare la comunicazione 
	2) CSMA/CA = questa viene usate nelle comunicazione senza cavi, non vi e la possibilita di rilevare le collisioni e quindi si attende il permesso di parlare, si usa il _3-Way-And-Shake_ 
2) Delimitazione delle trama: aggiunge una serire di bit al inizio e alla fine della trama cosi da far capire al ricevente quando questa termina e quando ne inizia una nuova 

---
## Collegamenti
- Torna al corso: [[Dashboard CompTIA Network+]]