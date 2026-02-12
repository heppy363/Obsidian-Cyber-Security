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
`I mezzi si dividono in Guidati (cavi) e **Non Guidati** (onde radio). Concentriamoci sul duello classico: **Rame vs Fibra Ottica**.`

#### 1. Il Rame: Il veterano (Doppino Intrecciato - UTP/STP)
Il rame trasmette dati sotto forma di **variazioni di tensione elettrica**.
- **L'intreccio (Twisting):** Ti sei mai chiesto perché i fili dentro un cavo Ethernet sono intrecciati a coppie? Serve a cancellare l'interferenza elettromagnetica. Grazie alla simmetria, il rumore colpisce entrambi i fili in modo simile e viene eliminato in ricezione (differenza di potenziale).
- **Limitazioni Fisiche:**
    - **Attenuazione:** La resistenza elettrica del rame dissipa il segnale in calore. Oltre i **100 metri**, il segnale è troppo debole per essere letto correttamente senza un ripetitore.
    - **Interferenze (EMI):** Essendo un metallo, funge da antenna. Motori elettrici, ascensori o cavi della corrente vicini possono "sporcare" i dati.
    - **Effetto Pelle (Skin Effect):** Ad alte frequenze, la corrente tende a scorrere solo sulla superficie del conduttore, aumentando la resistenza e limitando la banda.

#### 2. La Fibra Ottica: Perché è "Magica"?
La fibra non usa elettroni, ma **fotoni** (luce) che viaggiano dentro un sottilissimo filamento di vetro (silice).
**Il segreto fisico: La Riflessione Totale Interna**
La fibra è composta da un **Core** (nucleo) e un **Cladding** (mantello) con indici di rifrazione diversi. La luce colpisce il confine tra i due con un angolo tale da rimanere "intrappolata" nel nucleo, rimbalzando senza uscire mai.
**Perché batte il rame su tutti i fronti?**
1. **Larghezza di Banda Immensa:** La frequenza della luce è nell'ordine dei Terahertz (THz). Più alta è la frequenza della portante, più dati puoi modulare.
2. **Attenuazione Bassissima:** Un segnale in fibra può viaggiare per decine di chilometri senza bisogno di amplificazione (mentre il rame si ferma a 100m).
3. **Immunità Elettromagnetica Totale:** Il vetro è un isolante. Puoi far passare una fibra accanto a un cavo ad alta tensione o in una tempesta solare e il segnale rimarrà puro. Niente interferenze, niente "crosstalk".
4. **Sicurezza:** È quasi impossibile intercettare i dati in fibra senza rompere il cavo (mentre il rame emette onde radio che possono essere captate dall'esterno).
![[composizioneFibraOttica.png]]

#### Domande tipiche
Esistono due macro-categorie che devi conoscere:
- **Multimodale (MMF):** Il nucleo è più largo. La luce rimbalza con diverse angolazioni (modi). Causa **dispersione modale** (i raggi arrivano in tempi leggermente diversi), limitando la distanza.
    - _Uso:_ Data center, distanze brevi (fino a 500m).
- **Monomodale (SMF):** Il nucleo è piccolissimo (8-10μm). La luce viaggia dritta senza rimbalzare. Quasi zero dispersione.
    - _Uso:_ Dorsali oceaniche, tratte nazionali (Km e Km).

|**Caratteristica**|**Doppino in Rame (Cat 6/7)**|**Fibra Ottica**|
|---|---|---|
|**Mezzo di propagazione**|Elettroni (Elettricità)|Fotoni (Luce)|
|**Distanza Max (senza bridge)**|~100 metri|Fino a 100+ Km|
|**Costo Apparati**|Molto basso|Alto (Laser/Ricevitori)|
|**Sensibilità al rumore**|Alta|Nulla|
|**Installazione**|Facile (si può piegare)|Delicata (non va piegata troppo)|

#### Curiosità per approfondire
Sapevi che nei cavi sottomarini che collegano l'Europa all'America, dentro il rivestimento di protezione, ci sono dei veri e propri amplificatori ottici (EDFA) alimentati ad alta tensione per rigenerare la luce ogni 50-80 km?


## Link 
1) 