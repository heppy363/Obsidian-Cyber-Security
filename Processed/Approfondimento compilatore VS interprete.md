---
tipo: nota_lezione
corso: "Programmazione"
tags: [uni, programmazione, appunti, Completed]
creato: 2026-03-03 21:53
---

# 📝 Lezione: Approfondimento compilatore VS interprete 
**Corso:** [[Programmazione]]

---
## Contenuto
## 1. Il Compilatore: Traduzione Statica e Ottimizzazione
Il compilatore è un programma complesso che trasforma il **Codice Sorgente** (High Level) in **Codice Oggetto** (Linguaggio Macchina specifico per l'ISA della CPU).
### Le fasi della compilazione (Il "Front-end" e "Back-end")
1. **Analisi Lessicale (Lexing):** Il codice viene ridotto in "token" (parole chiave, operatori).
2. **Analisi Sintattica (Parsing):** Viene costruito un **AST (Abstract Syntax Tree)**, un albero che rappresenta la struttura logica del programma. Se l'albero non può essere costruito, hai un _Syntax Error_.
3. **Analisi Semantica:** Il compilatore controlla la coerenza (es. non puoi sommare una stringa a un intero).
4. **Ottimizzazione del Codice:** Questa è la parte "succosa". Il compilatore riorganizza le istruzioni per sfruttare i **registri della CPU**, elimina codice morto e srotola i cicli (_loop unrolling_) per aumentare la velocità.
5. **Generazione del Codice:** Viene prodotto il file binario.
### Peculiarità tecniche:
- **Static Linking:** Il compilatore (o meglio, il _Linker_) unisce tutte le librerie esterne in un unico file eseguibile.
- **Performance:** Il codice è già pronto per la CPU. Non c'è overhead durante l'esecuzione.
- **Dipendenza dall'Hardware:** Il binario generato per un Intel non funzionerà su un processore ARM (Apple M1/M2 o smartphone).

---
## 2. L'Interprete: Esecuzione Dinamica
L'interprete non genera un file separato. È un programma che "legge" il sorgente e simula l'esecuzione delle istruzioni in tempo reale.
### Come funziona tecnicamente
1. L'interprete analizza una riga (o un'unità logica).
2. Chiama una funzione interna (scritta in C o C++) che esegue quell'azione sull'hardware.
3. Passa alla riga successiva.
### Peculiarità tecniche:
- **Late Binding:** Il tipo di una variabile viene deciso solo quando la riga viene eseguita. Questo permette il **duck typing** (tipizzazione dinamica).
- **Portabilità:** Lo stesso script Python gira su Windows, Mac e Linux senza modifiche, perché è l'interprete (già installato sul sistema) a farsi carico della traduzione specifica per quell'OS.
- **Overhead:** Poiché il PC deve "pensare" a come tradurre mentre esegue, le performance sono tipicamente da 10 a 100 volte inferiori rispetto a un linguaggio compilato.

---
## 3. L'Approccio Ibrido: Bytecode e JIT (Just-In-Time)
Oggi la distinzione netta sta scomparendo. Linguaggi come **Java** o **C#** usano un approccio misto per ottenere il meglio dai due mondi.
1. **Compilazione in Bytecode:** Il codice sorgente non viene tradotto in linguaggio macchina, ma in un linguaggio intermedio universale (es. il _Java Bytecode_).
2. **Virtual Machine (JVM / .NET):** Una "macchina virtuale" legge il bytecode.
3. **Compilazione JIT (Just-In-Time):** Mentre il programma gira, la macchina virtuale identifica le parti di codice eseguite più spesso ("hot spots") e le **compila al volo** in linguaggio macchina reale, salvandole in RAM.
---
## 4. Analisi Comparativa Universitaria
### Perché questa differenza è vitale?
Se stai scrivendo il software di controllo di una **frenata ABS** in un'auto, userai un linguaggio **compilato** (C): hai bisogno di tempi di risposta deterministici e zero overhead. Se stai scrivendo uno script per analizzare dati scientifici o un prototipo rapido, userai un **interprete** (Python): la velocità di sviluppo conta più della velocità di esecuzione.

- [[I linker]]
---
## Collegamenti
- Torna al corso: [[Programmazione]]