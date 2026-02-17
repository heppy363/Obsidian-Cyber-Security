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
### 1. Come funziona il Sistema di Routing
Il sistema si basa sulla collaborazione tra i router. Per sapere dove mandare i pacchetti, un router deve conoscere la topologia della rete. Può farlo in tre modi:
1. **Rotte Direttamente Connesse:** Il router conosce automaticamente le reti attaccate fisicamente alle sue interfacce.
2. **Routing Statico:** L'amministratore di rete inserisce manualmente le rotte ("Per arrivare alla rete X, passa da Y"). È sicuro ma non si adatta se un cavo si rompe.
3. **Routing Dinamico:** I router usano protocolli (come **OSPF, RIP, BGP**) per parlarsi e dirsi: "Ehi, la strada per la rete A è libera ed è la più veloce". Se un percorso cade, ne calcolano uno nuovo automaticamente.
### 2. Esempio Pratico di Funzionamento
Immagina questa situazione:
- **Tu (Host A):** IP `192.168.1.10`
- **Il tuo Router (R1):** IP `192.168.1.1`
- **Destinazione (Server Google):** IP `8.8.8.8`

**Il processo:**
1. **Analisi Locale:** Il tuo PC nota che `8.8.8.8` non è nella sua rete locale (`192.168.1.0`).
2. **Invio al Gateway:** Il PC invia il pacchetto al suo "Default Gateway" (R1).
3. **Decisione del Router:** R1 guarda l'IP di destinazione `8.8.8.8`. Cerca nella sua **Tabella di Routing**.
4. **Hop (Salto):** La tabella dice: "Per qualsiasi indirizzo esterno, manda al router del Provider (ISP)". R1 spedisce il pacchetto al prossimo router.
5. **Arrivo:** Il processo si ripete di router in router finché non si arriva a quello che ha il server `8.8.8.8` direttamente connesso.

### 3. Esempio di Tabella di Routing popolata
Ecco come appare tecnicamente una tabella di routing (simile a quella di un router Cisco o di un server Linux).
Supponiamo un router con tre interfacce: una verso la LAN interna, una verso una sede distaccata e una verso Internet.

|Destinazione Rete|Maschera (Prefix)|Next Hop (Gateway)|Interfaccia|Metrica|
|---|---|---|---|---|
|`192.168.1.0`|`/24`|`0.0.0.0` (Connessa)|`eth0`|0|
|`10.0.0.0`|`/8`|`192.168.1.254`|`eth1`|10|
|`172.16.5.0`|`/24`|`10.0.0.5`|`eth1`|20|
|**`0.0.0.0`**|**`/0`**|**`82.10.10.1`**|**`eth2 (WAN)`**|100|

#### Legenda della tabella:
- **192.168.1.0/24:** È la rete locale. Il Next Hop è `0.0.0.0` perché il router ci è "seduto" sopra fisicamente.
- **10.0.0.0/8:** Una rete remota. Per arrivarci, il router deve mandare i dati a un altro router specifico (`192.168.1.254`).
- **0.0.0.0/0 (Default Route):** È la rotta più importante. Significa "Tutto il resto". Se la destinazione non è nelle prime tre righe, il pacchetto viene mandato all'IP `82.10.10.1` (il router dell'operatore telefonico).
- **Metrica:** Indica il "costo" della strada. Se ci fossero due strade per la stessa rete, il router sceglierebbe quella con la metrica più bassa.
### 4. Concetti Universitari Avanzati
- **Sistemi Autonomi (AS):** Internet è divisa in grandi blocchi chiamati AS (es. la rete di TIM, la rete di Google). Il routing dentro un AS si chiama **IGP** (es. OSPF), quello tra AS diversi si chiama **EGP** (es. BGP).
- **Convergenza:** È il tempo che i router impiegano ad aggiornare le loro tabelle dopo che un guasto ha cambiato la topologia della rete. Più è veloce, meglio è.

## Link 
1) 