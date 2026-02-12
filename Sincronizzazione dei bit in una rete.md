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
La **sincronizzazione dei bit** e una delle parti piu critiche di una rete la problematica la si puo ridurre al coordinamento dei clock (gli orologi interni) del trasmettitore e del ricevente, senza questo passaggio il ricevente non potrebbe sapere quando termina un "1" oppure inizia uno "0" e si potrebbe incombere in _errori di duplicazione_ o di _campionamento_ (es: interpretare due "1" come uno solo). 
Tutti questi problemi si affrontano e risolvono, con differenti modelli di trasmissione sulla rete stessa i principali sono i seguenti. 

#### 1. Trasmissione Asincrona
In questa modalità, la sincronizzazione non è continua, ma avviene "per carattere" o per piccoli blocchi di dati.
- **Funzionamento**: il trasmettitore aggiunge dei bit extra di inizio e fine trasmissione (avvisa il ricevente che inizia a termina la trasmissione)
- **Caratteristiche** 
	- il ricevente _resetta_ il suo orologio ad ogni bit di start 
	- semplice ed economico 
	- _ineficenza_: c'e un altro overhead circa il 20-25% viene sprecato per i bit di controllo di inizio e fine comunicazione 
_Esempio_ le vecchie porte seriali _RS-232 COM_ o la comunicazione tra microcontrollori via _UART_ 

#### 2. trasmissione sincrona 
Qui i bit vengono inviati senza un controllo di inizio e di fine abbiamo un flusso continuo quindi niente start/stop. In questa tipo di trasmissione e fondamentale che il trasmettitore e il ricevente siano perfettamente allineati a livello temporale (i clock non devono essere sfalsati), per fare questo esistono vari modi:
**A. Sincronizzazione tramite Canale Separato**
In questo tipo di sincronizzazione si ha un canale separato per l'invio effettivo del clock, quindi banalmente un cavo apposto 
- **Esempio**: L'interfaccia **SPI** (Serial Peripheral Interface) nei sistemi embedded, dove il master invia il segnale di clock su un pin chiamato SCK (Serial Clock).
- **Limite:** Non è scalabile su lunghe distanze (il segnale di clock e i dati potrebbero subire ritardi diversi, un fenomeno chiamato _clock skew_).
**B. Sincronizzazione tramite Codifica (Self-Clocking)** 
Si tratta della soluzione piu usata nelle reti moderne, questa tecnica consiste nel "nascondere" il segnale di clock al interno dei dati stesso questo avviene tipicamente tramite il transizioni di tensione.
- **Codifica Manchester:** non si guarda il livello di tensione ma la direzioni delle passaggio di informazioni:
	- Esempio: Una transizione da Basso ad Alto = "1", da Alto a Basso = "0".
	- Poiché c'è una transizione in ogni bit, il ricevitore può usarla per ricalibrare il proprio clock continuamente.
	- **Uso:** [[Definizione di uno standard]] **Ethernet 10BASE-T**. 
- **Scrambling (Mescolamento):** Nelle reti ad alta velocità (come Gigabit Ethernet), si usano algoritmi matematici per evitare lunghe sequenze di "0" o "1" identici, forzando cambiamenti di stato che permettono al ricevitore di rimanere sincronizzato.

#### Problemi Critici: Il "Jitter" e il "Clock Drift"
Nello studio universitario ti verrà chiesto cosa può andare storto:
1. **Clock Drift (Deriva del Clock):** Gli oscillatori al quarzo non sono mai identici al 100%. Se il clock del mittente è leggermente più veloce di quello del ricevitore, dopo migliaia di bit il ricevitore inizierà a leggere il bit sbagliato.
2. **Jitter:** È la variazione temporale della posizione dei fronti del segnale rispetto alla loro posizione ideale. Può essere causato da interferenze elettromagnetiche o surriscaldamento dei componenti.

#### Caratteristiche delle due metodologie 

| **Caratteristica**            | **Asincrona**              | **Sincrona (Self-clocking)**  |
| ----------------------------- | -------------------------- | ----------------------------- |
| **Unità di sincronizzazione** | Singolo carattere (byte)   | Blocco di bit (frame)         |
| **Efficienza**                | Bassa (bit start/stop)     | Alta                          |
| **Complessità Hardware**      | Bassa                      | Alta                          |
| **Esempio tipico**            | Tastiere, Sensori semplici | Ethernet, Fibra Ottica, Wi-Fi |

#### Quanti dati posso passare 
La **Multiplazione (Multiplexing)**, definisce **"quanti"** segnali indipendenti possono condividere lo stesso mezzo fisico contemporaneamente. In pratica, è la tecnica che permette di ottimizzare la larghezza di banda (bandwidth) per non stendere un cavo per ogni singola comunicazione.
- [[Multiplazione quando dati passano in una singola linea]]

## Link 
1) 