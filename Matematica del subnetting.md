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
## 1. L'operazione di AND (Il cuore del routing)
Il router deve capire se un IP appartiene a una rete. Per farlo, confronta bit a bit l'IP e la Maschera.
- 1 AND 1=1
- 1 AND 0=0
- 0 AND 0=0
**Esempio:** Indirizzo IP: `192.168.1.10` Maschera: `255.255.255.0` (/24)
In binario (ultimo ottetto):
- IP: `... . 00001010` (10)
- Mask: `... . 11111111` (255)
- **Risultato (Rete):** `... . 00001000` → La rete è `192.168.1.0`
## 2. Le formule fondamentali
Per l'esame, devi tatuarti in mente queste due potenze di 2:
1. **Numero di sottoreti creabili:** 2n _(dove n è il numero di bit "presi in prestito" dalla parte host)_.
2. **Numero di Host utilizzabili per sottorete:** 2h−2 _(dove h è il numero di bit rimasti a zero nella maschera)_.

> **Perché −2?** Sottraiamo sempre l'indirizzo di **Rete** (tutti i bit host a 0) e l'indirizzo di **Broadcast** (tutti i bit host a 1).
## 3. Esercizio Pratico: Dividere una rete
Hai la rete `192.168.10.0 /24`. Ti viene chiesto di creare **4 sottoreti**.
### Step 1: Quanti bit servono?
Applichiamo 2n≥4. Con n=2 bit otteniamo esattamente 4 sottoreti (22=4).
### Step 2: Nuova Maschera
La maschera originale era `/24` (24 bit a uno). Aggiungiamo i 2 bit "presi in prestito": Nuova maschera = 24+2=/26. In decimale: i primi tre ottetti sono `255.255.255`, l'ultimo è `11000000` in binario, ovvero **192**.
### Step 3: Calcolo del "Salto" (Magic Number)
Sottrai l'ultimo ottetto significativo della maschera da 256: 256−192=64. Questo è il tuo incremento. Le reti inizieranno ogni 64 numeri.
### Step 4: Prospetto delle Sottoreti

|Sottorete|Indirizzo Rete|Range Host Utili|Broadcast|
|---|---|---|---|
|**#1**|`192.168.10.0`|`.1` - `.62`|`192.168.10.63`|
|**#2**|`192.168.10.64`|`.65` - `.126`|`192.168.10.127`|
|**#3**|`192.168.10.128`|`.129` - `.190`|`192.168.10.191`|
|**#4**|`192.168.10.192`|`.193` - `.254`|`192.168.10.255`|

## 4. La tabella di conversione rapida (Trucco per l'esame)
Impara a memoria i valori dell'ultimo ottetto per risparmiare tempo:
- `/25` = `10000000` = `.128`
- `/26` = `11000000` = `.192`
- `/27` = `11100000` = `.224`
- `/28` = `11110000` = `.240`
- `/29` = `11111000` = `.248`
- `/30` = `11111100` = `.252` (Usata per i collegamenti punto-punto tra router, solo 2 host utili).
## 5. VLSM (Variable Length Subnet Mask)
A un livello universitario avanzato, non tutte le sottoreti hanno la stessa dimensione. Il **VLSM** permette di ottimizzare:
- Se il Reparto A ha 50 persone, gli dai una `/26` (62 host).
- Se il Reparto B ha 10 persone, gli dai una `/28` (14 host). In questo modo non sprechi indirizzi.

## Link 
1) 