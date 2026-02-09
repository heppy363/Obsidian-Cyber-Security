---
aliases:
  - Completate
tags:
  - Completed
  - claud
  - risorsePersonali
---
--- 
`Per capire il cloud di Microsoft, non devi immaginarlo solo come un insieme di server, ma come una **piattaforma globale distribuita** che trasforma l'hardware fisico in risorse virtuali astratte, disponibili su richiesta.`
## Nozioni

## 1. L'Infrastruttura Fisica: Regioni e Zone
Azure non è un unico "posto". È una rete globale di data center:
- **Regioni:** Un'area geografica (es. "Italy North" a Milano) che contiene uno o più data center.
- **Availability Zones (AZ):** All'interno di una regione, sono data center fisicamente separati con alimentazione, raffreddamento e rete indipendenti. Servono per la **High Availability**: se un fulmine colpisce un data center, la tua app continua a girare nell'altro.

## 2. Il Cervello: L'Azure Fabric Controller
Ti sei mai chiesto come faccia Azure a creare una VM in 30 secondi solo perché hai cliccato un tasto? Dietro le quinte c'è il **Fabric Controller**. È un sistema distribuito (un "kernel del cloud") che:
1. Gestisce migliaia di server che eseguono una versione custom di **Hyper-V**.
2. Monitora lo stato di salute dei server.
3. Alloca le risorse: decide lui su quale server fisico piazzare la tua VM in base alla RAM e CPU disponibili.

## 3. I Modelli di Servizio (La Piramide del Cloud)
Microsoft descrive Azure attraverso tre modalità principali di consumo, a seconda di quanto controllo vuoi mantenere:
- **IaaS (Infrastructure as a Service):** È il "ferro" virtuale. Affitti VM (tramite Hyper-V), dischi e reti. Tu gestisci l'OS e gli aggiornamenti.
- **PaaS (Platform as a Service):** Qui non vedi più il server. Carichi solo il tuo codice (es. in un container o un'app web) e Microsoft gestisce l'OS, il runtime e le patch.
- **SaaS (Software as a Service):** Il prodotto finito. Esempi classici sono **Microsoft 365** o **Teams**. Tu usi solo il software.

## 4. Tecnologie Distintive: Perchè Azure è diverso?
Microsoft ha integrato il suo ecosistema storico nel cloud in modo unico:

### A. Azure Active Directory (ora Microsoft Entra ID)
È il cuore dell'identità. Se un'azienda usa Windows in ufficio, usa Active Directory. Azure permette di estendere quella stessa identità nel cloud, permettendo il **Single Sign-On (SSO)**: la stessa password che usi per il PC dell'ufficio serve per accedere alle tue risorse cloud.
### B. Azure Arc: Il Cloud Ibrido
Questa è una tecnologia geniale. Microsoft sa che non tutte le aziende possono spostare tutto sul cloud. **Azure Arc** permette di gestire server che si trovano fisicamente nel _tuo_ ufficio o su altri cloud (come AWS) come se fossero dentro Azure, usando lo stesso pannello di controllo.
### C. Serverless (Azure Functions)
È l'evoluzione estrema. Non paghi per un server acceso, ma paghi solo per i **millisecondi** in cui il tuo codice viene eseguito in risposta a un evento (es. qualcuno carica una foto, il codice si attiva per ridimensionarla e poi si spegne).

## 5. La Sicurezza: Il Modello di Responsabilità Condivisa
Nel cloud di Microsoft vige una regola d'oro:
> Microsoft è responsabile della sicurezza **del** Cloud (data center, hardware, hypervisor). Tu sei responsabile della sicurezza **nel** Cloud (configurazione delle VM, dati, password).

### In sintesi: Perchè è così potente?
Azure vince perché permette a un'azienda che usa già Windows Server, SQL Server e .NET di spostarsi online con una compatibilità quasi del 100%, sfruttando **Hyper-V** come linguaggio comune tra il server locale e il cloud globale.

## Link 
1) 