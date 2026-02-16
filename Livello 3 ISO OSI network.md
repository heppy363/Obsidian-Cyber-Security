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

## 1. Lo Scopo del Livello 3: L'Instradamento
Mentre il [[Livello 2 ISO OSI Data link]] si occupa di spostare i dati tra due macchine vicine (nello stesso segmento fisico), il Livello 3 si occupa dell'**interconnessione globale**. Il suo compito è il **Routing**.
### Le due funzioni chiave:
1. **Inoltro (Forwarding):** È l'azione locale. Quando un pacchetto arriva su un'interfaccia di un router, il router deve decidere su quale interfaccia d'uscita mandarlo. Pensa a un incrocio stradale.
2. **Instradamento (Routing):** È il processo globale. Tramite algoritmi complessi, la rete determina il percorso migliore (il più breve, il più veloce o il meno costoso) che un pacchetto deve seguire dall'origine alla destinazione. Pensa al GPS che pianifica l'intero viaggio.
## 2. L'Unità di Misura: Il Pacchetto (Datagramma)
A questo livello non parliamo più di bit o di frame, ma di **Pacchetti** (o più precisamente, nel mondo IP, di **Datagrammi**).
- Il pacchetto è composto da un **Header** (intestazione) che contiene informazioni cruciali (come gli indirizzi IP) e dal **Payload** (i dati che arrivano dal Livello 4 - Trasporto).

## 3. L'Indirizzamento Logico (IP)
Questa è la caratteristica distintiva. Mentre il Livello 2 usa indirizzi fisici (MAC) che sono "scritti" nell'hardware, il Livello 3 usa **Indirizzi Logici (IP)**.
- Gli indirizzi IP sono gerarchici (come un indirizzo postale: Città -> Via -> Numero) e permettono di raggruppare i dispositivi in sottoreti.
- **IPv4 vs IPv6:** Nel 2026, la transizione è quasi completa, ma studierai entrambi (32 bit vs 128 bit).
## 4. Apparati e Protocolli: Chi comanda qui?
### L'Apparato: Il Router
Il router è il re del Livello 3. È un computer specializzato che possiede una **Tabella di Routing**. Legge l'indirizzo IP di destinazione di ogni pacchetto, lo confronta con la sua tabella e lo lancia verso il prossimo "salto" (_hop_).
### I Protocolli Principali:
- **IP (Internet Protocol):** Il protocollo di trasporto fondamentale (best-effort, non garantisce la consegna).
- **ICMP (Internet Control Message Protocol):** Usato per messaggi di errore e diagnostica (il comando `ping` ne è l'esempio classico).
- **Protocolli di Routing (RIP, OSPF, BGP):** Sono i "linguaggi" con cui i router parlano tra loro per scambiarsi informazioni sulle strade migliori da percorrere.
## 5. Caratteristiche Fondamentali (Domande da Esame)
- **Servizio Connectionless (Senza Connessione):** Di base, il protocollo IP non stabilisce una sessione. Ogni pacchetto è un'entità indipendente e potrebbe persino seguire percorsi diversi per arrivare alla stessa destinazione.
- **Best-Effort Delivery:** Il Livello 3 non garantisce che il pacchetto arrivi. Se un router è troppo carico, semplicemente "scarta" il pacchetto. Saranno i livelli superiori (come il TCP al livello 4) a preoccuparsi di richiederne l'invio.    
- **Frammentazione:** Se un pacchetto è troppo grande per la rete che deve attraversare (supera la _MTU - Maximum Transmission Unit_), il Livello 3 ha il compito di spezzettarlo e riassemblarlo.

- [[PDU livello 3 ISO OSI]]

## Link 
1) 