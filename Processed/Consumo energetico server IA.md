---
aliases:
  - Completate
tags:
  - Completed
  - H-net
  - IA
---
--- 
## Nozioni
`Consumo a pieno reggimi per 24 ore`
## Carico e Consumi (A pieno regime)
Far girare un modello come **Llama-3 70B** o **DeepSeek** su tre schede caricherà il sistema in questo modo:
### Consumo Energetico
- **GPU (x3):** Ogni P40 consuma circa **250W** sotto sforzo (inferenza pesante). Totale: **750W**.
- **CPU + Sistema:** Lo Xeon e la scheda madre X99 consumano circa **150W-180W** sotto carico.
- **Totale al muro:** Circa **950W - 1000W**.
    > **Nota sui costi:** Se tieni il server acceso 24/7 a pieno carico, con un costo medio di 0,25€/kWh, spenderesti circa **6€ al giorno**. In modalità idle (acceso ma senza calcoli), il consumo scende a circa 100W.
### Calore e Rumore
Preparati: le ventole necessarie per raffreddare le P40 sono **estremamente rumorose** (sembrano un piccolo jet). Non è una macchina da tenere in camera da letto, ma in un garage o in una stanza dedicata.

## Link 
1) 