---
tipo: nota_lezione
corso: "Programmazione"
tags: [uni, programmazione, appunti, Completed]
creato: 2026-03-03 21:29
---

# 📝 Lezione: Rappresentazione dati testuali 
**Corso:** [[Programmazione]]

---
## Contenuto
Come abbiamo visto, il computer non conosce le lettere. La soluzione è una **mappa di corrispondenza** (look-up table).
### 1.1 Evoluzione delle Codifiche
- **ASCII (7 bit):** Creato negli anni '60. Rappresenta 128 caratteri. È perfetto per l'inglese, ma mancano le lettere accentate (è, ò) e simboli di altre lingue.
- **ASCII Esteso (8 bit):** Arriva a 256 caratteri. Ogni produttore (Microsoft, Apple) aveva la sua versione, il che creava problemi di compatibilità (i famosi simboli strani nei testi).
- **UNICODE (Standard attuale):** È una tabella universale che assegna un numero univoco a ogni carattere esistente.
    - **UTF-8:** È il formato più usato sul web. Usa un numero variabile di byte (da 1 a 4). Se scrivi in inglese usa 1 byte, se usi un'emoji 🍎 o un carattere cinese ne usa di più.
- [[Approfondimento sulle codifiche testuali]]
---
## Collegamenti
- Torna al corso: [[Programmazione]]