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
`Se il MAC è il "braccio" (l'hardware, i bit sul cavo, il controllo degli errori fisico), l'LLC (Logical Link Control) è la "mente" Si tratta anche del punto di congiuzione tra il livello 2 ed il livello 3.

È il sottolivello superiore del Data Link Layer, definito dallo standard **IEEE 802.2**. La sua esistenza serve a rendere il software (Livello 3 - Network) indipendente dall'hardware sottostante.
#### 1. Panorama: A cosa serve l'LLC?
Immagina che il tuo sistema operativo (Windows, Linux, Android) voglia inviare un pacchetto IP. Non gli importa se stai usando il Wi-Fi, un cavo Ethernet o una fibra ottica; lui vuole solo "spedire".
L'**LLC funge da interprete**: prende i dati dai protocolli di rete (IPv4, IPv6, IPX) e li prepara per il sottolivello MAC. Senza l'LLC, ogni protocollo di rete dovrebbe sapere esattamente come parlare con ogni tipo di scheda di rete esistente.
#### 2. Funzioni Principali
L'LLC svolge tre compiti critici:
1. **Multiplexing (Punti di Accesso al Servizio - SAP):** È la funzione più importante. Permette a più protocolli di livello superiore di condividere lo stesso collegamento fisico. Utilizza degli identificatori chiamati **DSAP** (Destination Service Access Point) e **SSAP** (Source Service Access Point) per capire a quale "ufficio" (protocollo) consegnare il pacchetto una volta arrivato a destinazione.
2. **Controllo di Flusso (opzionale):** Se il destinatario è troppo lento rispetto al mittente, l'LLC può inviare segnali per dire "rallenta!". Questo evita che i buffer di memoria si riempiano e i dati vadano persi.
3. **Controllo degli Errori Logici:** A differenza del CRC (che controlla se i bit sono corrotti), l'LLC può gestire la **ricevuta di ritorno (ACK)**. Se un frame non arriva, l'LLC può richiederne la ritrasmissione (anche se oggi questa funzione è quasi sempre delegata al protocollo TCP al Livello 4).
#### 3. Nozioni Tecniche e Tipi di Servizio
L'LLC offre tre modi diversi di comunicare, chiamati "Classi di Servizio":
- **Tipo 1 (Unacknowledged Connectionless):** È il più usato (es. in Ethernet). Non c'è conferma di ricezione e non si stabilisce una connessione. È veloce e "leggero". Se un frame si perde, pazienza (ci penserà il Livello 4).
- **Tipo 2 (Connection-Oriented):** Si stabilisce una connessione logica tra mittente e destinatario prima di inviare dati. Ogni frame deve essere confermato. Molto sicuro, ma molto lento.
- **Tipo 3 (Acknowledged Connectionless):** Una via di mezzo. Non c'è connessione fissa, ma ogni messaggio richiede una conferma immediata.
#### 4. L'intestazione LLC (Header)
Quando un pacchetto IP scende al livello LLC, gli viene messa una piccola "testata" prima di essere passato al MAC:

|DSAP (1 byte)|SSAP (1 byte)|Control (1/2 byte)|Information (Dati IP)|
|---|---|---|---|
|Indica il protocollo di destinazione|Indica il protocollo sorgente|Gestisce i numeri di sequenza e i tipi di frame|Il pacchetto vero e proprio|
**Curiosità Tecnica (SNAP):** Poiché lo spazio per il DSAP/SSAP era troppo piccolo (solo 1 byte), è stato creato il protocollo **SNAP (Sub-Network Access Protocol)**. È un'estensione dell'LLC che permette di identificare migliaia di protocolli diversi (come quelli usati oggi in internet) usando un codice a 2 byte chiamato **EtherType**.
- 

##### In sintesi: La catena di montaggio
1. **Livello 3:** "Ecco un pacchetto IPv4 per l'ufficio di fronte".
2. **LLC:** "Ricevuto. Ci metto l'etichetta 'Protocollo IP' (SAP) così il destinatario sa cos'è".
3. **MAC:** "Ok, ora ci metto il mio indirizzo fisico, quello del destinatario e calcolo il CRC per la sicurezza".
4. **Livello 1:** "Trasformo tutto in impulsi elettrici e vado!".


## Link 
1) 