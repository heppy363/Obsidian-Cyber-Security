---
tipo: nota_lezione
corso: "Algoritmi"
tags: [AlgoritmiUNI, uni, appunti, Completed]
creato: 2026-03-24 18:49
---

# 📝 Lezione: Programmazione Dinamica (DP)
**Corso:** [[Algoritmi]]

---
## Contenuto

Si usa quando un problema può essere scomposto in **sottoproblemi sovrapposti** (che si ripetono). Invece di ricalcolarli, salviamo il risultato.
- **Approccio Bottom-Up (Tabulation):** Si parte dai casi più piccoli (i "mattoni") e si costruisce una tabella fino ad arrivare alla soluzione del problema principale. È spesso più efficiente perché evita la ricorsione.
- **Approccio Top-Down (Memoization):** Si parte dal problema grande e lo si spezza ricorsivamente.
    - **Memoization:** Come dicevi tu, è una sorta di **cache**. Se una funzione viene chiamata con parametri già visti, restituisce il valore salvato invece di ricalcolarlo.
    - _Nota:_ La memoization è una _tecnica_ usata dalla programmazione dinamica, non sono due cose separate.

---
## Collegamenti
- Torna al corso: [[Algoritmi]]