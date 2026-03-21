---
tipo: nota_lezione
corso: "Dashboard Python"
tags: [progetto, linguaggiProg, python, uni, programmazione, Completed]
creato: 2026-03-21 14:39
---

# 📝 Lezione: Introduzione a Python
**Corso:** [[Dashboard Python]]

---
## Contenuto
## Filosofia e Caratteristiche Core
Python è un linguaggio **interpretato**, **interattivo** e **orientato agli oggetti**. A differenza di linguaggi compilati come il C++, Python utilizza una gestione della memoria automatica (**Garbage Collection**) e una **tipizzazione dinamica ma forte**.
- **Leggibilità:** Il codice è strutturato tramite l'indentazione (regola del _whitespace_), eliminando la necessità di parentesi graffe per definire i blocchi di codice.
- **Multiparadigma:** Supporta la programmazione procedurale, orientata agli oggetti (OOP) e funzionale.
- **Batteries Included:** La libreria standard offre moduli per tutto, dalla manipolazione di file alla gestione di protocolli di rete.
    

---

## 2. Sintassi e Strutture Dati Fondamentali
Dal punto di vista della computer science, è fondamentale comprendere come Python gestisce le collezioni di dati.
## Variabili e Tipi
Non è necessario dichiarare il tipo di una variabile; l'interprete lo deduce a runtime:


```
x = 5          # Integer
y = 3.14       # Float
name = "Alma"  # String
```
## Le Quattro Collezioni Native

|Struttura|Caratteristica|Sintassi|
|---|---|---|
|**Lista**|Ordinata, mutabile, permette duplicati.|`[1, 2, 2, 3]`|
|**Tupla**|Ordinata, **immutabile**, permette duplicati.|`(1, 2, 3)`|
|**Set**|Non ordinata, mutabile, **no duplicati**.|`{1, 2, 3}`|
|**Dizionario**|Coppie Chiave-Valore, mutabile.|`{"id": 1}`|

## 3. Controllo del Flusso
La logica di esecuzione segue i costrutti standard, ma con una sintassi molto asciutta.
- **Condizionali:** `if`, `elif`, `else`.
- **Cicli:** * `for` (utilizzato principalmente come iteratore su sequenze).
    - `while` (basato su una condizione booleana).
## 4. Funzioni e Modularità
In ambito universitario, l'astrazione è fondamentale. Le funzioni in Python sono **oggetti di prima classe**, il che significa che possono essere passate come argomenti ad altre funzioni.

```
def calcola_area(raggio):
    """Calcola l'area di un cerchio."""
    import math
    return math.pi * (raggio ** 2)
```

## 5. Perché Python in Accademia?
Python è diventato lo standard _de facto_ in diversi domini scientifici grazie a librerie specializzate:
1. **Data Science & AI:** NumPy per il calcolo matriciale, Pandas per l'analisi dati, e PyTorch/TensorFlow per il Deep Learning.
2. **Ricerca Scientifica:** SciPy per l'integrazione numerica e le equazioni differenziali.
3. **Sviluppo Web:** Framework robusti come Django e Flask.

---
## Collegamenti
- Torna al corso: [[Dashboard Python]]