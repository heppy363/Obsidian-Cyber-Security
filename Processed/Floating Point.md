---
tipo: nota_lezione
corso: "Programmazione"
tags: [uni, programmazione, appunti, Completed]
creato: 2026-03-03 21:19
---

# 📝 Lezione: Floating Point
**Corso:** [[Programmazione]]

---
## Contenuto
Per rappresentare numeri molto grandi o molto piccoli (es. 0,000034 o 6,022×1023), usiamo lo standard **IEEE 754**. Il numero non è memorizzato "così com'è", ma in **notazione scientifica binaria**: ±M×2E.
In un sistema a **32 bit** (Single Precision), lo spazio è così diviso:
1. **Segno (1 bit):** 0 per positivo, 1 per negativo.
2. **Esponente (8 bit):** Determina dove si sposta la virgola. Viene memorizzato con un "eccesso" (bias) di 127 per gestire anche esponenti negativi.
3. **Mantissa o Frazione (23 bit):** Contiene le cifre significative del numero.
### Il concetto di approssimazione
A differenza degli interi, il floating point può soffrire di **errori di arrotondamento**. Poiché abbiamo solo 23 bit per la mantissa, alcuni numeri decimali (come 0,1) non possono essere rappresentati in modo esatto in binario e diventano sequenze infinite periodiche.
> **Curiosità tecnica:** È per questo che nei software finanziari non si usano mai i `float`, ma si preferisce lavorare con gli interi (es. calcolando tutto in centesimi) per evitare che spariscano centesimi a causa degli arrotondamenti binari.

---
## Collegamenti
- Torna al corso: [[Programmazione]]