---
aliases:
  - Completate
tags:
  - Completed
  - claud
---
--- 
## Nozioni

## 1. Cos'è Hyper-V?
Hyper-V è la tecnologia di virtualizzazione di Microsoft che permette di creare e gestire **Macchine Virtuali (VM)**. A differenza degli hypervisor di tipo 2 (come VirtualBox o VMware Workstation che girano sopra un OS), Hyper-V viene _caricato subito dopo il boot_, prendendo il controllo del processore e della memoria.

Anche se lo vedi dentro Windows, tecnicamente è Windows stesso che gira "sopra" Hyper-V in una partizione speciale.
## 2. L'Architettura: Partizioni e VMBus
Hyper-V si basa sul concetto di **Partizioni**, che sono unità logiche di isolamento:
- **Parent Partition (Root):** È la partizione principale che gestisce l'intero sistema. Contiene lo stack di gestione (Hyper-V Manager) e i driver dei dispositivi hardware. È qui che gira il tuo Windows "principale".
- **Child Partitions:** Sono le VM dove installi i Guest OS (Linux, Windows Server, ecc.). Non hanno accesso diretto all'hardware.

### Come comunicano? (VMBus)
Invece di emulare ogni singolo pezzo di hardware (che è lento), Hyper-V usa il **VMBus**. È un canale di comunicazione ad alta velocità che permette alle "Child Partitions" di inviare richieste di I/O (disco, rete) direttamente alla "Parent Partition" in modo estremamente efficiente.

## 3. Tecnologie Chiave alla Base
Hyper-V non è un software isolato, ma sfrutta specifiche istruzioni del processore e del sistema:
- **Intel VT-x / AMD-V:** Senza queste estensioni hardware nel processore, Hyper-V non può funzionare. Servono per gestire l'isolamento dei ring della CPU.
- **SLAT (Second Level Address Translation):** Una tecnologia (chiamata EPT da Intel e RVI da AMD) che aiuta a mappare la memoria della VM sulla RAM fisica senza sovraccaricare la CPU.
- **VHDX:** Il formato di file per i dischi virtuali. Supporta fino a 64TB, è resiliente alla corruzione dei dati in caso di sbalzi di corrente e ottimizza le prestazioni su dischi moderni.

## 4. Integrazione ed Ecosistema
Hyper-V non serve solo a far girare "Windows dentro Windows". La sua integrazione è profonda:
- **Windows Containers:** Ricordi i [[Processed/Container]] di cui parlavamo prima? Su Windows, puoi far girare i container in **Hyper-V Isolation mode**. Ogni container riceve il proprio kernel dedicato (molto più sicuro ma leggermente più pesante).
- **WSL2 (Windows Subsystem for Linux):** Se usi Linux su Windows 10/11, sappi che dietro le quinte c'è un'istanza "lightweight" di Hyper-V che fa girare il kernel Linux originale.
- **Azure:** L'intero cloud di Microsoft (Azure) è basato su una versione custom e iper-scalabile di Hyper-V. Imparare Hyper-V significa capire come funziona il cloud di Microsoft.
	- 

## 5. Funzionalità Avanzate per IT Pro
Se lo usi in ambito server, Hyper-V offre strumenti di classe Enterprise:
- **Live Migration:** Spostare una VM accesa da un server fisico a un altro senza un secondo di downtime (zero pacchetti persi).
- **Dynamic Memory:** La RAM viene tolta o aggiunta alla VM in tempo reale in base al carico di lavoro.
- **Checkpoint (Snapshot):** Salvare lo stato della macchina per tornarci in caso di errore (utilissimo prima di aggiornamenti rischiosi).

### Hyper-V vs Container: Un riepilogo rapido
Per chiudere il cerchio con la tua domanda precedente:
- **Hyper-V:** Virtualizza l'**Hardware**. Isola interi sistemi operativi. Ideale per sicurezza massima e sistemi legacy.
- **Container:** Virtualizzano l'**OS**. Isolano singole applicazioni. Ideale per velocità, portabilità e microservizi.

## Link 
1) 