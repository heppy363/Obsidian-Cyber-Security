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
`Definisce quante informazioni possano passare contemporaneamente sulla stessa linea di comunicazione, cavi fibra ottica ecc` 
#### 1. FDM (Frequency Division Multiplexing)
La multiplazione a divisione di frequenza divide la larghezza di banda totale disponibile in una serie di **canali di frequenza** separati.
- **Concetto:** Ogni segnale viene modulato su una frequenza portante diversa. È come avere un'autostrada a più corsie dove ogni corsia è riservata a un tipo di veicolo.
- **Caratteristiche:**
    - I segnali vengono trasmessi **contemporaneamente**.
    - Necessita di **Bande di Guardia (Guard Bands)**: intervalli di frequenza vuoti tra un canale e l'altro per evitare interferenze (crosstalk).
- **Esempio:** La radio FM o la vecchia TV analogica. Anche l'ADSL usa FDM per separare il traffico voce (frequenze basse), upload e download.

#### 2. TDM (Time Division Multiplexing)
La multiplazione a divisione di tempo non divide lo spettro di frequenza, ma il **tempo di utilizzo** del mezzo.
- **Concetto:** L'intera larghezza di banda è dedicata a un solo utente, ma solo per un brevissimo intervallo di tempo (chiamato **Time Slot** o quanto di tempo).
- **Caratteristiche:**
    - I segnali sono trasmessi in modo sequenziale.
    - **TDM Sincrono:** Ogni dispositivo ha un turno fisso, anche se non ha dati da inviare (spreco di banda).
    - **TDM Statistico (Asincrono):** I turni vengono assegnati dinamicamente solo a chi ha effettivamente dati pronti (molto più efficiente).
- **Esempio:** La telefonia digitale (standard GSM) o i collegamenti T1/E1.

#### 3. WDM (Wavelength Division Multiplexing)
Questa è una variante della FDM, ma applicata specificamente alla **fibra ottica**
- **Concetto:** Invece di usare frequenze elettriche, si usano diverse **lunghezze d'onda** (λ) della luce (colori diversi, anche se invisibili all'occhio umano).   
- **Evoluzione (DWDM):** Il _Dense WDM_ permette di far viaggiare centinaia di canali su una singola fibra, raggiungendo capacità di Terabit al secondo.
- **Perché è speciale:** Permette di aumentare la capacità di una rete in fibra già esistente semplicemente cambiando gli apparati alle estremità, senza scavare per posare nuovi cavi.

#### Confronto Rapido per lo Studio

|Tecnica|Dominio|Mezzo Tipico|Caratteristica Chiave|
|---|---|---|---|
|**FDM**|Frequenza|Rame / Aria|Trasmissione simultanea su frequenze diverse.|
|**TDM**|Tempo|Rame / Digitale|Uso esclusivo del mezzo in slot temporali.|
|**WDM**|Luce (λ)|Fibra Ottica|Più "colori" laser nello stesso nucleo di vetro.|

### Un dettaglio da "esame"
Ricorda che la multiplazione avviene al **Livello 1**, ma le decisioni su _chi_ trasmette e _quando_ (specialmente nel TDM statistico) iniziano a toccare le responsabilità del **Sottolivello MAC (Medium Access Control)** del Livello 2. È qui che i due livelli "si stringono la mano".

## Link 
1) 