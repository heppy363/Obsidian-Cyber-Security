---
tipo: nota_lezione
corso: "Programmazione"
tags: [uni, programmazione, appunti, Completed]
creato: 2026-03-21 14:23
---

# 📝 Lezione: Definizione di un algoritmo 
**Corso:** [[Programmazione]]

---
## Contenuto
Si passa dal cosa quindi [[requisiti del software]] al [[Il come]] quindi tramite gli  [[Approccio top-dow]] e [[Approccio bottom-up]] che sono regolamentati dalla [[Programmazione strutturata]] alla definizione reale di come un algoritmo deve essere generato 
## La Formalizzazione Grafica: Il Diagramma di Flusso
Il diagramma di flusso (flowchart) è lo strumento che trasforma la logica astratta in un percorso visivo univoco. Esso utilizza simboli standardizzati per descrivere le azioni e il loro ordine di esecuzione:
- **Ovale**: Rappresenta i punti di **Inizio** e **Fine** dell'algoritmo.
- **Parallelogramma**: Utilizzato per le operazioni di **Input** (lettura dati) e **Output** (scrittura/visualizzazione).
- **Rettangolo**: Indica le fasi di **Elaborazione** o calcolo (es. operazioni matematiche).
- **Rombo**: Rappresenta le **Decisioni** o test condizionali.
- **Frecce**: Collegano i blocchi indicando il flusso della sequenza.
## Completezza Logica e Correttezza
Un diagramma di flusso è considerato **corretto** e **formale** solo se rispetta determinati vincoli logici che hai giustamente evidenziato:
1. **Percorso Definito**: Deve sempre esistere un percorso che parta dal blocco di inizio e arrivi al blocco di fine.
2. **Mutua Esclusività**: Nel blocco di decisione (rombo), le condizioni di uscita devono escludersi a vicenda (es. se è vero, non può essere contemporaneamente falso).
3. **Completezza**: Le condizioni devono coprire tutte le possibilità per evitare ambiguità nell'algoritmo.
## La Dinamicità del Flusso
Il diagramma di flusso rende visibile la differenza tra la struttura del codice e la sua esecuzione reale:
- **Sequenza Statica**: È l'insieme complessivo di tutti i blocchi e le frecce disegnati; questa struttura non cambia mai, indipendentemente dai dati.
- **Sequenza Dinamica**: È il percorso specifico che i dati "attraversano" durante una singola esecuzione.
    - Senza blocchi di selezione (rombi), la sequenza dinamica coincide con quella statica: c'è una sola strada possibile.
    - In presenza di selezioni o cicli, ogni esecuzione può prendere percorsi diversi in base ai valori di input.

## Il Collegamento Finale
Quadro completo: 
1. **Analisi**: Capisci il problema (il **Cosa**) e ne verifichi la **fattibilità**.
2. **Strategia**: Usi il **Top-Down** per scomporre il problema in blocchi elementari o il **Bottom-Up** per unire moduli esistenti.
3. **Programmazione Strutturata**: Ti assicuri che ogni blocco o modulo abbia un solo ingresso e una sola uscita.
4. **Formalizzazione**: Disegni il **Diagramma di Flusso** per definire la sequenza statica e prevedere tutte le possibili sequenze dinamiche.

> **Nota importante**: Se durante il disegno del diagramma ti accorgi che una condizione non è chiara, devi tornare alla fase di **analisi dei requisiti** per evitare il backtracking pesante in fase di scrittura del codice.
---
## Collegamenti
- Torna al corso: [[Programmazione]]
- [[Che cosa e un algoritmo]]