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
Attenzione, qui c'è un punto cruciale da chiarire per evitare confusione all'esame: **il router, di norma, non "sale" mai fino al Livello 4.** Un router standard è un dispositivo di **Livello 3**. Legge l'intestazione IP e si ferma lì. Non gli interessa se dentro c'è un messaggio WhatsApp (Livello 7) o un segmento TCP (Livello 4).

Tuttavia, il percorso che descrivi avviene negli **Host** (il tuo PC o un Server) o quando il router deve gestire se stesso (es. quando fai un _ping_ al router).

Ecco la panoramica del flusso dati in entrambe le direzioni:

---

## 1. Flusso in Salita (Ricezione): Dal Cavo verso l'Alto

Immagina che un pacchetto arrivi alla scheda di rete. Il processo è chiamato **Decapsulamento**.

1. **Livello 1 (Fisico):** La scheda di rete riceve segnali elettrici/ottici e li converte in un flusso di **Bit**.
    
2. **Livello 2 (Data Link):** I bit vengono raggruppati in un **Frame**.
    
    - Il dispositivo controlla l'**Indirizzo MAC di destinazione**. Se è il suo (o un broadcast), procede.
        
    - Controlla il CRC (errori). Se è integro, "scarta" l'intestazione e la coda del Frame (L2) e passa il contenuto al livello superiore.
        
3. **Livello 3 (Network):** Ora abbiamo in mano il **Pacchetto IP**.
    
    - Il sistema controlla l'**Indirizzo IP di destinazione**.
        
    - Se il pacchetto è destinato proprio a questa macchina, il sistema guarda il campo **"Protocol"** nell'header IP (es. 6 per TCP, 17 per UDP) per sapere a chi consegnarlo sopra.
        
    - "Scarta" l'header IP.
        
4. **Livello 4 (Trasporto):** Quello che resta è il **Segmento** (TCP o UDP). Qui vengono controllate le **Porte** (es. porta 80, 443) per consegnare i dati all'applicazione corretta (Livello 7).
    

---

## 2. Flusso in Discesa (Invio): Dall'Applicazione al Cavo

Questo è il processo di **Incapsulamento**. Immagina di inviare un messaggio.

1. **Livello 4 (Trasporto):** L'applicazione genera i dati. Il Livello 4 aggiunge l'header (TCP o UDP) creando il **Segmento**. Qui si definiscono le porte sorgente e destinazione.
    
2. **Livello 3 (Network):** Il Segmento scende al Livello 3. Qui viene aggiunto l'header IP (quello che abbiamo studiato prima). Ora abbiamo il **Pacchetto**.
    
    - Viene inserito l'IP del destinatario.
        
    - Viene impostato il TTL.
        
3. **Livello 2 (Data Link):** Il Pacchetto scende al Livello 2. Viene "impacchettato" in un **Frame**.
    
    - Viene aggiunto l'**Indirizzo MAC** della scheda di rete locale (Sorgente) e quello del prossimo salto (Destinazione, solitamente il router).
        
    - Viene calcolato il CRC (controllo errore).
        
4. **Livello 1 (Fisico):** Il Frame viene convertito in una sequenza di impulsi elettrici o luminosi e sparato sul mezzo trasmissivo.
    

---

## 3. Cosa fa il Router nel mezzo? (Il "Passaggio Orizzontale")

Il router riceve il frame, ma **non arriva al Livello 4**. Fa questo:

- **Riceve** (L1 -> L2 -> L3).
    
- Arrivato al **Livello 3**, guarda l'IP, consulta la tabella di routing, decrementa il TTL.
    
- **NON sale al Livello 4**.
    
- **Riscende** immediatamente (L3 -> L2 -> L1) su un'altra interfaccia.
    

> **Nota Universitaria:** Il router scarta il "vecchio" frame di Livello 2 e ne crea uno **completamente nuovo** per il prossimo salto. L'header IP invece viaggia quasi identico (cambia solo il TTL e il Checksum).

---

### Riassunto della "Cipolla" (Encapsulation)

- **L4 (Segmento):** "A quale porta/app devo consegnare?"
    
- **L3 (Pacchetto):** "A quale indirizzo IP (Host) devo arrivare?"
    
- **L2 (Frame):** "A quale indirizzo fisico (Interfaccia) devo saltare ora?"

## Link 
1) 