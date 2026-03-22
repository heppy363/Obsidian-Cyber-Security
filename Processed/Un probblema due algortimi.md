---
tipo: nota_lezione
corso: "Algoritmi"
tags: [AlgoritmiUNI, uni, appunti, Completed]
creato: 2026-03-21 23:10
---

# 📝 Lezione: Un probblema due algortimi
**Corso:** [[Algoritmi]]

---
## Contenuto
Consideriamo il seguente caso:
`Ricercare un elemento dentro un array` 
per risolvere questo problema si anno diverse strade: 
- [[Ricerca Linerare]]
Ora supponiamo che il nostro array sia ordinato in ordine crescente:
- [[Ricerca binaria]]
Questi due algoritmi fano la stessa cosa ma con una differenza sostanziale ovvero il tempo di esecuzione: 
 Supponiamo n=108 (100 milioni di elementi) e una velocità di 105 operazioni/secondo:

|Algoritmo|Formula Operazioni|Tempo Stimato|
|---|---|---|
|**Lineare**|108/105=1000 secondi|**~16,6 minuti**|
|**Binaria**|log2​(108)/105≈27/105|**0,00027 secondi**|


> **Nota:** log2​(108) è circa 27. La differenza è abissale: passiamo da un quarto d'ora a un istante impercettibile.

Intuitivamente capiamo che da un analisi _gready_ quindi intuitiva possiamo andare a migliorare quella che e la nostra implementazione per ottenere delle prestazioni migliori in termini di computazione. 
- se e corretto -> da sempre la risposta corretta indipendentemente dalla istanza del problema (le variabili) 
- se e completo -> ogni risposta che produce la deve necessariamente restituire 
Da qui si entra nel concetto di [[Complessita computazionale]] un metro di missa per capire come il nostra algoritmo sta performando e capire se per quel determinato problema si effettivamente il migliore.  


---
## Collegamenti
- Torna al corso: [[Algoritmi]]