---
tipo: nota_lezione
corso: "Programmazione"
tags: [uni, programmazione, appunti, Completed]
creato: 2026-03-21 14:02
---

# 📝 Lezione: Il come
**Corso:** [[Programmazione]]

---
## Contenuto

## 1. Dal Problema all'Istanza: Il Ruolo delle Variabili
- **Il Problema**: È una classe di domande omogenee risolvibili con un metodo uniforme.
- **L'Istanza**: Rappresenta la domanda specifica, ovvero il "problema reale" che l'utente incontra ogni giorno inserendo dati diversi.
- **Le Variabili**: Sono lo strumento tecnico che permette di passare dal problema generale all'istanza specifica, rendendo il software flessibile.

## 2. Classificazione e Risolvibilità (Filtro Tecnico)
Prima di scrivere codice, bisogna classificare la richiesta del cliente:
- **Problemi imprecisi/ambigui**: La descrizione manca di un metodo risolutivo chiaro, portando a potenziali errori.
- **Problemi con più soluzioni**: In base ai requisiti (tempo, soldi, velocità), si sceglie l'algoritmo più vantaggioso.
- **Problemi non calcolabili**: Situazioni logicamente impossibili per cui non esiste soluzione.
- **Problemi non trattabili**: Esistono soluzioni, ma richiedono tempi o risorse non funzionali (es. Torre di Hanoi).

## L'Algoritmo: La Soluzione Universale
L'algoritmo funge da ponte tra il problema e l'esecutore. Per rispondere alla variabilità dei dati (istanze), deve essere:
- **Preciso e non ambiguo**: L'esecutore non deve interpretare, ma solo eseguire passi chiari.
- **Finito**: Deve garantire un risultato in un tempo e numero di passi definiti.
- **Riproducibile**: Deve generare lo stesso output partendo dallo stesso input.

## Esecuzione: Programma e Dinamicità
Il software prende vita quando l'algoritmo incontra il calcolatore.
## 1. L'Esecutore (Il Processore)
- È un componente "stupido" che esegue istruzioni in modo automatico.
- Interpreta i passi dell'algoritmo e trasforma gli input in output.
- Senza l'esecutore, l'algoritmo non può essere attuato.
## 2. Sequenza Statica vs Dinamica
Questa distinzione spiega come il software muta al variare dei dati:
- **Sequenza Statica**: È il codice scritto, l'implementazione precisa dell'algoritmo che rimane immutabile.
- **Sequenza Dinamica**: È il percorso effettivo compiuto dall'esecutore. Cambia in base ai dati di ingresso (istanze) che attivano selezioni (`if`) o iterazioni (`while`), rendendo il flusso variabile.

## Conclusione del "Collante"

> Il **problema** definisce il "cosa", i **requisiti** ne filtrano la **trattabilità**, l'**algoritmo** progetta la soluzione universale e il **programma** istruisce l'**esecutore** per gestire ogni singola **istanza** attraverso una **sequenza dinamica** di passi.

---
## Collegamenti
- Torna al corso: [[Programmazione]]