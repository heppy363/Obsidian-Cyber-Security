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
`Si tratta del primo livello dello stack (o ultimo dipende da come lo si tratta) il suo compito e quello di fare passare i bit tra una macchina e l'altra della rete o di diverse reti`

### Cos'è il Livello Fisico?
Il compito principale di questo livello e quello di definire le specifiche meccaniche, elettrice, funzionali e procedurali per attivare, mantenere e disattivare il collegamento fisico tra sistemi filali (si possono intendere come gli host), in sostanza _trasforma i bit in segnali elettrici e vice versa_. 
**Funzioni principali**
1) _Rappresentazione dei bit_: decide come codificare i biti quindi "0" e "1" (es: variazioni di tensioni o impulsi luminosi).
2) _Data Rate (trasmissioni di dati)_: definisce il numero di bit inviati al secondo (_BPS_).
3) _Sincronizzazione dei bit_: e fondamentale che mittente e ricevente siano sincronizzati e questo lo si fa considerando il _clock_ delle singole macchine interessate alla trasmissione, questo consente di capire quando iniziare e finire la trasmissione basandosi proprio sul clock delle macchine.
	- [[Sincronizzazione dei bit in una rete]]
4) _Topologia fisica_: definisce come sono collegati i dispositivi e da questo sene definisce la topologia, (es: stessa, a bus, ad anello, mesh) 
5) _Modalita di trasmissione_: si intende come i bit i muovono sulla rete (in che direzione) 
	- [[Modalitá di trasmissione di una rete]]

### Aspetti tecnici e specifiche 
A livello generico si devono distingue degli aspetti universalmente riconosciuti e percepiti 
**1. Caratteristiche "meccaniche"** 
Riguarda l'aspetto fisico dei connettori, il numero dei pin il materiale dei cavi:
- RJ45 = Ethernet
- SC/LC per fibra ottica 
- [[Principali tipi di connettori]]
**2. Caratteristiche Elettriche/Ottiche**
Definisce i livelli di tensione per i segnali elettrici o le lunghezze d'onda per i segnali ottici quindi si parla della [[Codifica di linea]]
- Non-Return-to-Zero (NRZ): Semplice ma soffre di problemi di sincronizzazione.
- Manchester: Usata nella vecchia Ethernet, garantisce la sincronizzazione tramite una transizione a metà di ogni bit.
- MLT-3: Usata nell'Ethernet moderna su rame per ridurre le emissioni elettromagnetiche.
**3. Mezzi Trasmissivi** 
Il livello fisico opera su diversi media:
- **Guidati:** Cavi in rame (TP - Twisted Pair, Coassiali) e Fibra Ottica.
- **Non Guidati:** Onde radio (Wi-Fi, Bluetooth), Microonde, Infrarossi.

### Esistono "Protocolli" al Livello 1?
È una domanda trabocchetto comune. Tecnicamente, a questo livello si parla più di [[Definizione di uno standard]] e **specifiche hardware** che di protocolli software nel senso stretto del termine (come TCP o HTTP). Tuttavia, gli standard definiscono il comportamento operativo:
- **Ethernet (IEEE 802.3):** Specifica i dettagli fisici come il 1000BASE-T.
- **Wi-Fi (IEEE 802.11):** Nelle sue varianti fisiche (PHY) per la modulazione del segnale radio.
- **DSL / ADSL:** Standard per la trasmissione dati su doppino telefonico.
- **USB / Bluetooth:** Standard fisici per comunicazioni a corto raggio.
- **OTN (Optical Transport Network):** Per le reti in fibra ottica ad altissima velocità.
- [[Apparecchi HW del livello 1]]
- [[Definizione della PDU livello 1]]

### Perché è fondamentale?
Senza il Livello Fisico, i livelli superiori (Data Link, Network, ecc.) non avrebbero un "corpo" su cui viaggiare. I problemi a questo livello sono spesso i più difficili da diagnosticare: **attenuazione** (perdita di potenza del segnale), **rumore** (interferenze esterne) e **distorsione**.
> **Nota per l'esame:** Ricorda che il Livello Fisico non vede "frame" o "pacchetti". Esso vede solo **bit** (0 e 1). Se un bit viene corrotto, il Livello Fisico non lo sa; sarà il Livello 2 (Data Link) a occuparsi dell'eventuale rilevamento dell'errore.


## Link 
1) 