---
tipo: nota_lezione
corso: "Programmazione"
tags: [uni, programmazione, appunti, Completed]
creato: 2026-03-04 19:03
---

# 📝 Lezione: Progettazione di un programma
**Corso:** [[Programmazione]]

---
## Contenuto
La creazione di un programma non si riduce alla sola scrittura del codice; quella è, in realtà, una delle fasi finali. Per sviluppare software di qualità è necessario seguire un iter strutturato che riduca il rischio di errori e ottimizzi i costi di produzione (manutenibilità).

## 1. Fase di Analisi: Capire "Cosa" fare
Prima di progettare la soluzione, bisogna comprendere il problema attraverso l'**Analisi dei Requisiti**.
- **Obiettivo**: Definire con precisione le funzioni che il software deve implementare, stabilendone i confini.
- **Il Cliente**: È colui che ha un bisogno da risolvere. Una comunicazione costante ed efficiente è fondamentale per evitare fraintendimenti.
- **Documento dei Requisiti**: Ogni requisito deve essere chiaro, non ambiguo e approvato dal cliente. Solo dopo l'approvazione di questo documento si può procedere oltre, evitando il rischio di **backtracking** (dover tornare sui propri passi e rifare il lavoro).
	- [[requisiti del software]]
## 2. Fase di Progettazione: Capire "Come" farlo
Una volta definiti i requisiti, si passa alla strategia risolutiva.
- **Scomposizione del problema**: Un problema complesso viene diviso in sotto-problemi più semplici e ordinati. Questo facilita sia la comprensione iniziale che la futura manutenzione del software.
- **Definizione dell'Algoritmo**: Si progetta una sequenza logica di passi per ottenere il risultato corretto. In questa fase l'**ordine di esecuzione** delle istruzioni è fondamentale: se cambia la sequenza, cambia il risultato dell'algoritmo.
	- [[Strumenti per creare algoritmi]]

## 3. Fase di Realizzazione e Verifica
Dopo che la logica è chiara e completa, si passa all'implementazione pratica seguendo questi step:
1. **Scrittura del codice**: Si traduce l'algoritmo in un linguaggio di programmazione ad alto livello.
2. **Debug (Errori di Sintassi)**: In questa fase intervengono i traduttori (compilatori o interpreti) che segnalano se i vincoli del linguaggio non sono stati rispettati. Se questi errori non vengono rimossi, il programma non può essere eseguito.
3. **Test del programma**: Qui il codice è formalmente corretto e "gira". L'obiettivo è individuare **errori logici**: il programmatore verifica se il software produce i risultati attesi.
4. **Debugging logico**: Si utilizza un software specifico (debugger) per eseguire il codice istruzione per istruzione e capire esattamente dove la logica si rompe.
5. **Correzione e Ciclo**: Se vengono trovati errori, si torna alla fase di scrittura e si ripete il test finché il codice non è dichiarato funzionante.

## Concetti Chiave da ricordare
> - **Backtracking**: Il ritorno a fasi precedenti dovuto a errori di progettazione o requisiti poco chiari.
> - **Manutenibilità**: La facilità con cui un software può essere aggiornato o corretto nel tempo.
> - **Algoritmo**: Il "cuore" logico che precede sempre il codice.




---
## Collegamenti
- Torna al corso: [[Programmazione]]