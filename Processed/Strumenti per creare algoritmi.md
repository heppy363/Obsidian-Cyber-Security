---
tipo: nota_lezione
corso: "Programmazione"
tags: [uni, programmazione, appunti, Completed]
creato: 2026-03-21 13:20
---

# 📝 Lezione: Strumenti per creare algoritmi
**Corso:** [[Programmazione]]

---
## Contenuto

## 1. Pseudocodice (Linguaggio di Progettazione)
Lo pseudocodice è un linguaggio non formale, molto vicino al linguaggio naturale umano e lontano da quello macchina.
- **Scopo**: Serve a pianificare la logica del codice prima della stesura definitiva.
- **Vantaggi**:
    - Permette di evitare errori di sintassi, poiché non esistono regole rigide come nei linguaggi di programmazione.
    - Consente di concentrarsi esclusivamente sulla risoluzione del problema.
    - È un ottimo strumento per comunicare l'idea del programma ad altri sviluppatori.
- **Esempio**:
    > SE la password è corretta ALLORA permetti l'accesso ALTRIMENTI nega l'accesso.

## 2. Diagrammi di Flusso (Flowchart)
A differenza dello pseudocodice, il diagramma di flusso rappresenta l'algoritmo in maniera **grafica** attraverso figure geometriche precise che indicano il tipo di operazione da svolgere.
#### I blocchi principali:
- **Ovali**: Rappresentano i punti di **Inizio** e **Fine** dell'algoritmo.
- **Parallelogrammi**: Utilizzati per le operazioni di **Input** (lettura dati) e **Output** (scrittura/visualizzazione risultati).
- **Rettangoli**: Indicano le fasi di **Elaborazione** o calcolo (es. `x = a + b`).
- **Rombi**: Rappresentano le **Decisioni**. Da qui partono due strade (Vero/Falso) che rendono la sequenza dell'algoritmo dinamica.

#### Regole di Correttezza:
- Un diagramma è corretto se esiste un percorso continuo che porta dal blocco di inizio a quello di fine.
- Le condizioni nei blocchi di decisione devono essere **mutualmente esclusive** per evitare ambiguità (non si può andare in due direzioni contemporaneamente con lo stesso dato).

## 3. Strutture di Controllo Fondamentali
Sia nello pseudocodice che nei flowchart, l'algoritmo si basa su tre strutture che guidano l'esecutore:
- **Sequenza**: Le istruzioni vengono eseguite una dopo l'altra in ordine statico.
- **Selezione**: L'esecutore sceglie quale strada prendere in base a una condizione (sequenza dinamica).
- **Iterazione (Cicli)**: Una serie di passi viene ripetuta più volte.
    - **Ciclo While**: Controlla la condizione _prima_ di agire (può essere eseguito zero volte).
    - **Ciclo Do-While**: Esegue l'azione e _poi_ controlla (eseguito almeno una volta).

## 💡 Concetto Chiave: Sequenza Statica vs Dinamica
- **Sequenza Statica**: È l'insieme di tutte le istruzioni scritte nell'algoritmo; non cambia mai.
- **Sequenza Dinamica**: È il percorso effettivo compiuto dai dati durante l'esecuzione. Cambia ogni volta in base ai valori di input e alle decisioni prese nei rombi.

---
## Collegamenti
- Torna al corso: [[Programmazione]]