---
tipo: nota_lezione
corso: "Dashboard Udemy morroLinux Linux"
tags: [progetto, Linux, Udemy, morroLinux, certificazioni, Completed]
creato: 2026-03-19 22:37
---

# 📝 Lezione: File collegati a proc
**Corso:** [[Dashboard Udemy morroLinux Linux]]

---
## Contenuto
## Comunicazione Hardware-Memoria: I/O Ports e DMA
Mentre gli **Interrupt** servono all'hardware per "chiamare" la CPU, le **I/O Ports** e il **DMA** servono per il passaggio dei dati vero e proprio.
## 1. I/O Ports (`/proc/ioports`)
Ogni dispositivo hardware (scheda video, tastiera, controller disco) ha bisogno di un "indirizzo" per scambiare comandi e dati con la CPU.
- **Cos'è:** Immagina le I/O Ports come delle "caselle postali" numerate nella memoria.
- **Il File:** `/proc/ioports` elenca i **range di indirizzi esadecimali** riservati a ogni periferica.
- **Conflitti:** Due dispositivi non possono mai occupare lo stesso range di porte. Se accade, il sistema va in crash o la periferica non viene rilevata (un problema comune nei vecchi PC, oggi gestito automaticamente dal protocollo _Plug and Play_).

## 2. DMA - Direct Memory Access (`/proc/dma`)
Questa è la tecnologia che salva le prestazioni del tuo computer.
- **Il Problema (PIO):** Senza DMA, la CPU dovrebbe leggere ogni singolo byte dal disco e scriverlo nella RAM (modalità chiamata _Programmed I/O_). Questo renderebbe il PC lentissimo durante il trasferimento di grandi file.
- **La Soluzione (DMA):** Il controller DMA permette a una periferica (es. una scheda audio o un hard disk) di scrivere o leggere dati **direttamente nella RAM**, saltando completamente il passaggio attraverso la CPU.
- **Il Vantaggio:** La CPU "istruisce" il dispositivo su cosa fare (_"Copia questo file dal disco alla RAM"_) e poi torna a occuparsi d'altro. Quando il trasferimento è finito, il dispositivo invia un **Interrupt** per dire: _"Ehi CPU, ho finito!"_.

---
## Collegamenti
- Torna al corso: [[Dashboard Udemy morroLinux Linux]]