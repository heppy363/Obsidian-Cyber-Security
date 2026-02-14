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
`Lo scopo di questo livello e tarsferire i dati in maniera affidabile al livello 3 oppure prenderli dal livello 3 per passarli al livello 1 in maniera coerente`

### Funzioni principali 
1) _Framing_: prende i pacchetti del livello 3 e gli aggiunge un intestazione in coda generando cosi il _Frame_ (la trama)
2) _Indirizzamento Fisico_: utilizza gli _indirizzi MAC_ per identificare mittente e destinatario nella rete locale (capisce cosi a chi mandare il messaggio) 
3) _Controllo degli errori_: rivela se i bit sono stati danneggiati durante il trasporto questo grazie al [[Campo FCS CRC livello 2 ISO OSI]] 
4) _Controllo del flusso_: evita che un trasmettitore veloce affoghi un ricevente lento 
5) _Controllo del accesso MAC_: stabilisce quelle macchina comunica in caso di un unico cavo che stabilisce la connessione oppure frequenza 
### Divisione del livello 
Al interno del livello 2 si possono distingue due parti distinti e fondamentali:
- [[MAC livello 2 ISO OSI]]
	- piu vicino al livello 1
	- Gestisce l'accesso fisico al cavo e l'indirizzo HW
- [[LLC livello 2 ISO OSI]]
	- Piu vicino al livello 3
	- Comunica con il livello 3 gestendo gli indirizzi IP e ha lo scopo di controllare gli errori
**Nota importante:** Il Livello 2 di base _non chiede la rispedizione_ del frame se è corrotto (non è "affidabile" in quel senso). Semplicemente lo butta via. Saranno i livelli superiori (come il TCP al Livello 4) a accorgersi che manca qualcosa e a chiederne l'invio di nuovo.
![[Composizionelivello2.jpg]]

### Protocolli principali 
[[Differenza tra protocollo e standard]]
Nel ambito delle rete cablate il protocollo piu usate ancora ad oggi 2026 e quello del **Ethernet** (IEEE 802.3), non si tratta del unico:
- **Ethernet:** Per reti LAN cablate.
- **Wi-Fi (IEEE 802.11):** Per il collegamento dati via radio.
- **PPP (Point-to-Point Protocol):** Usato per connessioni dirette tra due nodi (comune nelle vecchie ADSL).
- **ARP (Address Resolution Protocol):** Un "protocollo di confine" fondamentale che serve a trovare l'indirizzo MAC conoscendo l'indirizzo IP.
- [[Switching livello 2 ISO OSI]]
- [[Protocollo ARP livello 2 ISO OSI]]

## Link 
1) 