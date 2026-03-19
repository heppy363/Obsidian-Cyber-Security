---
tipo: nota_lezione
corso: "Dashboard Udemy morroLinux Linux"
tags: [progetto, Linux, Udemy, morroLinux, certificazioni, Completed]
creato: 2026-03-19 22:23
---

# 📝 Lezione: Gli interrupts in linux
**Corso:** [[Dashboard Udemy morroLinux Linux]]

---
## Contenuto

## La Gestione degli Interrupt in Linux
Un **Interrupt (IRQ - Interrupt Request)** è un segnale inviato dall'hardware alla CPU per richiedere attenzione immediata. Quando la CPU riceve un interrupt, sospende temporaneamente l'esecuzione del processo corrente per gestire l'evento hardware (es. un clic del mouse o l'arrivo di un pacchetto di rete).
## 1. Il File `/proc/interrupts`
In Linux, tutto è un file. Il file `/proc/interrupts` non risiede sul disco rigido, ma è un'interfaccia "volatile" direttamente nel Kernel.
- **Dinamicità:** Viene generato in tempo reale.
- **Persistenza:** Essendo memorizzato nella RAM dal Kernel, tutti i contatori vengono **azzerati al riavvio** del sistema.

## 2. Struttura del File (Come leggerlo)
Se digiti `cat /proc/interrupts` nel terminale, vedrai una tabella simile a questa:

|Colonna|Significato|
|---|---|
|**IRQ ID**|Il numero identificativo dell'interrupt (es. 0, 1, 9).|
|**CPU0, CPU1...**|Il **contatore**: quante volte quell'interrupt è stato gestito da ogni specifico core della CPU.|
|**Type**|Il tipo di interrupt (es. `Edge`, `Level`, `MSI`).|
|**Device**|Il nome del dispositivo che ha generato l'interrupt (es. `timer`, `keyboard`, `eth0`).|

## 3. Concetti Avanzati per LPI
Per superare l'esame, tieni a mente questi tre aspetti della gestione delle periferiche:
#### A. Differenza tra Interrupt e Polling
- **Interrupt:** L'hardware "bussa" alla CPU solo quando serve (efficiente).
- **Polling:** La CPU controlla costantemente se l'hardware ha novità (dispendioso in termini di risorse). Linux predilige quasi sempre gli interrupt.


## Tabella Comparativa per l'esame

|Risorsa|File in `/proc`|Funzione Principale|Ruolo della CPU|
|---|---|---|---|
|**Interrupts**|`/proc/interrupts`|Segnalazione eventi|**Attiva**: gestisce la richiesta subito.|
|**I/O Ports**|`/proc/ioports`|Indirizzi di comunicazione|**Attiva**: invia comandi agli indirizzi.|
|**DMA**|`/proc/dma`|Trasferimento dati massivo|**Passiva**: viene solo avvisata alla fine.|

#### C. Softirqs
Se vedi molti interrupt gestiti in modo asincrono, si parla di **Softirqs** (interrupt software). Linux li usa per gestire compiti che non devono bloccare immediatamente la CPU ma che sono comunque prioritari (come il traffico di rete pesante).


> **Tip Pratico:** Prova a dare il comando `watch -n 1 cat /proc/interrupts`. Muovi il mouse o digita sulla tastiera: vedrai i numeri nelle colonne delle CPU aumentare in tempo reale!


---
## Collegamenti
- Torna al corso: [[Dashboard Udemy morroLinux Linux]]
- [[File collegati a proc]]