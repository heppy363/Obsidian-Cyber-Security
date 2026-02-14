---
aliases:
  - Completate
tags:
  - Completed
  - CompTIAnetwork
  - Certificati
  - protocollo
---
--- 
## Nozioni
`Il protocollo **ARP (Address Resolution Protocol)** è il "collante" fondamentale dell'intera suite di protocolli Internet. Senza di esso, la comunicazione nelle reti locali si fermerebbe istantaneamente.`

### 1. Perché l'ARP è necessario?
Immagina che il tuo computer voglia inviare un messaggio a un altro PC nella stessa rete.
- Il tuo computer conosce l'**Indirizzo IP** del destinatario (Livello 3).
- Tuttavia, lo switch e la scheda di rete (Livello 2) non capiscono gli IP; loro sanno consegnare dati solo usando gli **Indirizzi MAC**.
L'ARP serve a rispondere alla domanda: _"Chi ha l'indirizzo IP 192.168.1.5? Per favore, dimmi il tuo indirizzo MAC"_.
### 2. Il Funzionamento (Il processo Request/Reply)
Il processo ARP avviene in quattro fasi rapide:
1. **ARP Cache Check:** Prima di inviare qualsiasi cosa, il PC controlla la sua **ARP Cache** (una tabella temporanea in RAM). Se l'abbinamento IP-MAC è già lì, lo usa e finisce qui.
2. **ARP Request (Broadcast):** Se l'indirizzo non è in cache, il mittente crea un pacchetto ARP Request. Poiché non sa chi sia il destinatario, invia il frame all'indirizzo MAC di broadcast: `FF:FF:FF:FF:FF:FF`. **Tutti** nella rete leggono questo messaggio.
3. **ARP Reply (Unicast):** Tutti i PC ricevono la richiesta, ma solo quello che ha l'IP cercato risponde. Gli altri scartano il pacchetto. Il destinatario risponde con un ARP Reply inviato in **Unicast** (direttamente al mittente), includendo il proprio indirizzo MAC fisico.
4. **Updating Cache:** Il mittente riceve la risposta, scrive l'abbinamento nella sua tabella ARP e finalmente può incapsulare il pacchetto IP nel frame Ethernet e inviarlo.
### 3. La Struttura del Pacchetto ARP
Il pacchetto ARP è "incastrato" direttamente dentro un frame Ethernet (non usa IP, è un'alternativa a IP all'interno del frame).

|Campo|Descrizione|
|---|---|
|**Hardware Type**|Tipo di rete (solitamente Ethernet = 1).|
|**Protocol Type**|Tipo di protocollo (solitamente IPv4 = 0x0800).|
|**Operation (Opcode)**|Specifica se è una **Request** (1) o una **Reply** (2).|
|**Sender MAC / IP**|Gli indirizzi di chi invia.|
|**Target MAC / IP**|Gli indirizzi di chi deve ricevere (nella Request, il Target MAC è 00:00:00...).|

### 4. Situazioni Particolari
#### Gratuitous ARP
È un messaggio ARP che un dispositivo invia senza che nessuno glielo abbia chiesto. Serve a:
- Annunciare il proprio MAC dopo l'accensione.
- Verificare che non ci siano **conflitti di indirizzi IP** (se qualcuno risponde al mio stesso IP, c'è un errore).
#### Proxy ARP
Accade quando un **Router** risponde a una richiesta ARP per conto di un altro dispositivo che si trova su una rete diversa. Il router "finge" di essere il destinatario per permettere al traffico di passare attraverso di lui.
### 5. La Sicurezza: ARP Spoofing (o Poisoning)
L'ARP è un protocollo "basato sulla fiducia". Non c'è alcun controllo che verifichi se chi risponde sia veramente chi dice di essere.
- Un hacker può inviare costantemente ARP Reply false dicendo: _"L'indirizzo IP del Router è associato al MIO indirizzo MAC"_.
- Il tuo PC crederà all'hacker e gli invierà tutto il traffico (attacco **Man-in-the-Middle**).

### 6. Comandi Pratici
 `arp -a` Vedrai la lista di tutti gli indirizzi IP e i relativi MAC che il tuo computer ha imparato recentemente.

``` Bash
arp -a

Interfaccia: 192.168.178.166 --- 0x5
  Indirizzo Internet    Indirizzo fisico      Tipo
  192.168.178.1         2c-91-ab-5b-89-0f     dinamico
  192.168.178.100       f4-a9-97-45-dd-bd     dinamico
  192.168.178.107       2c-f0-5d-2a-89-a6     dinamico
  192.168.178.126       c8-08-e9-51-4e-71     dinamico
  192.168.178.159       7e-95-8b-9d-63-9e     dinamico
  192.168.178.165       20-be-b8-92-1d-20     dinamico
  192.168.178.255       ff-ff-ff-ff-ff-ff     statico
  224.0.0.2             01-00-5e-00-00-02     statico
  224.0.0.22            01-00-5e-00-00-16     statico
  224.0.0.251           01-00-5e-00-00-fb     statico
  224.0.0.252           01-00-5e-00-00-fc     statico
  239.255.255.250       01-00-5e-7f-ff-fa     statico
  255.255.255.255       ff-ff-ff-ff-ff-ff     statico
```


## Link 
1) 