---
tipo: nota_lezione
corso: "Dashboard CompTIA Network+"
tags: [progetto, CompTIANetwork, certificazioni, Completed]
creato: 2026-02-19 15:44
---

# 📝 Lezione: STP (Spanning Tree Protocol) - Standard IEEE 802.1D
**Corso:** [[Dashboard CompTIA Network+]]

---
## Contenuto
## 1. Il problema: Il "Loop" di Livello 2
A differenza dei pacchetti IP (Livello 3) che hanno un campo chiamato **TTL (Time to Live)** che li distrugge dopo un po', i Frame di Livello 2 **non hanno una scadenza**. Se un frame entra in un anello fisico (loop), girerà all'infinito.
### Le conseguenze di un Loop:
1. **Broadcast Storm:** Un singolo messaggio di broadcast (come un ARP request) viene duplicato e gira in circolo, moltiplicandosi. La banda viene saturata al 100%.
2. **Instabilità della MAC Table:** Lo switch riceve lo stesso MAC sorgente da porte diverse continuamente, "impazzisce" e non sa più dove mandare i dati.
## 2. Come lavora l'STP: Le 3 Fasi dell'Elezione
Per risolvere il problema, l'STP trasforma una rete con anelli in una **struttura a albero** (senza cicli). Lo fa attraverso uno scambio di messaggi chiamati **BPDU (Bridge Protocol Data Units)**.
### Fase 1: Elezione del Root Bridge (Il "Capo")
Tutti gli switch iniziano dicendo: "Sono io il capo!". Poi confrontano il loro **Bridge ID (BID)**.
- Il BID è composto da una **Priorità** (default 32768) + il **MAC Address**.
- Lo switch con il **Bridge ID più basso** vince e diventa il **Root Bridge**.
- _Consiglio tecnico:_ In una rete seria, l'amministratore abbassa manualmente la priorità dello switch più potente per forzarlo a diventare il Root Bridge.
### Fase 2: Elezione delle Root Ports
Ogni switch che _non_ è il capo deve scegliere una sola porta per parlare con il Root Bridge.
- Sceglie la porta con il **Costo del Percorso più basso** (basato sulla velocità del cavo: un cavo da 1Gbps "costa" meno di uno da 100Mbps).
### Fase 3: Elezione delle Designated Ports
Su ogni segmento di cavo, viene scelta una porta "Designata" per inoltrare il traffico verso il Root Bridge. Tutte le altre porte che creano un anello vengono messe in stato di **Blocking**.
## 3. Gli Stati delle Porte
Una porta switch che usa STP non si accende istantaneamente (ecco perché a volte il LED è arancione prima di diventare verde). Passa attraverso vari stati:
1. **Blocking:** La porta è attiva ma non invia dati. Ascolta solo i messaggi BPDU.
2. **Listening:** Lo switch decide se la porta può diventare una Root o Designated port.
3. **Learning:** Lo switch inizia a popolare la sua MAC Table ma non inoltra ancora i dati dell'utente.
4. **Forwarding:** La porta è finalmente operativa e invia dati.
5. **Disabled:** La porta è spenta amministrativamente.
## 4. Evoluzioni: Dal "Lento" al "Veloce"
L'STP originale (802.1D) è molto lento: può impiegare fino a **30-50 secondi** per riprendersi da un guasto. Troppo per il mondo moderno. Per questo oggi usiamo:
- **RSTP (Rapid STP - 802.1w):** Molto più veloce, converge in meno di **2 secondi**. È lo standard attuale.
- **MSTP (Multiple STP):** Permette di avere "alberi" diversi per VLAN diverse. Ad esempio, il cavo A è bloccato per la VLAN 10 ma attivo per la VLAN 20, ottimizzando l'uso dei cavi.

## 5. Curiosità: Il "PortFast"
Se colleghi un PC a uno switch con STP, il PC potrebbe non ricevere un indirizzo IP perché il server DHCP scade prima che la porta passi da "Blocking" a "Forwarding". Gli amministratori usano il comando **PortFast** sulle porte collegate ai PC (non ad altri switch!) per farle saltare direttamente allo stato di **Forwarding** istantaneo.

---
## Collegamenti
- Torna al corso: [[Dashboard CompTIA Network+]]