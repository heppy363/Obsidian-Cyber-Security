---
tipo: nota_lezione
corso: "Programmazione"
tags: [uni, programmazione, appunti, Completed]
creato: 2026-03-03 20:44
---

# 📝 Lezione: Computer e programmazione
**Corso:** [[Programmazione]]

---
## Contenuto
In questa prima parte del corso di programmazione si parte dalle basi pero arrivare alla realizzazione del primo effettivo programma in python:
- **che cosa e un programma**: si tratta di una sequenza di azioni che un computer puo eseguire per svolgere un certo compito 
	- il fatto che i computer possano eseguire diversi programmi per assolvere a molti compiti li definisce macchine [[general purpose]]
	- i programmi vengono realizzati dai programmatori di fatto sono gli architetti 
Un computer funzionamento di un computer dipende da _2_ grandi macro componenti
- [[hardware]]
- [[software]]

|Componente|Caratteristica Principale|Esempio|
|---|---|---|
|**CPU**|Esecuzione istruzioni|Intel i9, Apple M3|
|**RAM**|Velocità / Volatilità|16GB DDR5|
|**SO**|Gestione Risorse|Linux, Windows 11|
|**Compilatore**|Traduzione Totale|GCC (per linguaggio C)|
Il computer conosce solo il passaggio e non passaggi di corrente e per rappresentare l'informazioni necessarie al funzionamento dei nostri programmi abbiamo di fatto solo due cifre _0_ e _1_ di fatto il [[Sistema binario]].
- **Bit (Binary Digit):** La più piccola unità di informazione. Può valere **0** (off/scarico) o **1** (on/carico).
- **Byte:** Un gruppo di **8 bit**. È l'unità di misura base della memoria.
    - Con 8 bit, le combinazioni possibili sono 28=256 (valori da 0 a 255).
questo metodo pero ha molteplici problematiche:
- Non si possono rappresentare numeri negativi o numeri con la virgola 
- Per aumentare la dimensione dei numeri che vogliamo rappresentare dobbiamo aumentare fisicamente lo spazio 
per risolvere questi problemi si usa la [[Codifica a complemento a 2]] per rappresentare numeri negativi e il sistema a virgola mobile [[Floating Point]]
- [[Esempio di floating point]]
Tutto questo sistema riguarda ma memorizzazione dei numeri, ma con il sistema binario si possono memorizzare virtualmente tutti i tipo di dato:
- [[Rappresentazione dati testuali]]
- [[Rappresentazioni di immagini]]
- [[Rappresentazioni di suoni]]

#### Dal fisco al astrazione 

Quanto detto fino ad adesso serve per capire come rappresentare l'informazioni e come essa viene vista dal computer ora si passa a come i computer la utilizzano e la trasformano.
- [[Il Ciclo di Macchina Fetch-Decode-Execute]]
- [[la gerarchia dei linguaggi di programmazione]]
per passare da quelli che si definiscono linguaggi di programmazione a basso livello a quelli ad alto livello ci servono degli interpreti o compilati questi fungono da ponte e consentono di fare il passaggi tra un linguaggio macchina molto veloce ma poco capibile da noi esseri umani ad un linguaggi ad alto livello meno veloce in termini di esecuzione ma molto piu capibile da noi esseri umani.
- [[Traduzione Compilatori vs Interpreti]]
Quanto detto rappresenta la catena che ci porta da un linguaggio di basso livello fino alla creazione di un file eseguibile, quindi ora ci si deve spostare su quella che e la struttura logica dei linguaggi di programmazione:
- [[La Triade Formale Lessico, Sintassi e Semantica]]
Ogni linguaggi di programmazione per risolvere i differenti probblemi usa dei [[Paradigmi di Programmazione Stili di Pensiero]] diversi oppure ne unisce diverse categorie questo naturalmente lo si fa per aiutare nella risoluzione di problemi specifici. 


---
## Collegamenti
- Torna al corso: [[Programmazione]]