---
tipo: nota_lezione
corso: "Programmazione"
tags: [uni, programmazione, appunti, Completed]
creato: 2026-03-03 21:30
---

# 📝 Lezione: Rappresentazioni di immagini
**Corso:** [[Programmazione]]

---
## Contenuto
Esistono due modi diametralmente opposti di codificare un'immagine.
### 2.1 Immagini Raster (Bitmap)
L'immagine è vista come una griglia (matrice). Ogni cella è un **Pixel**.
- **Risoluzione:** Il numero di pixel (es. 1920×1080).
- **Profondità di colore:** Quanti bit usiamo per ogni pixel?
    - **1 bit:** Solo bianco o nero.
    - **8 bit:** 256 livelli di grigio.
    - **24 bit (True Color):** 8 bit per il Rosso, 8 per il Verde, 8 per il Blu (RGB). Questo permette 16,7 milioni di colori.
### 2.2 Immagini Vettoriali
Invece di memorizzare i punti, memorizzano **formule matematiche**.
- Invece di "punto nero in x,y", memorizza "disegna un cerchio di raggio r con centro x,y".
- **Vantaggio:** Puoi ingrandirle all'infinito senza che sgranino (es. loghi, font).

---
## Collegamenti
- Torna al corso: [[Programmazione]]