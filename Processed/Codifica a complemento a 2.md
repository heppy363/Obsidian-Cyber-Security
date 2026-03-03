---
tipo: nota_lezione
corso: "Programmazione"
tags: [uni, programmazione, appunti, Completed]
creato: 2026-03-03 21:18
---

# 📝 Lezione: Codifica a complemento a 2
**Corso:** [[Programmazione]]

---
## Contenuto
Rappresentare i numeri negativi non è banale: non possiamo usare il simbolo "−". La tecnica del **Complemento a 2** è lo standard perché permette alla CPU di eseguire sottrazioni usando lo stesso circuito della somma.
### Come si calcola (Esempio su 8 bit per il numero -5)
1. **Scrivi il numero positivo in binario:** 5→00000101
2. **Inverti i bit (Complemento a 1):** Trasforma gli 0 in 1 e gli 1 in 0.
    - 00000101→11111010
3. **Somma 1 al risultato:**
    - 11111010+1=11111011
- **Risultato:** 11111011 rappresenta **-5**.
**Perché è geniale?** Il bit più a sinistra (**MSB**) funge da indicatore di segno:
- **0** = Positivo
- **1** = Negativo Inoltre, se sommiamo 5 (00000101) e −5 (11111011), otteniamo 0 (ignorando l'ultimo riporto), proprio come in aritmetica classica.

---
## Collegamenti
- Torna al corso: [[Programmazione]]