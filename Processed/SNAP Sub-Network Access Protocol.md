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
## 1. Il Problema: Il limite dell'LLC Standard
Come abbiamo visto, l'LLC standard (IEEE 802.2) usa i campi **DSAP** e **SSAP** per identificare i protocolli di livello superiore. Questi campi sono lunghi solo **8 bit** (1 byte).
- Di questi 8 bit, alcuni sono riservati, lasciando solo **64 combinazioni** possibili per identificare i protocolli.
- Negli anni '80 i protocolli stavano esplodendo (IP, AppleTalk, IPX, DECnet, ecc.) e 64 posti erano decisamente troppo pochi.
Inoltre, il mondo Ethernet "commerciale" (quello di Xerox/Intel) usava un campo chiamato **EtherType** che era di 16 bit, mentre il mondo dello standard IEEE (802.3) voleva usare l'LLC. Lo SNAP è nato per mettere d'accordo tutti e permettere l'espandibilità infinita.
---
## 2. Cos'è lo SNAP?
Lo SNAP non è un livello separato, ma un'**estensione dell'intestazione LLC**. Viene attivato quando i campi DSAP e SSAP sono impostati sul valore esadecimale **`0xAA`**. Quando un computer riceve un frame con `0xAA`, "capisce" che non deve guardare l'LLC standard, ma deve leggere i 5 byte successivi (l'intestazione SNAP).

---
## 3. Struttura dell'Header SNAP (5 Byte)
L'header SNAP si divide in due parti:
1. **OUI (Organizationally Unique Identifier) - 3 Byte:** Indica l'organizzazione che gestisce il protocollo. Se il valore è `00:00:00`, significa che quello che segue è un protocollo standard Ethernet (EtherType).
2. **Protocol ID (Type) - 2 Byte:** Qui viene inserito il codice del protocollo (es. `0x0800` per IPv4). Avendo 16 bit a disposizione, abbiamo **65.536** combinazioni possibili invece delle misere 64 dell'LLC originale.
---
## 4. Perché è importante ancora oggi?
Lo SNAP è il "ponte" che permette di trasportare protocolli moderni su tecnologie che nativamente userebbero solo lo standard IEEE 802.2.
- **Wi-Fi (802.11):** È l'esempio più comune. Il Wi-Fi usa internamente l'incapsulamento LLC/SNAP per trasportare i pacchetti IP. Quando ti colleghi al router di casa, i tuoi dati stanno viaggiando dentro pacchetti SNAP.
- **Compatibilità:** Permette a dispositivi di produttori diversi (Apple, Cisco, Microsoft) di definire i propri protocolli proprietari (usando il proprio codice OUI) senza "rubare" spazio ai protocolli standard mondiali.

---

## Sintesi Visiva: L'incapsulamento finale
Ecco come appare un dato che viaggia, ad esempio, su Wi-Fi:
`[MAC Header] -> [LLC (AA-AA-03)] -> [SNAP (OUI + Type)] -> [Dati IP] -> [FCS]`
- **AA-AA:** Indica che segue uno SNAP.
- **03:** Indica un frame "Unnumbered Information" (Tipo 1, senza connessione).
- **SNAP:** Specifica finalmente che dentro c'è un pacchetto IP


## Link 
1) 