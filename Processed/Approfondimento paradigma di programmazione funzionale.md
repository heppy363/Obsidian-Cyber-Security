---
tipo: nota_lezione
corso: "Programmazione"
tags: [uni, programmazione, appunti, Completed]
creato: 2026-03-03 22:06
---

# 📝 Lezione: Approfondimento paradigma di programmazione funzionale 
**Corso:** [[Programmazione]]

---
## Contenuto
Se l'approccio imperativo è una "lista della spesa" (fai questo, poi quello), quello funzionale è una "formula matematica".

## 1. Paradigma Imperativo vs. Funzionale: La gestione dello Stato
La differenza fondamentale risiede nel concetto di **Stato** e **Mutabilità**.
### A. Approccio Imperativo (C, Java, Python)
Si basa sull'architettura di von Neumann: abbiamo una memoria e una CPU che la modifica.
- **Assegnazione:** È l'operazione cardine. `x = x + 1` ha senso perché stiamo sovrascrivendo una cella di memoria.
- **Effetti Collaterali (Side Effects):** Una funzione può modificare variabili esterne o stampare a video. Questo rende il codice difficile da testare in sistemi complessi, perché il risultato dipende da "cosa è successo prima".
### B. Approccio Funzionale (Haskell, Lisp, Erlang)
Si basa sul **Lambda Calcolo** di Alonzo Church. Il programma è un'espressione matematica.
- **Immutabilità:** Le variabili non esistono, esistono le **costanti**. Una volta definito `x = 5`, `x` sarà sempre 5. Non puoi fare `x = x + 1`.
- **Funzioni Pure:** Una funzione, dato lo stesso input, restituirà _sempre_ lo stesso output, senza modificare nulla all'esterno.
- **Trasparenza Referenziale:** Puoi sostituire una chiamata a funzione con il suo valore risultante senza cambiare il comportamento del programma.

## 2. Caratteristiche Tecniche del Paradigma Funzionale
Per poter programmare senza "cambiare lo stato", il paradigma funzionale introduce strumenti avanzati:
### Funzioni di Ordine Superiore (First-Class Functions)
In questi linguaggi, le funzioni sono trattate come comuni variabili.
- Puoi passare una funzione come argomento a un'altra funzione.
- Una funzione può restituire un'altra funzione come risultato.
### Ricorsione vs Cicli
Poiché non puoi avere una variabile "contatore" che aumenta (come `i++` in un ciclo `for`), il paradigma funzionale usa la **ricorsione**. Per ripetere un'operazione, la funzione chiama se stessa con un input diverso.
> _Nota tecnica:_ Per evitare che la memoria si riempia (Stack Overflow), questi linguaggi usano la **Tail Call Optimization** (ottimizzazione della ricorsione in coda).
### Operatori Fondamentali: Map, Filter, Reduce
Invece di scrivere cicli complessi, si usano trasformatori di liste:
- **Map:** Applica una funzione a ogni elemento di una lista.
- **Filter:** Tiene solo gli elementi che soddisfano una condizione.
- **Reduce:** Combina tutti gli elementi in un unico valore (es. la somma).

---
## Collegamenti
- Torna al corso: [[Programmazione]]