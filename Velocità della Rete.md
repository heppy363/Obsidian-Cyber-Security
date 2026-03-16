---
tipo: nota_lezione
corso: "Dashboard Networking Basics"
tags: [progetto, certificazioni, networkingBasics, Completed]
creato: 2026-03-16 15:07
---

# 📝 Lezione: Velocità della Rete
**Corso:** [[Dashboard Networking Basics]]

---
## Contenuto
## 1. Bandwidth (Larghezza di Banda)
- **Definizione:** È la capacità massima teorica di un mezzo (cavo o wireless) di trasportare dati.
- **Analogia:** Immagina un'autostrada. La _Bandwidth_ è il numero di corsie disponibili. Più corsie ci sono, più auto (bit) possono transitare contemporaneamente.
- **Misurazione:** Si misura in bit al secondo (**bps**), **Kbps** (mille), **Mbps** (milioni) o **Gbps** (miliardi).

## 2. Throughput (Produttività Effettiva)
- **Definizione:** È la misura reale dei bit trasferiti in un dato momento. Quasi mai corrisponde alla Bandwidth.
- **Analogia:** Se l'autostrada ha 4 corsie (Bandwidth) ma c'è un incidente o lavori in corso, il numero di auto che passano davvero in un minuto è il _Throughput_.
- **Fattori che influenzano il Throughput:**
    - **Quantità di traffico:** Troppi utenti connessi contemporaneamente.
    - **Latenza (Latency):** Il tempo che un pacchetto impiega per andare da un punto A a un punto B (ritardi dovuti ai router intermedi).
    - **Tipo di dati:** Alcuni file richiedono più controllo di altri.

## 3. Concetti Chiave Associati
- **Latenza (Latency):** Si riferisce ai ritardi nel viaggio dei dati. Nel gaming online o nelle chiamate VoIP, una latenza alta causa "lag".
- **Il collo di bottiglia (Bottleneck):** In una rete con più segmenti, la velocità totale sarà sempre dettata dal **segmento più lento**. Se hai una fibra da 1 Gbps ma il tuo cavo Ethernet è vecchio e regge solo 100 Mbps, il tuo Throughput sarà bloccato a 100 Mbps.
- **Goodput:** (Concetto avanzato spesso menzionato) È la misura dei soli dati _utili_ trasferiti, escludendo i bit di controllo e gli errori.

---

## Perché è importante per il tuo obiettivo (Sistemista)
Quando lavorerai al CSE o in un ufficio tecnico, gli utenti si lamenteranno che "Internet è lento". Il tuo compito sarà capire se:
1. Manca **Bandwidth** (bisogna pagare un contratto migliore al provider).
2. C'è un problema di **Throughput** (un router è sovraccarico o c'è un cavo danneggiato che crea latenza).

---
## Collegamenti
- Torna al corso: [[Dashboard Networking Basics]]