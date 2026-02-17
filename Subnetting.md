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
### 1. Perché si fa il Subnetting?
A livello universitario, devi sapere che il subnetting non serve solo a fare ordine, ma risolve problemi tecnici enormi:
- **Riduzione del traffico di Broadcast:** Ogni rete ha un traffico di servizio (es. ARP) che arriva a tutti. Se avessimo una rete gigante con 10.000 PC, il traffico di broadcast la saturerebbe. Dividendo in sottoreti, il broadcast rimane confinato.
- **Sicurezza:** Puoi isolare i reparti (es. la sottorete "Amministrazione" non può parlare con la sottorete "Ospiti" senza passare da un router/firewall).
- **Risparmio di indirizzi:** Permette di non sprecare indirizzi IP pubblici, che sono limitati e costosi.
### 2. Gli attrezzi del mestiere: Indirizzo IP e Maschera
Il router non vede l'indirizzo IP come lo vediamo noi (`192.168.1.10`), ma come una stringa di **32 bit**.
- **L'Indirizzo IP:** Identifica il dispositivo.
- **La Subnet Mask:** È una sequenza di bit "1" seguiti da bit "0". I bit a "1" dicono al router: _"Guarda, questi bit dell'indirizzo IP rappresentano il nome della strada (Rete)"_. I bit a "0" dicono: _"Questi sono il numero civico (Host)"_.
### 3. Come funziona il calcolo (L'operazione di AND)
Quando un pacchetto deve essere inoltrato, il router esegue un'operazione logica chiamata **AND binario** tra l'IP di destinazione e la maschera.
- Se il risultato dell'operazione è uguale all'indirizzo della rete locale, il pacchetto resta nella LAN.
- Se è diverso, il router capisce che deve mandarlo all'esterno (Default Gateway).
### 4. La notazione CIDR (quella con lo "slash")
Oggi non si usano quasi più le vecchie "Classi" (A, B, C), ma la notazione **CIDR (Classless Inter-Domain Routing)**.
- `/24` significa che i primi 24 bit (su 32) sono dedicati alla rete.
- Esempio: `255.255.255.0` in binario ha 24 "uno", quindi è una `/24`.
### 5. Esempio di Subnetting Universitario
Supponiamo di avere la rete `192.168.1.0/24`. Abbiamo 256 indirizzi disponibili. Se vogliamo dividerla in due sottoreti più piccole, "rubiamo" un bit alla parte host e passiamo a una `/25`:
- **Sottorete 1:** da `192.168.1.0` a `192.168.1.127` (Maschera `255.255.255.128`)
- **Sottorete 2:** da `192.168.1.128` a `192.168.1.255` (Maschera `255.255.255.128`)
- [[]]
> **Regola d'oro per l'esame:** In ogni sottorete perdi sempre **due indirizzi**:
> 1. Il primo (es. `.0`): Indirizzo della **Rete** stessa.
> 2. L'ultimo (es. `.127`): Indirizzo di **Broadcast**.


## Link 
1) 