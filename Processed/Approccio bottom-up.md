---
tipo: nota_lezione
corso: "Programmazione"
tags: [uni, programmazione, appunti, Completed]
creato: 2026-03-21 13:38
---

# 📝 Lezione: Approccio bottom-up
**Corso:** [[Programmazione]]

---
## Contenuto
Il metodo **Bottom-Up** è l'approccio speculare (duale) al [[Approccio top-dow]]. Se nel Top-Down si "scendeva" dal generale al particolare, qui si "sale" dai componenti semplici verso la soluzione complessa.

## Strategia e Logica Induttiva
L'approccio Bottom-Up si basa su un **metodo induttivo**: si parte dal particolare per arrivare al generale.
- **Punto di Partenza**: Si identificano e si realizzano prima i **moduli elementari** (le "foglie" dell'albero delle decisioni).
- **Integrazione**: Questi moduli base vengono poi combinati e integrati tra loro per formare sottosistemi sempre più ampi e complessi, fino alla risoluzione dell'intero problema.
- **Dalle Foglie alla Radice**: In una struttura a albero, questo percorso muove dalle estremità verso il centro (la radice).

## Caratteristiche del Processo
Mentre il Top-Down si concentra sulla scomposizione, il Bottom-Up si concentra sulla **composizione** e sul riutilizzo:
1. **Identificazione dei Blocchi Base**: Si individuano le funzioni elementari che serviranno sicuramente nel progetto.
2. **Realizzazione Granulare**: Si scrivono e si testano singolarmente queste piccole parti (moduli).
3. **Costruzione a Strati**: Si creano "strati" superiori di logica che coordinano i moduli sottostanti.
4. **Astrazione Crescente**: Più si sale, più il software diventa complesso e specifico per il problema del cliente.

## Programmazione Strutturata e Bottom-Up
Il paradigma della **programmazione strutturata** utilizza spesso un approccio sistematico che sfrutta la logica Bottom-Up per garantire la qualità del codice.
- **Modularità**: Questo metodo incoraggia una gestione efficace del codice dividendo il software in blocchi indipendenti.
- **Compiti Precisi**: Ogni modulo elementare deve svolgere un compito ben definito con un unico punto di ingresso e uno di uscita.
- **Affidabilità**: Poiché si parte testando i singoli mattoni di base, è più facile garantire che l'intera struttura finale sia solida e priva di errori nelle fondamenta.

## Confronto Rapido: Top-Down vs Bottom-Up

|Caratteristica|Top-Down|Bottom-Up|
|---|---|---|
|**Punto di partenza**|Problema generale (Radice)|Moduli elementari (Foglie)|
|**Metodo logico**|Deduttivo (Scomposizione)|Induttivo (Integrazione)|
|**Focus principale**|Definizione della struttura|Realizzazione dei componenti|
|**Astrazione**|Da alta a bassa|Da bassa ad alta|

## Nota sulla "Creatività e Intuito"

Come indicato nelle tue note, non esiste un algoritmo universale per decidere quale metodo usare. La scelta dipende dai requisiti del cliente e dalle risorse a disposizione (tempo, budget, personale). Spesso, nella pratica professionale, i due metodi vengono usati insieme.

---
## Collegamenti
- Torna al corso: [[Programmazione]]