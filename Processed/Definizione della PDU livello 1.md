---
tipo: nota_lezione
corso: "Dashboard CompTIA Network+"
tags: [progetto, CompTIANetwork, certificazioni, Completed]
creato: 2026-02-19 15:34
---

# 📝 Lezione: Definizione della PDU livello 1
**Corso:** [[Dashboard CompTIA Network+]]

---
## Contenuto
al **Livello 1** non esiste un vero e proprio "pacchetto" o "contenitore" logico. Quelli appartengono ai livelli superiori.
Tuttavia, i bit non vengono sparati nel cavo in modo totalmente casuale. Vediamo come vengono definiti e "modellati" a questo livello.

## 1. L'Unità di Misura: La PDU (Protocol Data Unit)
Nel modello OSI, ogni livello ha la sua unità di dati.
- Per il Livello 2 è il _Frame_.
- Per il Livello 3 è il _Pacchetto_.
- Per il **Livello 1**, la PDU è semplicemente il **BIT**.

**Caratteristiche del dato al Livello 1:**
- **Forma:** Non hanno una "forma" intesa come struttura dati software, ma hanno una **forma d'onda** (elettrica, ottica o radio).
- **Lunghezza:** Un bit non ha una "lunghezza" in byte, ma ha una **durata temporale** (Tb​), che è l'inverso della velocità di trasmissione (Tb​=1/bps). Ad esempio, in una rete a 1 Gbps, un bit dura esattamente 1 nanosecondo.

## 2. La "Struttura" Fisica: Il Preambolo
Anche se il Livello 1 trasmette bit, molti standard (come l'Ethernet) aggiungono una sequenza di bit specifica prima che inizino i dati veri e propri (il Frame del Livello 2). Questa sequenza è parte integrante del lavoro del Livello Fisico.
### Il Preambolo (Preamble)
È una sequenza fissa di bit (alternanza di 0 e 1) che serve a "svegliare" il ricevitore.
- **Funzione:** Permette al ricevitore di agganciare il clock (sincronizzazione) del trasmettitore.
- **Esempio Ethernet:** Consiste in 7 byte di `10101010` seguiti da 1 byte chiamato **SFD (Start Frame Delimiter)** `10101011`.
- **Importanza:** Il Livello Fisico "vede" questi bit, li usa per stabilizzare il segnale e, una volta arrivato all'SFD, avvisa il Livello 2: _"Ehi, da qui in poi iniziano i dati veri (il Frame)!"_.

## 3. Bit Stream e Flusso Continuo
A differenza dei livelli superiori che lavorano "a blocchi" (invio un pacchetto, aspetto, ne invio un altro), il Livello 1 vede la comunicazione come un **Bit Stream** (flusso di bit) continuo.

### Caratteristiche del flusso:
1. **Bit di Riempimento (Padding/Idle bits):** Quando non ci sono dati da trasmettere, il Livello 1 non sempre sta "zitto". In molti standard moderni (come la fibra o il Gigabit Ethernet), vengono inviati segnali di **Idle** per mantenere il laser o il circuito sincronizzato.
2. **Delimitazione:** Il Livello 1 non sa quanto è lungo un file. Sa solo quando il segnale elettrico inizia e quando finisce (grazie a variazioni di tensione o frequenza specifiche).

## 4. Riepilogo per lo studente universitario

|Proprietà|Definizione al Livello 1|
|---|---|
|**Nome del dato**|Bit (o flusso di bit / Bitstream).|
|**Contenitore**|Nessuno (è un flusso continuo di segnali).|
|**Incapsulamento**|Il Livello 1 riceve il _Frame_ dal Livello 2 e lo converte in segnali.|
|**Lunghezza**|Definita dal tempo di bit (1/frequenza).|
|**Controlli**|Nessun controllo d'errore sui dati (quelli si fanno al Livello 2 con il CRC).|


> **In sintesi:** Se chiedi a un dispositivo di Livello 1 (come un Hub) "Cosa stai trasportando?", lui non ti risponderà "Un'email" o "Un pacchetto IP", ma ti risponderà: **"Sto trasportando una sequenza di impulsi elettrici a 5 Volt con una frequenza di 100 MHz"**.

---
## Collegamenti
- Torna al corso: [[Dashboard CompTIA Network+]]