---
tipo: nota_lezione
corso: "Algoritmi"
tags: [AlgoritmiUNI, uni, appunti, Completed]
creato: 2026-03-21 23:01
---

# 📝 Lezione: Esempio di applicazione del teorema di Böhm-Jacopini
**Corso:** [[Algoritmi]]

---
## Contenuto
Il teorema ci dice che, per quanto l'azione possa sembrare complessa, possiamo ridurla esclusivamente a **Sequenze**, **Selezioni** e **Cicli**.

---

## Esempio: Algoritmo "Caffè Mattutino"
Ecco come applichiamo le tre strutture in modo ricorsivo:
1. **Sequenza (Passi ordinati):**
    - Svitare la moka.
    - Mettere l'acqua nel serbatoio.
    - Inserire il filtro.
2. **Ciclo / Iterazione (Ripetizione finché una condizione è vera):**
    - **Mentre** il filtro non è pieno:
        - Aggiungi un cucchiaino di caffè.
    - _(Questa è la struttura "While" del teorema)_
3. **Selezione / Condizione (Bivio decisionale):**
    - **Se** vuoi il caffè zuccherato:
        - Aggiungi lo zucchero.
    - **Altrimenti**:
        - Versalo amaro nella tazzina.

## Perché è importante
Il teorema è rivoluzionario perché ha dimostrato matematicamente che **non serve il comando "GOTO"** (saltare da un punto all'altro del codice in modo disordinato, il cosiddetto _Spaghetti Code_).
Ogni algoritmo complesso può essere "scomposto" in questi tre mattoncini fondamentali. Come hai giustamente scritto nei tuoi appunti, il teorema non dice che questa sia la soluzione _più veloce_ (efficienza), ma garantisce che sia _possibile_ farlo usando solo queste tre strutture.

## Un dettaglio tecnico per l'esame
Ricorda che queste strutture si applicano in modo **gerarchico o ricorsivo**: dentro una _Selezione_ (un `if`) puoi avere un _Ciclo_, e dentro quel _Ciclo_ puoi avere un'altra _Sequenza_. Questa "componibilità" è ciò che rende potente il teorema.

---
## Collegamenti
- Torna al corso: [[Algoritmi]]