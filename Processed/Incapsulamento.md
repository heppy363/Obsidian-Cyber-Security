---
aliases:
  - Completate
tags:
  - Completed
  - CompTIAnetwork
  - Certificati
---
--- 
## Nozioni
L'incapsulamento è il processo mediante il quale i dati scendono lungo la pila del modello **ISO/OSI**, venendo "impacchettati" con informazioni aggiuntive (header e trailer) a ogni livello.
Pensa all'incapsulamento come a una serie di **matrioske** o a una lettera spedita via posta: il tuo messaggio (i dati) viene messo in una busta, che viene messa in un furgone, che viaggia su una strada.

### Come funziona il processo (Step-by-Step)
Quando invii un dato (es. un'email), questo attraversa i livelli dal 7 al 1:
1. **Dati (Livelli 7-5):** L'applicazione genera i dati puri.
2. **Segmento (Livello 4 - Trasporto):** Ai dati viene aggiunto l'header **TCP** o **UDP** (numeri di porta).
3. **Pacchetto (Livello 3 - Rete):** Al segmento viene aggiunto l'header **IP** (indirizzi IP mittente e destinatario).
4. **Frame (Livello 2 - Data Link):** Al pacchetto vengono aggiunti l'header e il trailer **Ethernet** (indirizzi MAC e controllo errori).
5. **Bit (Livello 1 - Fisico):** Il frame viene convertito in segnali elettrici, ottici o radio.

Al ricevente avviene il processo inverso, chiamato **decapsulamento**: ogni livello "scarta" l'intestazione di sua competenza e passa il resto al livello superiore.

### Perché è un principio fondamentale?
L'incapsulamento non è solo un modo di organizzare i dati, ma il pilastro che garantisce il funzionamento di Internet per tre motivi chiave:
#### 1. Astrazione e Modularità (L'indipendenza)
Grazie all'incapsulamento, un livello non ha bisogno di sapere _come_ lavora quello sotto.
- **Esempio:** Al tuo browser (Livello 7) non interessa se sei connesso via Wi-Fi, cavo Ethernet o fibra ottica (Livello 1). Il "pacchetto" resta lo stesso, cambia solo l'ultimo "involucro".
#### 2. Separazione delle responsabilità
Ogni livello si occupa di un problema specifico senza interferire con gli altri:
- Il **Livello 4** si assicura che i dati arrivino integri.
- Il **Livello 3** si occupa di trovare la strada (routing).
- Il **Livello 2** si occupa del passaggio fisico tra due dispositivi vicini.
#### 3. Standardizzazione (Interoperabilità)
Permette a dispositivi di produttori diversi di comunicare. Un server Linux può inviare dati a un iPhone perché entrambi seguono le stesse regole di "impacchettamento". Se cambiassi il protocollo di un livello (es. passi da IPv4 a IPv6), dovresti cambiare solo l'involucro di quel livello, senza dover riscrivere tutte le applicazioni web.

### Curiosità per i tuoi studi (CompTIA Network+)
Nel gergo tecnico, ogni unità di dati incapsulata ha un nome specifico chiamato **PDU (Protocol Data Unit)**. Ricordare questa sequenza è fondamentale per l'esame:
- Livello 4: **Segmento**
- Livello 3: **Pacchetto**
- Livello 2: **Frame**
- Livello 1: **Bit**

## Link 
1) 