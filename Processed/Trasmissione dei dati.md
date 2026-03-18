---
tipo: nota_lezione
corso: "Dashboard Networking Basics"
tags: [progetto, certificazioni, networkingBasics, Completed]
creato: 2026-03-16 15:01
---

# 📝 Lezione: Trasmissione dei dati
**Corso:** [[Dashboard Networking Basics]]

---
## Contenuto
## 1. Il Bit: L'unità fondamentale
- **Definizione:** Il termine **Bit** è l'abbreviazione di _Binary Digit_ (cifra binaria). Rappresenta la più piccola unità di informazione gestibile da un computer.
- **Valori:** Un bit può avere solo due stati: **0** o **1**.
- **Rappresentazione Fisica:** Questi "0" e "1" non sono magici, ma corrispondono a stati fisici reali:
    - Presenza o assenza di tensione elettrica (es. 0V o 5V).
    - Impulsi di luce (acceso/spento).
    - Direzioni di magnetizzazione (su hard disk).

## 2. Dal Bit al Byte (ASCII)
- **Il Byte:** Un gruppo di **8 bit** forma un **Byte**.
- **Codifica ASCII:** Per far sì che il computer capisca le lettere e i numeri umani, si usa un codice standard chiamato ASCII. In ASCII, ogni carattere è un byte.
    - Esempio: La lettera **A** maiuscola nel computer è memorizzata come `01000001`.
- **Traduzione:** * I dispositivi di **input** (tastiera, mouse) convertono i tuoi movimenti in binario.
    - I dispositivi di **output** (monitor, stampanti) convertono il binario in immagini o suoni comprensibili.

## 3. I Metodi di Trasmissione (I Media)
Una volta che i dati sono trasformati in bit, devono viaggiare attraverso un **media** (il mezzo fisico). Esistono tre modi principali:
#### A. Segnali Elettrici (Rame)
- I dati viaggiano come impulsi elettrici su cavi di rame.
- **Esempio:** Il classico cavo Ethernet (RJ45).
- **Uso:** Molto comune nelle case e nei piccoli uffici (SOHO).
#### B. Segnali Ottici (Fibra Ottica)
- I dati vengono convertiti in impulsi di luce.
- **Vantaggi:** Molto veloci e coprono distanze enormi senza perdere segnale.
- **Uso:** Grandi aziende, dorsali internet e connessioni FTTH.

#### C. Segnali Wireless (Onde Radio)
- I dati viaggiano nell'aria tramite onde elettromagnetiche (infrarossi, microonde, radio).
- **Esempio:** Wi-Fi, Bluetooth, 5G.

---

## Perché è importante per un Sistemista/Pentester?
1. **Troubleshooting:** Se un link di rete non va, devi sapere se il problema è fisico (cavo di rame rotto), elettromagnetico (interferenza sul Wi-Fi) o logico (bit errati).
2. **Sniffing (Pentesting):** Quando "intercetti" il traffico di rete, quello che vedi inizialmente sono serie di bit. Tool come **Wireshark** fanno il lavoro inverso: prendono i segnali elettrici/radio catturati dalla tua scheda di rete e li riconvertono in byte e poi in testo leggibile per permetterti di analizzarli.

---
## Collegamenti
- Torna al corso: [[Dashboard Networking Basics]]