---
tipo: nota_lezione
corso: "Algoritmi"
tags: [AlgoritmiUNI, uni, appunti, Completed]
creato: 2026-03-24 18:40
---

# 📝 Lezione: Esempio di utilizzo di dividi et impera
**Corso:** [[Algoritmi]]

---
## Contenuto

![[Pasted image 20260324184222.png]]

>Questa immagine mostra un classico esempio di algoritmo **ricorsivo** basato sulla tecnica del **Divide et Impera** per trovare il valore minimo in un array.

## Analisi del Codice
La funzione `recursive_min` non scorre l'array dall'inizio alla fine con un semplice ciclo `for`. Invece, "taglia" continuamente l'array a metà finché non rimangono elementi singoli.

## Come funziona il codice (passo dopo passo):
1. **Caso Base (`if (start == finish)`)**: Se l'intervallo analizzato contiene un solo elemento, quel valore è necessariamente il minimo di quella piccola porzione. La funzione lo restituisce.
2. **Divisione (`int mean = (start+finish)/2`)**: Se ci sono più elementi, l'algoritmo calcola il punto centrale per dividere l'array in due sottoproblemi.
3. **Ricorsione (Imperia)**: La funzione chiama se stessa due volte:
    - Una volta per la metà sinistra (`start` fino a `mean`).
    - Una volta per la metà destra (`mean+1` fino a `finish`).
4. **Combinazione (`return min(...)`)**: Una volta ottenuti i minimi delle due metà, li confronta e restituisce il più piccolo tra i due.

## Perché si usa il Divide et Impera?
Potresti chiederti: _"Perché complicarsi la vita se un ciclo `for` è più semplice?"_. Ecco le ragioni principali in ambito universitario e professionale:
- **Parallelizzazione:** Questa è la ragione tecnica più importante. Poiché le due chiamate ricorsive (metà sinistra e metà destra) sono **indipendenti**, potresti eseguirle contemporaneamente su due processori diversi, dimezzando i tempi di calcolo. Un ciclo `for` standard è invece sequenziale per natura.
- **Logica Architetturale:** Molti algoritmi fondamentali che studierai (come il **Merge Sort** o il **Quick Sort**) usano questa struttura. Capirla sul calcolo del minimo ti serve come base per algoritmi molto più complessi dove il guadagno di prestazioni è enorme (passando da complessità O(n2) a O(nlogn)).
- **Gestione della Cache:** Su array estremamente grandi, suddividere il problema aiuta a lavorare su "pezzi" di dati che entrano più facilmente nella memoria cache del processore, migliorando la velocità di accesso ai dati.

## Efficienza (Big O)
Nonostante la struttura complessa, la complessità temporale rimane O(n), esattamente come un ciclo `for`, perché ogni elemento dell'array viene comunque visitato una volta. La vera differenza sta nella **struttura** che permette l'ottimizzazione hardware (parallelismo).

---
## Collegamenti
- Torna al corso: [[Algoritmi]]