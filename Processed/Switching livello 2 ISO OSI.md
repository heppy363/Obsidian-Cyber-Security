---
tipo: nota_lezione
corso: "Dashboard CompTIA Network+"
tags: [progetto, CompTIANetwork, certificazioni, Completed]
creato: 2026-02-19 15:43
---

# 📝 Lezione: Switching livello 2 ISO OSI
**Corso:** [[Dashboard CompTIA Network+]]

---
## Contenuto
`Si tratta di un componente fisico che possiamo definire il RE del livello due la sua caratteristica fondamentale e che riesce a leggere i Fraim e ne indivisdua i MAC destinatario e mittente`
#### Differenze tra hab e Switch
1) l'HAB opera al livello 1 questo non e intelligente e genera un unico dominio di rete quindi non si a un controllo della collisione e le macchine parlano in contemporanea si ha una collisione e "basta"
2) lo Switch questo genera dei domini di rete tanti quante sono le sue porte e per ognuno di essi tramite un bufer interno che contiene proprio gli indirizzi MAC, manda il messaggio solo al diretto interessato impedendo cosi che vi siano delle collisioni questa tecnica si chiama ***Micro-segmentazione***
#### Popolazione della tabella CAM 
Questa tabella contiene tutti gli indirizzi MAC delle macchine collegate allo Switch, grazie a questa e possibile far funzionare la Micro-segmentazione dato che permette di capire in quale porta dello Switch quale macchina e quindi quale MAC e associato ad essa. Naturalmente ce un fase di apprendimento dello Switch non conosce di defoult tutti gli indirizzi di tutte le macchine quindi la fase di apprendimento prevede questi punti:
1. Il PC "A" invia un frame al PC "B".
2. Lo switch riceve il frame sulla Porta 1.
3. Lo switch guarda il **MAC sorgente** di "A" e lo scrive in tabella: _"Il MAC di A si trova sulla Porta 1"_.
4. Lo switch guarda il **MAC di destinazione** ("B"). Se non sa dove sia "B", esegue il **Flooding**: invia il frame a tutte le porte tranne quella da cui è arrivato.
5. Quando "B" risponde, lo switch impara anche la sua posizione e la scrive in tabella. Da quel momento, il dialogo tra A e B sarà privato e diretto.
#### Metodi di invio del pacchetto 
Lo switch può decidere quanto velocemente inoltrare un frame. Esistono tre modalità principali:
- **Store-and-Forward:** Lo switch riceve l'**intero** frame, calcola il **CRC** per verificare che non ci siano errori e solo dopo lo inoltra. È il metodo più sicuro ma il più "lento" (latenza più alta).
	- [[Campo FCS CRC livello 2 ISO OSI]]
- **Cut-Through:** Lo switch legge solo i primi 14 byte (fino al MAC di destinazione) e inizia subito a trasmettere. È velocissimo, ma rischia di inoltrare frame corrotti perché non controlla il CRC.
- **Fragment-Free:** Una via di mezzo. Legge i primi 64 byte (dove avvengono la maggior parte delle collisioni) e poi inoltra.
#### Gestione del traffico  Unicast, Multicast e Broadcast
Lo switch gestisce i frame in tre modi diversi:
- **Unicast:** Da un MAC specifico a un altro MAC specifico (traffico normale).
- **Multicast:** Da uno a un gruppo (es. videoconferenze).
- **Broadcast:** Da uno a **tutti**. Il frame di broadcast ha come indirizzo MAC di destinazione tutti `F` (`FF:FF:FF:FF:FF:FF`).
    - _Nota Bene:_ Lo switch inoltra sempre i broadcast a tutte le porte. L'insieme di tutti i dispositivi che ricevono lo stesso broadcast si chiama **Dominio di Broadcast**.
### Sintesi Tecnica: Switch vs Hub

| Caratteristica   | Hub (L1)                    | Switch (L2)                   |
| ---------------- | --------------------------- | ----------------------------- |
| **PDU**          | Bit                         | Frame                         |
| **Intelligenza** | Nessuna (Ripete e basta)    | Legge i MAC Address           |
| **Collisioni**   | Frequenti (Unico dominio)   | Assenti (Micro-segmentazione) |
| **Sicurezza**    | Bassa (Tutti leggono tutto) | Alta (Traffico mirato)        |

#### Concetti avanzati 
- [[VLAN (Virtual Local Area Network) - Standard IEEE 802.1Q]]
- [[STP (Spanning Tree Protocol) - Standard IEEE 802.1D]]
- [[PoE (Power over Ethernet) - Standard IEEE 802.3af at bt]]


---
## Collegamenti
- Torna al corso: [[Dashboard CompTIA Network+]]