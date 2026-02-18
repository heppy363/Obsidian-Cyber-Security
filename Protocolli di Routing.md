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
### 1. Classificazione per Ambito
#### IGP (Interior Gateway Protocols)
Si usano all'interno di un **AS (Autonomous System)**, come la rete di un'università o di un'azienda.
- **Protocolli Distance Vector:** Basati sulla distanza (quanti router devo saltare?).
- **Protocolli Link-State:** Basati sulla "salute" e la velocità dei collegamenti (conoscono l'intera mappa della rete).
#### EGP (Exterior Gateway Protocols)
Si usano per collegare tra loro diversi AS.
- Oggi ne esiste solo uno: il **BGP**.

### 2. I Protocolli Principali e le loro Caratteristiche
#### RIP (Routing Information Protocol) - _Distance Vector_
È il protocollo più vecchio e semplice.
- **Metrica:** Conta i salti (**Hop Count**). Se una rete è a 3 salti, la metrica è 3.
- **Limite:** Il numero massimo di salti è **15**. A 16 la rete è considerata irraggiungibile.
- **Funzionamento:** Invia la sua intera tabella di routing ai vicini ogni 30 secondi (molto inefficiente per reti grandi).
- **Uso:** Piccole reti, ormai quasi abbandonato.
- [[Protocollo RIP]]
#### OSPF (Open Shortest Path First) - _Link-State_
È lo standard "de facto" per le reti aziendali moderne.
- **Algoritmo:** Usa **Dijkstra** per calcolare il percorso più breve (Shortest Path).
- **Metrica:** Il **Costo**, basato sulla larghezza di banda (bandwidth). Una fibra ottica ha un costo molto più basso di un vecchio cavo in rame.
- **Caratteristiche:** Divide la rete in **Aree** (Area 0 è la principale) per ridurre il carico di lavoro dei router.
- **Vantaggio:** Convergenza velocissima (se un cavo si rompe, la rete se ne accorge in pochi secondi).

#### EIGRP (Enhanced Interior Gateway Routing Protocol) - _Ibrido_
Sviluppato da Cisco (ora standard aperto, ma usato quasi solo su macchine Cisco).
- **Metrica:** Molto complessa (usa larghezza di banda, ritardo, carico e affidabilità).
- **Vantaggio:** Combina la semplicità del Distance Vector con la velocità del Link-State. Mantiene una tabella dei percorsi di riserva pronta all'uso.
#### BGP (Border Gateway Protocol) - _Path Vector_
È il protocollo che fa funzionare **Internet**.
- **Funzionamento:** Non guarda la velocità dei cavi, ma i "percorsi tra Stati/Aziende" (Autonomous Systems).
- **Caratteristiche:** È basato su **Policy**. Un provider può decidere di non far passare i dati attraverso un altro per motivi economici o politici.
- **Metrica:** Basata su attributi del percorso (es. quanti AS devo attraversare?).

### 3. Tabella Comparativa per l'esame

|Protocollo|Tipo|Algoritmo|Metrica|Velocità Convergenza|
|---|---|---|---|---|
|**RIP**|IGP / Dist. Vector|Bellman-Ford|Numero di salti (Hop)|Lenta|
|**OSPF**|IGP / Link-State|Dijkstra|Costo (Bandwidth)|Veloce|
|**EIGRP**|IGP / Ibrido|DUAL|Banda + Ritardo|Molto Veloce|
|**BGP**|EGP / Path Vector|BGP Path Sel.|Attributi di percorso|Molto Lenta|

### Un concetto fondamentale: La Distanza Amministrativa (AD)
Se un router impara la stessa rotta da OSPF e da RIP, a chi crede? Usa la **Distanza Amministrativa**, che è un numero che indica l'affidabilità del protocollo. Più è basso, meglio è:
- Connessa direttamente: **0**
- Statica: **1**
- EIGRP: **90**
- OSPF: **110**
- RIP: **120**
Quindi, se il router riceve due rotte per la stessa rete, sceglierà quella di **EIGRP** (90) perché è considerata più affidabile di RIP (120).


## Link 
1) 