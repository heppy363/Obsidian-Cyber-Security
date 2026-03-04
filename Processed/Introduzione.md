---
tipo: nota_lezione
corso: "Dashboaard Rust"
tags: [progetto, rust, linguaggiProg, progettiPersonali, Completed]
creato: 2026-02-22 21:54
---

# 📝 Lezione: Introduzione
**Corso:** [[Dashboaard Rust]]

---
## Contenuto
Si tratta di un linguaggio di programmazione di basso livello orientato alla memory safty e alle prestazioni tutto questo senza il [[Garbadge collection]]. La prima versione stabile viene rilasciata nel 2015 

### Utilizzo di rust nel mondo aziendale 
- CLI -> command line interface, si tratta di un applicativo da terminale 
	- libbreria molto usata CLAP 
- WebAssembly (Wasm)
	- Leptos 
	- Dioxus
	- Spin framework 
In azziedna questo e lambito i cui il linguaggio per i video che o visto e stato maggiormento usato 
- Backend 
	- Axum 
	- Sea-ORM -> accesso ai DB  
	- SQLx -> accesso ai DB
- Intelligenza artiiciale 
	- RMCP -> si utilizza per connettere modelli IA ad altri sistemi 

per verificare l'installazione si procede cosi:
- Compilatore di Rust, _rustc_ si tratta del compilatore di rust 
- _cargo_ si tratta del gestore pacchetti, quindi quello che consnete di aggiungere pacchetti dalla comunity 
	- usiamo cargo per laciare i nostri programi che al suo interno usa rast 

Usiamo cargo per rannuere i nostri programi e rust analyzer con VS code per scrivere il codice 
```
cargo new nome_proggetto 
```
Ci sono delle convezioni per la convenzioni per la creazione di variabili e proggetti nel mio caso usero sempre _ con il creatore di proggetti di base ci si crea una struttura come questa 
- SCR -> contine il codice sorgente 
- cargo.toml -> contiene le nostre dipendenze 
	- la sezione _edition_ mi indica con quale compilatre deve essere compilato il mio codice quindi quale versione intermni di anni 
	- si tratta del manifest quindi come viene creato il nostro proggeto 
```
cargo run
```
permette di eseguire il nostro codice 
- prima lo compila 
- poi lo esegue 
```
cargo fmt 
```
formata il nostro codice con gli standard della comunity
```
cargo clyppy
```
ci informa se il nostro codice non segue gli standard 


---
## Collegamenti
- Torna al corso: [[Dashboaard Rust]]
- [video delle informazioni](https://www.youtube.com/watch?v=46eBpDUAt0Q&list=PLSLcKcqBWfjLG0UqA_Z4hWaouCGRvrcSR)