---
tipo: nota_lezione
corso: "Dashboaard Rust"
tags: [progetto, rust, linguaggiProg, progettiPersonali, Completed]
creato: 2026-03-08 21:51
---

# 📝 Lezione: Fondamenti del linguaggio
**Corso:** [[Dashboard Rust]]

---
## Contenuto
- le variabili sono uno spazio di memoria che contengono dati 
	- sono composte dal nome e dal loro contenuto 
	- in rust si deve definire anche il tipo di dato essendo fortemente tipizzato come linguaggio 
- Mutabilita e immutabilita 
	- la mutabilita si tratta di una proprita di tutti gli oggetti di rust e consnete la modifica della nostra variabile in termini di dati 
	- la immutabilita non consente il cambio dei dati della variabile 

```rust

let x: i32 = 5;
```
- questa e una variabile non mutabile in quanto _non_ possiede la cheywor _mut_ 

- Shadowing -> conente di avere la variabile con lo stesso nome ma con un tipo di dato diverso 

```rust

let x: i32 = 5;

let x: if64 = 10.0

```
- in questo caso _x_ sono due varibili indipendenti in quanto abbiamo richiamato nuovamente la cheyword _let_ nello stesso scoop quindi nelle gaffe in poco parole 

**Tutti i tipi di dati**
![[Immagine 2026-03-08 221553.png]]
- se il conpilatore non capisce di che variabili stiamo parlando allora lo devi dichiarare te in maniera esplicita 
- Singned integar -> la differenza e solo nella dimensione e posono contenere numeri con segno 
- Unsigne integesrs -> la differenza e solo nella dimensione e non posono contenere numeri con segno 
- Floating point -> differiscono per dimensione e possono contenere numeri con la virgola quindi numeri devimanli 
- boolenans -> valori buleani 
- characters -> contengono solo un tipo di carattere 

**Tipi di dati complesse**
- Le tuple -> hanno valore fissi quindi il numero di elemti inizziale resto quello possono contenere tipi di dato diverso 
- gli arry -> consnetono di salvare un solo tipo di dato e hanno lunghezza fissa 
![[Immagine 2026-03-08 222113.png]]

**Operatori**
![[Immagine 2026-03-08 223827.png]]



---
## Collegamenti
- Torna al corso: [[Dashboard Rust]]