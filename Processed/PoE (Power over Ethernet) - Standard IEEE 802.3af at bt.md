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
Questa tecnologia permette di inviare energia elettrica insieme ai dati sullo stesso cavo Ethernet (Cat5e o superiore).
- **Come funziona:** Un cavo Ethernet ha 4 coppie di fili di rame. Inizialmente, per i 10/100 Mbps, se ne usavano solo due per i dati e le altre due potevano portare corrente (**Alternative B**). Oggi, con il Gigabit, si usa una tecnica chiamata "Phantom Power" per inviare corrente sulle stesse coppie che portano i dati (**Alternative A**).
- **Negoziazione:** Lo switch non "spara" corrente a caso (rischierebbe di bruciare un PC vecchio). Prima invia un segnale a bassissima tensione per capire se il dispositivo collegato è un **PD** (Powered Device, come un telefono IP). Se riceve risposta, eroga la potenza necessaria.
- **Classi di potenza:**
    - **PoE (802.3af):** Fino a **15.4W** (telefoni, sensori).
    - **PoE+ (802.3at):** Fino a **30W** (telecamere PTZ, access point Wi-Fi potenti).
    - **PoE++ (802.3bt):** Fino a **60W-90W** (monitor, illuminazione LED, laptop).

## Link 
1) 