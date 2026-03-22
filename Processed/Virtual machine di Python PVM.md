---
tipo: nota_lezione
corso: "Dashboard Python"
tags: [progetto, linguaggiProg, python, uni, programmazione, Completed]
creato: 2026-03-21 14:58
---

# 📝 Lezione: Virtual machine di Python PVM
**Corso:** [[Dashboard Python]]

---
## Contenuto
## 1. Il Flusso di Esecuzione: Da Sorgente a Bytecode
Quando esegui un file `.py`, CPython (l'implementazione standard) compie i seguenti passi:
1. **Parsing:** Il codice viene trasformato in un _Abstract Syntax Tree_ (AST).
2. **Compilazione in Bytecode:** L'AST viene convertito in **Bytecode**, una rappresentazione di basso livello, indipendente dalla piattaforma, ma non ancora codice macchina.
    - _Nota:_ Questi sono i file `.pyc` che trovi nella cartella `__pycache__`.
3. **PVM (The Interpreter Loop):** La Virtual Machine carica il bytecode e lo esegue.

## 2. Cos'è tecnicamente la PVM?
La PVM non è un software separato o un sistema operativo (come VirtualBox), ma è semplicemente **un enorme ciclo `while`** (spesso chiamato _eval loop_) scritto in C.
Il suo compito è:
- Leggere l'istruzione di bytecode successiva.
- Cercare l'implementazione in C corrispondente a quell'istruzione.
- Eseguire l'operazione sui dati.

## Esempio di Bytecode
Se hai una funzione `add(a, b): return a + b`, puoi vedere cosa "vede" la PVM usando il modulo `dis`:

```
import dis
dis.dis(add)
```
L'output mostrerà istruzioni come `LOAD_FAST`, `BINARY_ADD` e `RETURN_VALUE`. La PVM è l'entità che sa cosa fare quando incontra `BINARY_ADD`.

## 3. Architettura Basata su Stack (Stack-based VM)
A differenza delle CPU moderne che usano i **registri** per manipolare i dati, la PVM è una **Stack Machine**.
- Per sommare due numeri, la PVM:
    1. Esegue `PUSH` del primo numero sullo stack.
    2. Esegue `PUSH` del secondo numero sullo stack.
    3. L'istruzione `BINARY_ADD` preleva (_POP_) i due numeri, li somma e mette il risultato (_PUSH_) di nuovo in cima allo stack.
Questo design rende la PVM molto più semplice da implementare su diverse architetture hardware (astrazione), ma è uno dei motivi per cui Python è più lento dei linguaggi compilati che ottimizzano l'uso dei registri della CPU.

## 4. PVM e il Sistema Operativo: L'Astrazione
La PVM funge da **strato di isolamento**.
- Il bytecode è identico su Windows, Linux o macOS.
- È la PVM specifica per quel sistema operativo che traduce il bytecode in chiamate di sistema corrette.

Questo è il motivo per cui Python è "portabile": scrivi il codice una volta, e finché esiste una PVM per la macchina di destinazione, il codice girerà esattamente allo stesso modo.

## 5. Il Rapporto con il Garbage Collector
La PVM integra strettamente la gestione della memoria di cui parlavamo prima. Mentre esegue il bytecode, la PVM monitora il **Reference Counting**. Non appena il bytecode porta una variabile fuori dallo scope (ad esempio terminando una funzione), la PVM decrementa i contatori di riferimento e, se necessario, invoca immediatamente il deallocatore in C.

---
## Collegamenti
- Torna al corso: [[Dashboard Python]]