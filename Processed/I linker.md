---
tipo: nota_lezione
corso: "Programmazione"
tags: [uni, programmazione, appunti, Completed]
creato: 2026-03-03 21:55
---

# 📝 Lezione: I linker
**Corso:** [[Programmazione]]

---
## Contenuto
Il **Linker** (o editore di legami) è l'ultima stazione della "catena di montaggio" che trasforma il codice sorgente in un file eseguibile. Spesso viene confuso con il compilatore, ma il suo compito è profondamente diverso: se il compilatore traduce le singole pagine, il linker le rilega insieme per creare un libro finito e coerente.
In ambito universitario, studiare il Linker significa capire la **gestione degli indirizzi** e la risoluzione dei simboli.

## 1. Perché serve il Linker? (Compilazione Separata)
I programmi moderni non sono scritti in un unico file da migliaia di righe. Sono divisi in decine di moduli (file `.c`, `.cpp`, ecc.) e librerie esterne.
- Ogni modulo viene compilato separatamente producendo un **File Oggetto** (es. `.obj` o `.o`).
- Il file oggetto contiene linguaggio macchina, ma ha un problema: **gli indirizzi sono relativi**. Se nel Modulo A chiami una funzione che sta nel Modulo B, il compilatore del Modulo A non sa ancora a quale indirizzo di memoria si troverà quella funzione.

## 2. Le due funzioni principali del Linker
### A. Risoluzione dei Simboli (Symbol Resolution)
Il compilatore crea una **Tabella dei Simboli** per ogni file oggetto. Questa tabella elenca:
- **Simboli definiti:** Funzioni e variabili globali create in quel modulo.
- **Simboli esterni:** Funzioni o variabili dichiarate ma non trovate (es. la funzione `printf` della libreria standard).
Il Linker analizza tutti i file oggetto e le librerie, cercando di "accoppiare" ogni simbolo esterno con la sua definizione corretta. Se non la trova, genera il famoso errore: _“Unresolved External Symbol”_.

### B. Rilocazione (Relocation)
Il compilatore assume che ogni modulo inizi dall'indirizzo di memoria `0`. Ovviamente, non possono stare tutti allo stesso indirizzo.
- Il Linker unisce le sezioni di codice dei vari file oggetto in un'unica sezione di codice (`.text`).
- Unisce le sezioni di dati in un'unica sezione dati (`.data`).
- **Ricalcola tutti gli indirizzi**: aggiorna ogni istruzione di salto (`JMP`) e ogni riferimento a variabili in modo che puntino alla nuova posizione corretta nel file eseguibile finale.
## 3. Linker Statico vs Linker Dinamico
Questa è la distinzione tecnica fondamentale che separa i sistemi operativi moderni da quelli del passato.
### Linkaggio Statico (Static Linking)
Tutto il codice necessario (incluse le librerie di sistema) viene copiato fisicamente dentro l'eseguibile.
- **Pro:** Il programma è "auto-sufficiente". Lo porti su un altro PC e funziona sempre.
- **Contro:** L'eseguibile è molto pesante. Se 10 programmi usano la stessa libreria, avrai 10 copie dello stesso codice in RAM, sprecando spazio.
### Linkaggio Dinamico (Dynamic Linking)
Il Linker non copia il codice della libreria, ma inserisce solo un "puntatore" (un riferimento). Il collegamento vero e proprio avviene quando il programma viene lanciato (grazie al **Dynamic Loader**).
- **Librerie Condivise:** Su Windows sono i file **.dll** (Dynamic Link Library), su Linux i file **.so** (Shared Object).
- **Pro:** Risparmio di RAM (la libreria è caricata una sola volta per tutti i programmi) e aggiornamenti facili (se aggiorni la DLL, tutti i programmi ne beneficiano senza essere ricompilati).
- **Contro:** Se la DLL manca o è la versione sbagliata, il programma non parte ("DLL Hell").

## 4. Struttura di un Eseguibile (ELF o PE)
Il risultato del lavoro del linker è un file strutturato (formato **ELF** su Linux, **PE** su Windows). Non è solo codice binario, ma contiene degli **Header** (intestazioni) che dicono al Sistema Operativo:
1. "Dove inizia la prima istruzione (Entry Point)".
2. "Quanta memoria serve per i dati".
3. "Quali librerie dinamiche devo caricare prima di partire".

### Riassunto tecnico per l'esame
> Il **Compilatore** si occupa della **Sintassi** e della traduzione logica locale. Il **Linker** si occupa della **Topologia** e della coerenza globale degli indirizzi.
Senza il linker, saremmo costretti a scrivere programmi giganteschi in un unico file, rendendo lo sviluppo collaborativo e le librerie standard impossibili da gestire.

---
## Collegamenti
- Torna al corso: [[Programmazione]]