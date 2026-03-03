---
tipo: nota_lezione
corso: "Programmazione"
tags: [uni, programmazione, appunti, Completed]
creato: 2026-03-03 22:00
---

# 📝 Lezione: La Triade Formale Lessico, Sintassi e Semantica
**Corso:** [[Programmazione]]

---
## Contenuto
Ogni linguaggio di programmazione è un sistema formale definito da tre strati gerarchici:
- **Lessico (Analisi Lessicale):** È l'alfabeto del linguaggio. Definisce quali sequenze di caratteri sono valide.
    - **Keyword:** Parole riservate (es. `if`, `while`, `return`).
    - **Identificatori:** Nomi dati dal programmatore a variabili o funzioni.
    - **Letterali:** Valori costanti (es. `3.14`, `"Ciao"`).
    - **Operatori e Delimitatori:** Simboli come `+`, `*`, `{`, `;`.
- **Sintassi (Analisi Grammaticale):** Definisce le regole di combinazione dei "token" lessicali. Una frase può avere parole corrette ma essere costruita male (es. `if else while`). La sintassi viene verificata tramite grammatiche formali (spesso espresse in notazione **BNF - Backus-Naur Form**).
- **Semantica (Il Significato):** È lo strato più critico. Un programma può essere scritto correttamente (sintassi OK), ma fare qualcosa di diverso da ciò che volevamo.
    - **Errore Semantico:** Se scrivo una funzione per calcolare l'area ma uso la formula del perimetro, il compilatore non mi darà errore, ma il risultato sarà sbagliato.

---
## Collegamenti
- Torna al corso: [[Programmazione]]