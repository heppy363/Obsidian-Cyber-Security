---
tipo: nota_lezione
corso: "Programmazione"
tags: [uni, programmazione, appunti, Completed]
creato: 2026-03-03 21:47
---

# 📝 Lezione: Sistemi di ottimizzazione per il ciclo Fetch-Decode-Execute
**Corso:** [[Programmazione]]

---
## Contenuto
Se la CPU dovesse pescare ogni singola istruzione direttamente dalla RAM, passerebbe il 99% del suo tempo ad aspettare, poiché la RAM è incredibilmente lenta rispetto alla velocità di calcolo di un processore moderno.
Ecco come la CPU ottimizza il suo lavoro utilizzando **Registri** e **Cache**.

## 1. La Piramide della Memoria: Velocità vs Capacità
Per capire il ciclo di esecuzione, dobbiamo immaginare una piramide dove, salendo verso la punta (la CPU), la memoria diventa più veloce, più costosa e più piccola.
- **Registri (La punta):** All'interno della CPU. Velocità istantanea (ciclo di clock zero). Contengono pochissimi dati (64 bit l'uno).
- **Cache (L1, L2, L3):** Memoria statica (SRAM) integrata nel chip. Molto veloce.
- **RAM (La base):** Memoria dinamica (DRAM). "Lenta" perché esterna alla CPU e deve viaggiare su un bus.

## 2. Il ruolo dei Registri nel Ciclo Fetch-Decode-Execute
I registri sono le "mani" della CPU. Senza di essi, il ciclo di esecuzione non avrebbe un posto dove appoggiare temporaneamente i dati.
1. **PC (Program Counter):** Durante il **Fetch**, questo registro tiene l'indirizzo della prossima istruzione. Appena l'istruzione viene prelevata, il PC si aggiorna per puntare alla successiva.
2. **IR (Instruction Register):** Qui viene depositata l'istruzione appena prelevata dalla memoria. È qui che avviene il **Decode**.
3. **MAR (Memory Address Register):** Contiene l'indirizzo di memoria a cui la CPU vuole accedere (per leggere o scrivere).
4. **Accumulatore (o registri generali):** Dove vengono messi i numeri durante l'**Execute**. Se devi fare 5+3, il 5 sta in un registro, il 3 in un altro, e il risultato (8) finirà in un terzo registro.

## 3. La Memoria Cache: Il "Buffer" Anti-Attesa
La RAM è distante dalla CPU. Ogni volta che la CPU chiede un dato alla RAM, deve aspettare centinaia di cicli di clock (un'eternità per lei). La **Cache** risolve questo problema tramite due principi:
- **Località Temporale:** Se la CPU ha appena usato un dato, è molto probabile che lo userà di nuovo a breve. La Cache lo tiene lì "vicino".
- **Località Spaziale:** Se la CPU chiede l'istruzione all'indirizzo `100`, è quasi certo che chiederà anche la `101, 102, 103`. La Cache preleva un intero blocco dalla RAM in anticipo.

### I livelli di Cache:
- **L1 (Livello 1):** La più piccola e veloce, divisa tra istruzioni e dati.
- **L2:** Più grande, solitamente dedicata a ogni singolo core.
- **L3:** Condivisa tra tutti i core della CPU, serve a coordinare i dati tra di loro.

## 4. Dall'Algoritmo al Ciclo di Macchina
Prima di diventare una sequenza di Fetch-Decode-Execute, un programma nasce come **Algoritmo**.
1. **Algoritmo:** Una sequenza logica di passi (es. "Se il numero è pari, dividi per 2"). È un concetto astratto, spesso scritto in **Pseudocodice**.
2. **Codice ad alto livello:** Traduci l'algoritmo in un linguaggio come C++ o Python.
3. **Compilazione/Interpretazione:** Il traduttore trasforma le tue funzioni complesse in centinaia di micro-istruzioni (MOV, ADD, JMP).
4. **Caricamento:** Il Sistema Operativo copia queste istruzioni dal disco alla RAM.
5. **Ciclo di Macchina:** La CPU inizia il Fetch della prima istruzione puntata dal Program Counter.

> **Esempio pratico:** Se il tuo algoritmo dice `x = a + b`, la CPU farà:
> - **Fetch** dell'istruzione di somma.
> - **Decode**: "Ah, devo sommare due numeri".
> - **Execute**: Prendi `a` dalla Cache/RAM, mettilo nel Registro 1. Prendi `b`, mettilo nel Registro 2. Somma. Metti il risultato nel Registro 3.

---
## Collegamenti
- Torna al corso: [[Programmazione]]