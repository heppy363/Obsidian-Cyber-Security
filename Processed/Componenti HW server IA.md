---
aliases:
  - Completate
tags:
  - Completed
  - H-net
---
--- 
## Nozioni
`Tutti i componenti necessari per assembrale i server`
### Componenti HW 
 ## 1. Scheda Madre e CPU (Il "Cervello")
Con tre GPU, il problema principale non è la potenza della CPU, ma le **linee PCIe**. Ogni P40 ha bisogno di dialogare velocemente con il sistema.
na scheda madre **X99** (LGA2011-3) di fascia alta o workstation (come la serie **Asus X99-E WS** o le **Supermicro**).
- **CPU:** Ti serve un processore che supporti **40 linee PCIe**. Un **Intel Xeon E5-2680 v4** (o v3) è perfetto e oggi si trova a prezzi stracciati. Se prendi una CPU con sole 28 linee (come alcuni i7 economici dell'epoca), la terza scheda andrà lentissima o non funzionerà.
- **RAM:** Punta a **128GB DDR4 ECC**. Con 72GB di VRAM, è bene avere almeno 128GB di RAM di sistema per gestire il caricamento dei modelli e il passaggio dei dati.
2. Alimentazione (Il punto critico)
Ogni P40 consuma fino a **250W**. Tre schede significano 750W solo di GPU, a cui devi aggiungere circa 150-200W per il resto del sistema.
- **PSU:** Ti serve un alimentatore da **almeno 1200W - 1300W** (80 Plus Gold o Platinum).
- **I Cavi (Attenzione!):** Le Tesla P40 **NON** usano i classici cavi PCIe a 8 pin delle schede gaming. Usano il connettore **CPU/EPS a 8 pin**.
    > **Pericolo:** Se forzi un cavo PCIe da gaming dentro una P40, rischi di bruciare tutto perché la polarità è invertita. Devi acquistare degli **adattatori specifici "Dual PCIe 8-pin to Tesla 8-pin"** o usare un alimentatore che abbia abbastanza cavi CPU (molto raro).
    
2. Disposizione Fisica e Raffreddamento
Tre P40 occupano 6 slot totali (sono dual-slot).
- **Case:** Ti serve un case **Full Tower** enorme o, meglio ancora, un **telaio Open Frame** (tipo quelli da mining). In un case chiuso, anche con le ventole, tre P40 vicine si "soffocherebbero" a vicenda.
- **Ventole:** Poiché hai detto di aver già risolto la dissipazione, assicurati che ogni scheda riceva un flusso d'aria costante. Le P40 non hanno ventole proprie; senza un getto d'aria forzato, raggiungono i 90°C in pochi secondi.

### La Lista dei Componenti (Specifiche Esatte)

| **Componente**   | **Modello Esatto Consigliato**             | **Perché?**                                                                                               | **Prezzo Stimato (2026)** |
| ---------------- | ------------------------------------------ | --------------------------------------------------------------------------------------------------------- | ------------------------- |
| **GPU (x3)**     | **NVIDIA Tesla P40 (24GB)**                | 72GB VRAM totali. Pascal architecture.                                                                    | **~600€** (200€ l'una)    |
| **Scheda Madre** | **ASUS X99-E WS (Workstation)**            | Ha 7 slot PCIe e un chip PLX che permette **3 GPU a x16/x16/x16**. Fondamentale per non strozzare i dati. | **~180€** (Usata)         |
| **CPU**          | **Intel Xeon E5-2680 v4**                  | 14 Core / 28 Thread. Supporta 40 linee PCIe e RAM ECC.                                                    | **~50€** (Usata)          |
| **RAM**          | **128GB (4x32GB) DDR4 ECC 2400MHz**        | La RAM ECC corregge gli errori, vitale per calcoli IA che durano ore.                                     | **~180€** (Usata)         |
| **Alimentatore** | **Corsair HX1500i (1500W Platinum)**       | Ti serve potenza pulita e molti cavi PCIe separati.                                                       | **~280€**                 |
| **Cavi (x3)**    | **Adattatori Dual 8-pin PCIe a 8-pin CPU** | Le P40 usano il pinout CPU. **Non collegare cavi PCIe diretti!**                                          | **~30€**                  |
| **Dissipazione** | **Kit Ventole Delta 40mm High-Static**     | Pressione d'aria estrema per raffreddare i dissipatori passivi.                                           | **~40€**                  |
| **TOTALE**       |                                            |                                                                                                           | **~1.360€**               |
- [[Consumo energetico server IA]]
- 

## Link 
1) 