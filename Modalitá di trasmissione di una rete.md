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
`A livello universitario, questo argomento si divide solitamente in due grandi categorie: la **direzionalità del flusso** (chi parla e quando) e la **natura del segnale** (analogico vs digitale).`

#### 1. Direzionalità del Flusso
Questa classificazione definisce come i dati si muovono fisicamente tra due nodi (A e B).
**Simplex (Unidirezionale)***
La comunicazione avviene in una sola direzione. Un dispositivo è solo trasmettitore, l'altro è solo ricevitore.
- **Caratteristica:** Tutta la larghezza di banda è usata in un unico senso. Non c'è possibilità di inviare feedback o conferme (ACK).
- **Esempio:** Trasmissione televisiva o radiofonica classica, cercapersone, sensori di sola lettura. 
 
 **Half-Duplex (Bidirezionale Alternata)**
I dati possono viaggiare in entrambe le direzioni, ma **non contemporaneamente**. Se A sta trasmettendo, B deve ascoltare e viceversa.
- **Caratteristica:** Il mezzo fisico è condiviso nel tempo. Richiede una gestione per evitare collisioni (se entrambi trasmettono insieme, il segnale si distorce).
- **Esempio:** Walkie-talkie (devi dire "passo" per liberare la linea), il vecchio standard Ethernet su bus (10BASE5) o il Wi-Fi (a livello fisico, il Wi-Fi è tipicamente half-duplex).

**Full-Duplex (Bidirezionale Simultanea)**
I dati viaggiano in entrambe le direzioni **contemporaneamente**.
- **Caratteristica:** È come avere due canali separati (uno per l'invio e uno per la ricezione) o usare tecniche di cancellazione dell'eco. È la modalità più efficiente perché non c'è attesa.
- **Esempio:** Telefonia moderna, Ethernet moderno (con switch e cavi TP), connessioni in fibra ottica dedicate.

#### 2. Trasmissione Seriale vs Parallela
Questa è un'altra distinzione tecnica fondamentale a livello fisico.
- **Trasmissione Parallela:** Si inviano più bit simultaneamente usando più fili fisici (es. 8 bit su 8 fili).
    - _Problema:_ Su lunghe distanze i bit arrivano "sfasati" (skew) a causa delle diverse resistenze dei fili.
    - _Uso:_ Vecchie stampanti (porta LPT), collegamenti interni alla scheda madre (bus dati).
- **Trasmissione Seriale:** I bit vengono inviati uno dopo l'altro su un unico canale.
    - _Vantaggio:_ Più economica, meno soggetta a interferenze, ideale per lunghe distanze.
    - _Uso:_ Praticamente tutto oggi: USB, SATA, Ethernet, Fibra.

#### 3. Trasmissione in Banda Base vs Banda Traslata
- **Banda Base (Baseband):** Il segnale digitale viene inviato così com'è (es. impulsi di tensione). Occupa tutto lo spettro del mezzo. (Esempio: Ethernet LAN).
- **Banda Traslata (Broadband):** Il segnale viene modulato su una frequenza portante più alta. Questo permette di usare la **FDM** per avere più canali sullo stesso cavo. (Esempio: Modem via cavo).

### Domande fondamentali per il livello 1
1) È seriale o parallelo? (Quasi sempre seriale nelle reti).
2) È Full-Duplex o Half-Duplex? (Fondamentale per capire se ci saranno collisioni).
3) Usa modulazione (Broadband) o segnali digitali diretti (Baseband)?

- [[Codifica di linea]]
## Link 
1) 