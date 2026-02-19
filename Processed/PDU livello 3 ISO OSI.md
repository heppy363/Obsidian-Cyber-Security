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
### Anatomia dell'Header IPv4 (La PDU di Livello 3)

Un header IPv4 standard ha una dimensione variabile, ma tipicamente è di **20 byte**. È composto da diversi campi critici:

|Campo|Lunghezza (Bit)|Funzione Specifica|
|---|---|---|
|**Version**|4|Indica se è IPv4 (0100) o IPv6 (0110).|
|**IHL (Header Length)**|4|Indica quanto è lungo l'header (necessario perché esistono i campi "Options").|
|**Type of Service (ToS)**|8|Serve per la Qualità del Servizio (QoS). Indica la priorità del pacchetto (es. voce su IP vs download file).|
|**Total Length**|16|La dimensione totale del pacchetto (Header + Dati) in byte. Max 65.535 byte.|
|**Identification**|16|Un numero univoco per identificare il pacchetto. Fondamentale per la **frammentazione**.|
|**Flags**|3|Controllano la frammentazione (es. "Don't Fragment" o "More Fragments").|
|**Fragment Offset**|13|Se il pacchetto è stato spezzettato, indica la posizione di questo frammento rispetto all'originale.|
|**TTL (Time to Live)**|8|**Cruciale.** Un contatore (salti) che decresce a ogni router. Evita che i pacchetti girino all'infinito se c'è un loop. Quando arriva a 0, il pacchetto viene scartato.|
|**Protocol**|8|Indica quale protocollo del Livello 4 si trova nel payload (es. 6 per TCP, 17 per UDP).|
|**Header Checksum**|16|Controllo degli errori, ma **solo per l'header**. Se l'header è corrotto, il router lo scarta.|
|**Source Address**|32|L'indirizzo IP di chi invia (il mittente).|
|**Destination Address**|32|L'indirizzo IP di chi deve ricevere (il destinatario).|
|**Options**|Variabile|Usato raramente per test, sicurezza o routing specifico.|

Esporta in Fogli

---

### Caratteristiche Principali del Datagramma

1. **Indipendenza dalla tecnologia sottostante:** Il pacchetto IP è incapsulato dentro i Frame del Livello 2 (Ethernet, Wi-Fi, ecc.). Quando cambia il mezzo (es. passi dal Wi-Fi al cavo), l'header di Livello 2 viene distrutto e rifatto, ma il **Pacchetto di Livello 3 rimane intatto** da sorgente a destinazione.
    
2. **Best-Effort:** Nota che nell'header non c'è nulla che garantisca la ricezione o l'ordine dei pacchetti. Se un pacchetto si perde, l'IP non lo sa.
    
3. **Il ruolo del TTL:** È la "sicurezza" della rete. Senza il TTL, un errore di configurazione in un router potrebbe far girare miliardi di pacchetti fantasma per sempre, intasando i cavi mondiali.
    

---

### Differenza rapida con IPv6

Se studi l'IPv6, noterai che l'header è molto più snello:

- È lungo **40 byte** fissi.
    
- Gli indirizzi sono da **128 bit**.
    
- Hanno rimosso il Checksum (perché i livelli 2 e 4 lo fanno già, e i router guadagnano velocità non dovendo ricalcolarlo).
    
- Non c'è frammentazione fatta dai router: la fanno solo gli host finali.
    

---

### Concetto Universitario: L'Incapsulamento

Per visualizzare la PDU nel suo contesto, ricorda questa "matrioska": `[ Header Ethernet (L2) [ Header IP (L3) [ Header TCP/UDP (L4) [ Dati Applicazione ] ] ] Trailer L2 ]`

Il router apre la busta esterna (L2), guarda l'Header IP (L3), decide dove mandarlo, e richiude il pacchetto in una nuova busta L2 adatta al prossimo salto.

## Link 
1) 