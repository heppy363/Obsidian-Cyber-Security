---
tipo: nota_lezione
corso: Algoritmi
tags:
  - uni
  - appunti
  - Completed
  - programmazione
creato: 2026-03-21 13:15
---

# 📝 Lezione: requisiti del software
**Corso:** [[Programmazione]]

---
## Contenuto

Questo documento rappresenta la formalizzazione di tutto ciò che è stato discusso durante le interviste e l'analisi. È il punto di passaggio obbligatorio: **senza approvazione, non si scrive codice**.
## 1. Cosa deve contenere il documento?
Per essere efficace, il documento deve rispondere a tre domande fondamentali:
- **Dati in Input**: Quali informazioni riceve il programma?
- **Dati in Output**: Quali risultati deve produrre?
- **Soluzione di massima**: Una descrizione logica del processo di trasformazione dei dati.

## 2. Le tre caratteristiche d'oro di un buon requisito
Affinché il documento sia approvabile, ogni singolo requisito deve essere:
- **Non Ambiguo**: Deve essere interpretabile in un solo modo da chiunque lo legga (cliente e programmatore).
- **Consistente**: Non devono esserci requisiti che si contraddicono tra loro.
- **Completo**: Deve coprire tutte le situazioni possibili e i casi limite (es. "cosa succede se l'utente inserisce una data sbagliata?").

## 3. Classificazione dei Requisiti
All'interno del documento, i requisiti si dividono in due grandi famiglie:

|Tipo di Requisito|Descrizione|Esempio Pratico|
|---|---|---|
|**Funzionale**|Definisce **cosa** deve fare il programma e quali dati deve usare.|"Il sistema deve permettere il login tramite email e password."|
|**Non Funzionale**|Definisce **come** il programma deve comportarsi (prestazioni, ambiente).|"Il software deve girare su Windows 11 e caricare le pagine in meno di 1 secondo."|

## 4. Perché è così importante?
Il documento dei requisiti serve a proteggere entrambi gli attori:
- **Per il Programmatore**: Definisce i "confini" del lavoro. Se il cliente chiede una funzione extra a metà opera, il documento serve a dire: "Questo non era previsto, richiede un nuovo preventivo".
- **Per il Cliente**: Garantisce che il bisogno iniziale venga effettivamente risolto.
- **Evita il Backtracking**: Ripartire da zero perché si è capito male un concetto è il costo più alto che un progetto possa avere.

## Consiglio per lo studio
Ricorda che l'analisi dei requisiti si concentra sul **COSA** (fase di analisi), mentre la progettazione successiva si concentra sul **COME** (fase di sintesi).


---
## Collegamenti
- Torna al corso: [[Programmazione]]