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
### 1. Il Ciclo di Vita di un Inoltro

Quando un pacchetto arriva su un'interfaccia di ingresso del router, avvengono tre passaggi chiave:
1. **Ricezione e decapsulamento:** Il router riceve il frame (Livello 2), verifica che sia per lui, lo apre e ne estrae il pacchetto (Livello 3).
2. **Lookup (Ricerca):** Il router legge l'**Indirizzo IP di destinazione** nell'header del pacchetto e consulta la tabella di inoltro per trovare la corrispondenza migliore.
3. **Commutazione (Switching):** Il pacchetto viene spostato attraverso il "backplane" (la struttura interna del router) dall'interfaccia di ingresso a quella di uscita corretta.
4. **Incapsulamento e Invio:** Il router ri-impacchetta il pacchetto in un nuovo frame (Livello 2) adatto alla nuova tratta fisica e lo spedisce.
### 2. La Regola d'Oro: Longest Prefix Match (LPM)
Questa è una nozione da esame. Un router potrebbe avere più rotte che corrispondono alla stessa destinazione. Quale sceglie? Sceglie la rotta con il **prefisso di rete più lungo** (ovvero la più specifica).
- **Esempio:**
    - Indirizzo Destinazione: `192.168.1.50`
    - Rotta A: `192.168.1.0/24
    - Rotta B: `192.168.1.0/25`
    - _Scelta:_ Il router userà la **Rotta B** perché il prefisso `/25` è più specifico (lungo) del `/24`.
### 3. Anatomia della Tabella di Inoltro
Cosa c'è dentro questa tabella? Essenzialmente tre colonne:
- **Prefisso di Rete:** L'indirizzo di destinazione o la rete.
- **Interfaccia di Uscita:** Quale porta fisica usare (es. `GigabitEthernet0/1`).
- **Next Hop (Prossimo Salto):** L'indirizzo IP del prossimo router a cui consegnare la "lettera".
### 4. Architettura Hardware: Il Piano di Controllo vs Piano Dati
A livello universitario si studia la separazione dei compiti:
- **Control Plane (Piano di Controllo):** È il software che scambia informazioni di routing e costruisce la tabella. (Lento, gestito dalla CPU).
- **Data Plane (Piano Dati):** È l'hardware (spesso chip specializzati chiamati **ASIC**) che esegue l'inoltro materiale dei pacchetti. (Velocissimo, deve gestire milioni di pacchetti al secondo).
### 5. Cosa cambia nel pacchetto durante l'inoltro?
Attenzione: il pacchetto IP **non è del tutto immutabile**. Durante il forwarding:
1. Il valore del **TTL** viene decrementato di 1.
2. Il **Checksum** dell'header viene ricalcolato (perché il TTL è cambiato).
3. L'header di Livello 2 (MAC address) viene **completamente sostituito**.
### Il concetto di "Default Gateway"
Se il router non trova nessuna corrispondenza specifica nella tabella per un indirizzo, usa la **Rotta di Default** (indicata come `0.0.0.0/0`). È l'uscita di emergenza: "Se non so dove mandarlo, mandalo lì (solitamente verso il provider internet)".

- [[Direzione dei dati nel forwording]]
## Link 
1) 