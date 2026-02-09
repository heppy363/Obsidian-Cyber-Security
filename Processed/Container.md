---
aliases:
  - Completate
tags:
  - Completed
  - proxmox
  - H-net
---
--- 
`Parlare di container oggi significa descrivere il pilastro fondamentale del cloud computing moderno. Per definirli in modo completo a livello informatico, non possiamo limitarci a dire che sono "macchine virtuali più leggere"; dobbiamo analizzare la loro architettura e come interagiscono con il sistema operativo.`
## Nozioni
## 1. Definizione Tecnica: L'Unità di Standardizzazione
Un container è un'unità standard di software che pacchettiza il **codice** e tutte le sue **dipendenze** (librerie, file di configurazione, runtime) affinché l'applicazione venga eseguita in modo rapido e affidabile da un ambiente informatico all'altro.

A differenza della virtualizzazione tradizionale, i container non includono una copia del sistema operativo (OS). Invece, condividono il **Kernel** dell'host con altri container.
## 2. I Pilastri Tecnologici (Sotto il Cofano)
A livello di kernel Linux, un container non è un "oggetto" magico, ma il risultato di tre tecnologie principali che isolano il processo:
- **Namespaces:** È la tecnologia che crea l'isolamento. Garantisce che ogni container veda solo le proprie risorse (processi, interfacce di rete, mount point) come se fosse l'unico sistema attivo.
- **Control Groups (cgroups):** Gestiscono l'allocazione delle risorse. Impediscono a un singolo container di consumare tutta la RAM o la CPU del server host, garantendo la stabilità.
- **Union File Systems (UnionFS):** Permette di creare il file system del container stratificando diversi livelli (layers). Questo rende i container estremamente leggeri e veloci da avviare.
## 3. L'Ecosistema: Immagini e Runtime
Per capire i container, bisogna distinguere tra l'oggetto statico e quello dinamico:

| Componente            | Descrizione                                                                                           |
| --------------------- | ----------------------------------------------------------------------------------------------------- |
| **Container Image**   | Un pacchetto statico, immutabile e in sola lettura che contiene tutto il necessario per l'esecuzione. |
| **Container Runtime** | Il software (come Docker o containerd) che legge l'immagine e la "trasforma" in un container attivo.  |
| **Container**         | L'istanza eseguibile di un'immagine. È il processo isolato vero e proprio.                            |
## 4. Perché sono rivoluzionari?
La completezza della descrizione passa per i vantaggi operativi che offrono rispetto alle VM (Virtual Machines):
- **Portabilità assoluta:** "Funziona sul mio PC, funzionerà sul server". Poiché l'ambiente è sigillato nell'immagine, si eliminano i conflitti di versione tra sviluppo e produzione.
- **Efficienza:** Avviandosi in pochi millisecondi e consumando pochissima memoria rispetto a una VM, permettono una densità di applicazioni molto più alta sullo stesso hardware.
- **Microservizi:** Sono lo strumento perfetto per l'architettura a microservizi, dove ogni funzione di un'app (database, login, checkout) vive nel proprio container indipendente.

## 5. L'ultimo tassello: L'Orchestrazione
Quando i container diventano centinaia o migliaia, gestirli a mano è impossibile. Qui entra in gioco l'**orchestrazione** (il cui standard di fatto è **Kubernetes**). L'orchestratore si occupa di:
1. **Auto-healing:** Se un container crasha, lo riavvia.
2. **Scaling:** Se c'è troppo traffico, crea nuove istanze del container.
3. **Load Balancing:** Distribuisce il traffico equamente tra i container.
> **Nota di approfondimento:** Ricorda che i container sono per natura **effimeri**. Se un container viene cancellato, i dati al suo interno vanno persi a meno di non collegare dei volumi esterni (Persistence).

## Link 
1) 