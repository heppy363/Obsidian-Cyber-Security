---
tipo: nota_lezione
corso: "Dashboard Python"
tags: [progetto, linguaggiProg, python, uni, programmazione, Completed]
creato: 2026-03-21 14:46
---

# 📝 Lezione: Aspetti architetturali
**Corso:** [[Dashboard Python]]

---
## Contenuto

## 1. Tipizzazione: Dinamica ma Forte
Esiste spesso confusione su questo punto. Python è un linguaggio a **tipizzazione dinamica** e **fortemente tipizzato**.
- **Dinamica (Dynamic Typing):** Il tipo è associato all'oggetto (il valore), non alla variabile (il nome). Non dichiariamo `int x`, ma semplicemente `x = 10`. L'interprete scopre il tipo a runtime.
- **Forte (Strong Typing):** Python non permette operazioni tra tipi incompatibili senza un casting esplicito.
    - In **JavaScript** (debolmente tipizzato), `"2" + 2` restituirebbe `"22"`.
    - In **Python**, lo stesso comando solleverebbe un `TypeError`. Questo garantisce integrità ed evita bug silenziosi tipici dei linguaggi a tipizzazione debole.

## 2. Gestione della Memoria e Modello a Oggetti
In Python, **"Everything is an object"** (Tutto è un oggetto). Anche un intero o una funzione sono istanze di una classe.
## Referencing e Astrazione
A differenza del C, dove una variabile è una locazione di memoria, in Python una variabile è un **puntatore (riferimento)** a un oggetto memorizzato nell'**Heap**.
- Se scrivi `a = [1, 2, 3]` e poi `b = a`, non stai copiando la lista. Entrambe le variabili puntano allo stesso indirizzo di memoria.

## Garbage Collection (GC)
Python gestisce la memoria automaticamente tramite due meccanismi principali:
1. **Reference Counting:** Ogni oggetto tiene traccia di quanti nomi puntano a lui. Quando il contatore scende a **0**, la memoria viene deallocata immediatamente.
2. **Generational Garbage Collector:** Per risolvere il problema dei "riferimenti circolari" (A punta a B e B punta a A, ma nessuno dei due è usato dal programma), Python scansiona periodicamente la memoria dividendo gli oggetti in tre "generazioni" in base alla loro longevità.

## 3. L'interprete e il Global Interpreter Lock (GIL)
L'implementazione standard di Python (CPython) non esegue direttamente il codice sorgente, ma lo compila in **Bytecode** (file `.pyc`), che viene poi eseguito dalla **Python Virtual Machine (PVM)**.
## Il limite del GIL
Un aspetto cruciale per il calcolo ad alte prestazioni è il **GIL**. È un "lucchetto" che permette a un solo thread alla volta di controllare l'interprete Python.
- **Conseguenza:** Python non può sfruttare pienamente i processori multi-core per task puramente legati alla CPU tramite il multithreading standard.
- **Soluzione:** Per il parallelismo reale, si utilizza il modulo `multiprocessing` (processi separati con memoria distinta) o librerie in C (come NumPy) che rilasciano il GIL durante i calcoli intensivi.

## 4. Mutabilità vs Immutabilità
Dal punto di vista della gestione dello stato, la distinzione tra tipi mutabili e immutabili è vitale per evitare effetti collaterali indesiderati:

|Categoria|Tipi|Comportamento|
|---|---|---|
|**Immutabili**|`int`, `float`, `str`, `tuple`|Ogni modifica crea un **nuovo oggetto** in memoria.|
|**Mutabili**|`list`, `dict`, `set`|L'oggetto viene modificato **in situ** (stesso indirizzo di memoria).|

---
## Collegamenti
- Torna al corso: [[Dashboard Python]]