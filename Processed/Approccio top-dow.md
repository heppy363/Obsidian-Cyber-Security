---
tipo: nota_lezione
corso: "Programmazione"
tags: [uni, programmazione, appunti, Completed]
creato: 2026-03-21 13:37
---

# 📝 Lezione: Approccio top-dow
**Corso:** [[Programmazione]]

---
## Contenuto
L'approccio **Top-Down** (dall'alto verso il basso) è una delle metodologie cardine dell'ingegneria del software per la risoluzione di problemi complessi. Si basa sul principio del _divide et impera_: scomporre un problema vasto in parti progressivamente più piccole e gestibili.

## Definizione e Strategia
Nell'approccio Top-Down, si parte dalla definizione del problema generale (il livello più alto di astrazione) e si procede verso il basso attraverso successivi livelli di dettaglio.
- **Punto di Partenza**: Il problema iniziale viene visto come la **radice** di una struttura ad albero.
- **Scomposizione Gerarchica**: Per ogni elemento del problema si individua un singolo sottosistema o funzione che lo descrive.
- **Riduzione dell'Astrazione**: Man mano che si scende nella gerarchia, l'astrazione diminuisce; si passa da concetti larghi e teorici a soluzioni granulari e concrete.

##  Il Processo di Scomposizione
Il passaggio dal "problema radice" alle soluzioni finali avviene seguendo fasi precise:
1. **Analisi del Problema**: Si identifica la funzione principale dell'intero software.
2. **Scomposizione in Sotto-problemi**: Il problema viene diviso in moduli più semplici e ordinati.
3. **Raffinamento Progressivo**: Ogni sotto-problema viene ulteriormente scomposto in "problemi elementari" finché non si arriva a unità così semplici da essere descrivibili come una serie di azioni finite.
4. **Descrizione in Linguaggio Naturale**: Ogni livello intermedio viene descritto chiaramente per facilitare la comprensione di "chi fa cosa".

## Struttura a "Foglie" e Logica di Controllo
La struttura finale dell'approccio Top-Down somiglia a un albero rovesciato:
- **Nodi**: Rappresentano le decisioni metodologiche e le scomposizioni intermedie.
- **Foglie**: Rappresentano la soluzione concreta ai problemi elementari identificati; sono le "azioni finite" che l'esecutore dovrà compiere.

## I 3 Principi di Scomposizione
Durante il processo Top-Down, ogni sotto-problema viene tipicamente risolto seguendo tre schemi logici, che spesso guidano anche la scelta del linguaggio di programmazione:
- **Sequenza**: Attività da compiere l'una dopo l'altra.
- **Alternativa**: Attività eseguite in maniera esclusiva in base a una scelta (es. if-else).
- **Iterazione**: Attività che devono essere ripetute una o più volte (es. cicli).

## Vantaggi dell'Approccio
L'utilizzo di questa metodologia garantisce diversi benefici durante lo sviluppo:
- **Chiarezza**: È molto facile identificare le responsabilità dei singoli moduli (chi si occupa di cosa).
- **Mantenibilità**: La scomposizione facilita la manutenzione futura, poiché è più semplice intervenire su un piccolo modulo elementare che sull'intero sistema.
- **Efficienza**: Permette di selezionare le risorse necessarie per ottenere coerenza e precisione fin dalle prime fasi.

![[Immagine 2026-03-04 195323.png]]


---
## Collegamenti
- Torna al corso: [[Programmazione]]