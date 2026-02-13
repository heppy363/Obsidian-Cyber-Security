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
Nel 2026, il panorama dei connettori si è consolidato attorno ad alcuni standard dominanti per l'uso quotidiano (ufficio/casa) e altri estremamente avanzati per i Data Center e l'Intelligenza Artificiale, dove si toccano velocità di **800 Gbps** e **1.6 Tbps**.

Tabella comparativa aggiornata dei connettori principali:

|**Connettore**|**Mezzo**|**Categoria/Standard**|**Velocità Tipica**|**Perché usarlo (Punti di forza)**|
|---|---|---|---|---|
|**RJ45**|Rame (TP)|Cat 5e / 6 / 6A / 8.1|1 - 10 Gbps|**Ubiquità.** È lo standard universale per PC, console e uffici. Economico e robusto.|
|**LC (Lucent)**|Fibra|Single/Multi-mode|1 - 100 Gbps|**Dimensioni ridotte.** Permette un'altissima densità di porte negli switch moderni. È il "re" della fibra oggi.|
|**SC (Square)**|Fibra|Single/Multi-mode|1 - 10 Gbps|**Robustezza.** Meccanismo push-pull sicuro. Molto usato nelle terminazioni casalinghe (borchie FTTH).|
|**MPO / MTP**|Fibra|Multi-fibra (12/24)|40 - 400 Gbps|**Densità estrema.** Un singolo connettore porta fino a 24 fibre. Usato per i "backbone" dei Data Center.|
|**QSFP-DD**|Ibrido|DAC (Rame) / AOC|400 - 800 Gbps|**Interconnessione Server.** Moduli "Double Density" per collegare server e switch a distanze brevissime.|
|**OSFP**|Ibrido|Ottico / Rame|800 Gbps - 1.6 Tbps|**AI & Cloud.** Progettato per dissipare il calore estremo delle reti ultra-veloci di nuova generazione.|
#### 1. L'evoluzione del Rame (RJ45 e oltre)
Nonostante molti pensassero che il rame sarebbe morto, nel 2026 il connettore **RJ45** regge ancora grazie alla **Cat 8.1**, che permette 40 Gbps su distanze brevi (30m). Esistono connettori come il **TERA** o il **GG45** (usati per la Cat 7/7A), ma non sono mai diventati standard di massa perché il mercato ha preferito saltare direttamente alla fibra o restare sul collaudatissimo RJ45.
#### 2. Il dominio del connettore LC
Nelle reti in fibra, il connettore **LC** ha quasi totalmente sostituito i vecchi connettori **ST** (a baionetta) o **FC** (a vite). Il motivo è puramente logistico: essendo piccolo la metà di un SC, permette di raddoppiare il numero di porte su uno switch di pari dimensioni.
#### 3. DAC vs AOC (I "Cavi con il cervello")
Una particolarità del 2026 è l'uso massiccio di:
- **DAC (Direct Attach Copper):** Cavi di rame con connettori (come SFP o QSFP) già saldati. Non c'è conversione in luce. Sono usati perché hanno **latenza quasi zero** e costano pochissimo (per distanze < 5-7 metri).
- **AOC (Active Optical Cable):** Esteticamente uguali ai DAC, ma all'interno dei connettori c'è un chip che converte il segnale in luce e lo spara in una fibra. Usati per distanze fino a 100 metri.


## Link 
1) 