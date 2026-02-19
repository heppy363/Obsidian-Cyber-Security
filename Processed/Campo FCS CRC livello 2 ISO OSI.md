---
tipo: nota_lezione
corso: "Dashboard CompTIA Network+"
tags: [progetto, CompTIANetwork, certificazioni, Completed]
creato: 2026-02-19 15:39
---

# 📝 Lezione: Campo FCS CRC livello 2 ISO OSI
**Corso:** [[Dashboard CompTIA Network+]]

---
## Contenuto
`Si tratta di una divisione polinomiale`
**Importante** il CRC e il prodotto della divisione polinomiale mentre il FCS si tratta del campo nella quale viene inserito questo valore. 

### Funzionamento 
Tutto il processo di funzionamento lo si deve vedere in ambito del ricevente e de mittente:
- **In Trasmissione (Mittente):**
    - La scheda di rete prende tutti i bit del frame (Payload + Indirizzi + Ethertype).
    - Applica una formula matematica (un polinomio generatore standard).
    - Il **resto** di questa divisione è il codice **CRC** (solitamente a 32 bit).
    - Questo resto viene scritto nel campo **FCS** alla fine del frame e inviato sul cavo.
- **In Ricezione (Destinatario):**
    - Quando il frame arriva, la scheda di rete ricevente esegue lo **stesso identico calcolo** matematico su tutti i bit ricevuti.
    - Confronta il suo risultato con quello scritto dal mittente nel campo FCS.
    - **Se i risultati coincidono:** Il frame è integro. Viene accettato e passato al Livello 3 (IP).
    - **Se i risultati NON coincidono:** Significa che anche un solo bit è cambiato durante il viaggio (a causa di interferenze elettriche o cavi difettosi). **Il frame viene scartato silenziosamente.**


### Funzionamento matematico
Tutto il funzionamento e basato su una divisione polinomiale, della somma dei bit della PDU che assume valore $M_(x)$ diviso $G_(x)$ ovvero un numero a 32 bit definita da uno standard che tutte e due le macchine devono conosce e parlare, il resto di questa divisione polinomiale sara il nostro 'CRC' quindi il valore di controllo del errore, questo valore verra inserito dentro il campo FRS. questo procedimento si basa sullo _XOR_ esclusivo e deve essere ripetuto per _ogni_ fraim del messaggio da inviare: 
- [[Funzionamento matematica calcolo CRC]]

---
## Collegamenti
- Torna al corso: [[Dashboard CompTIA Network+]]