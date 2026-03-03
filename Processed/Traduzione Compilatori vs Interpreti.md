---
tipo: nota_lezione
corso: "Programmazione"
tags: [uni, programmazione, appunti, Completed]
creato: 2026-03-03 21:44
---

# 📝 Lezione: Traduzione Compilatori vs Interpreti
**Corso:** [[Programmazione]]

---
## Contenuto
Per colmare il divario tra "Alto Livello" e "Linguaggio Macchina", servono due approcci differenti:
### Il Compilatore (Esempio: C, C++, Rust)
Immagina un traduttore che prende un intero libro e ne scrive una versione completa in un'altra lingua.
- **Processo:** Traduce tutto il codice sorgente in un file **eseguibile** (.exe o binario).
- **Vantaggi:** Molto veloce in esecuzione; il codice sorgente rimane segreto.
- **Svantaggi:** Se modifichi una riga, devi ricompilare tutto.
### L'Interprete (Esempio: Python, JavaScript, PHP)
Immagina un interprete simultaneo che traduce parola per parola mentre l'oratore parla.
- **Processo:** Legge una riga di codice, la traduce in linguaggio macchina e la fa eseguire immediatamente alla CPU, poi passa alla successiva.
- **Vantaggi:** Facilità di test (debug) e flessibilità.
- **Svantaggi:** Più lento del compilato, perché la traduzione avviene _durante_ l'esecuzione.

---
### Nota accademica sugli Errori Logici
Come hai giustamente sottolineato, la CPU è un "esecutore cieco". Se scrivi un programma che divide un numero per zero o entra in un loop infinito, la CPU non dirà "questo non ha senso". Lei continuerà a eseguire i bit finché il Sistema Operativo non interviene per abbattere il processo o finché non si verifica un crash hardware. Questo distingue il **Syntax Error** (scrivere male una keyword) dal **Logic Error** (scrivere un algoritmo sbagliato).




---
## Collegamenti
- Torna al corso: [[Programmazione]]