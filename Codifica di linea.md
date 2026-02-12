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
Ottima scelta. Se il Livello Fisico è il "corpo" della comunicazione, la **codifica di linea (Line Coding)** è il suo "linguaggio". A livello universitario, non basta dire che "0 è 0V e 1 è 5V"; bisogna capire perché alcune codifiche sono migliori di altre in base a efficienza, sincronizzazione e spettro di frequenza.

La codifica di linea è il processo di conversione dei bit digitali in un segnale che può viaggiare sul mezzo fisico.

---

## 1. Problemi da risolvere (I "Must" del Line Coding)
Una buona codifica di linea deve affrontare tre sfide:
1. **Auto-sincronizzazione:** Il segnale deve permettere al ricevitore di capire il tempo di bit (evitare il _Clock Drift_).
2. **Assenza di Componente Continua (DC Baseline):** Un segnale con troppi "1" o "0" seguiti crea una tensione media non nulla. Molti trasformatori e componenti di rete non filtrano bene la corrente continua.
3. **Efficienza Spettrale:** Occupare meno banda possibile per trasmettere più dati.
## 2. Le Principali Tecniche di Codifica
 **A. NRZ (Non-Return-to-Zero)**
È la forma più semplice.
- **NRZ-L (Level):** Lo "0" è un livello di tensione, l' "1" è un altro.
- **Problema:** Se invio una lunga stringa di zeri, il segnale rimane piatto. Il ricevitore perde il "ritmo" (sincronizzazione).
- **Uso:** Solo per comunicazioni brevissime e lente.
 **B. Manchester (Self-Clocking)**
Usata nella Ethernet classica (10 Mbps).
- **Logica:** Non conta il livello di tensione, ma la **transizione** a metà del tempo di bit.
    - _Esempio:_ Da basso ad alto = "1"; da alto a basso = "0".
- **Vantaggio:** C'è sempre una transizione, quindi il ricevitore può sincronizzarsi costantemente. Componente DC nulla.
- **Svantaggio:** Raddoppia la banda necessaria (servono due variazioni di stato per rappresentare un bit).
**C. MLT-3 (Multi-Level Transmit 3)**
Usata nella **Fast Ethernet (100 Mbps)** su rame.
- **Logica:** Usa tre livelli di tensione (+V, 0, -V). Lo stato cambia solo quando c'è un bit "1".
- **Vantaggio:** Riduce drasticamente le emissioni elettromagnetiche e la frequenza del segnale, permettendo velocità maggiori sul rame rispetto alla Manchester.
 **D. Codifiche a Blocchi (mB/nB)**
Nelle reti moderne (Gigabit Ethernet e oltre), non si codifica un bit alla volta, ma un **blocco di bit**.
- **8b/10b:** Prendi 8 bit di dati e li trasformi in 10 bit da trasmettere.
- **Perché?** I 2 bit extra servono per garantire che nel flusso finale non ci siano mai troppi zeri o uni consecutivi, forzando la sincronizzazione e mantenendo il bilanciamento DC.
- **Uso:** Gigabit Ethernet, Fibre Channel, SATA, USB 3.0.

---

## 3. Riepilogo Tecnico per l'esame

|Codifica|Caratteristica Chiave|Sincronizzazione|Efficienza|
|---|---|---|---|
|**NRZ**|Semplice voltaggio|Pessima (su lunghe sequenze)|Alta|
|**Manchester**|Transizione a metà bit|Eccellente (Auto-sincrona)|Bassa (50%)|
|**MLT-3**|Tre livelli (+/0/-)|Discreta|Molto Alta|
|**8b/10b**|Mappatura a blocchi|Ottima|Buona (80%)|

### Un concetto universitario avanzato: La Densità Spettrale

In sede d'esame, potrebbero chiederti perché non usiamo la Manchester per il Gigabit Ethernet. La risposta è che la Manchester ha una **frequenza di segnale troppo alta** (il segnale cambia troppo spesso). Sul rame, frequenze così alte subirebbero un'attenuazione enorme. Per questo si usano codifiche più complesse come **PAM-5** o **PAM-16** (Pulse Amplitude Modulation), che codificano più bit in un unico impulso variando l'ampiezza su più livelli.

## Link 
1) 