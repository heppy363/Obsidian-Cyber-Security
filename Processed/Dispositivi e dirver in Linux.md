---
tipo: nota_lezione
corso: "Dashboard Udemy morroLinux Linux"
tags: [progetto, Linux, Udemy, morroLinux, certificazioni, Completed]
creato: 2026-03-19 22:39
---

# 📝 Lezione: Dispositivi e dirver in Linux
**Corso:** [[Dashboard Udemy morroLinux Linux]]

---
## Contenuto
## Gestione Periferiche: Cold Plug vs Hot Plug
Il kernel Linux gestisce i dispositivi in base alla loro capacità di essere collegati a sistema avviato.
- **Cold Plug:** Dispositivi che richiedono lo spegnimento del sistema per essere collegati/scollegati (es. vecchi dischi IDE, RAM, CPU). Il Kernel li rileva solo durante la fase di boot.
- **Hot Plug:** Dispositivi che possono essere inseriti o rimossi a computer acceso (es. USB, Thunderbolt, dischi SATA configurati correttamente). Il Kernel riceve un segnale (evento) e carica il driver al volo.
## Visualizzazione: Il comando `lspci`
Per vedere i dispositivi collegati al bus PCI:
- `lspci`: Elenco lineare dei dispositivi.
- `lspci -t`: Visualizzazione **ad albero (tree)**, che mostra le relazioni gerarchiche tra i controller e i dispositivi.

## 📂 I File System Virtuali: `/dev` e `/sys`
Dal Kernel 2.6 in poi, la gestione dei dispositivi è diventata dinamica grazie a strumenti come **udev**.
## 1. `/dev` (Device Files)
I file in questa cartella rappresentano l'interfaccia verso l'hardware.
- **Dinamicità:** Se colleghi una penna USB, appare `/dev/sdb1`; se la scolleghi, il file scompare.
- **Nomenclatura:** Ad esempio, `/dev/sda` rappresenta il primo disco rigido.

## 2. `/sys` (sysfs)
Mentre `/dev` serve per _usare_ il dispositivo, `/sys` serve per _conoscerne le proprietà_.
- È un file system virtuale che espone la struttura del Kernel all'utente (anche non root, in sola lettura).
- Contiene **link simbolici** organizzati per gerarchia (bus, classi, dispositivi).
- **Esempio:** Puoi vedere lo stato della batteria o la velocità della ventola leggendo i file dentro `/sys`.

## 🛠️ Gestione dei Moduli (Driver)
In Linux, i driver sono chiamati **moduli del kernel** (`.ko`). Possono essere caricati e rimossi senza riavviare.
## Comandi Fondamentali

|Comando|Funzione|Note|
|---|---|---|
|`lsmod`|Elenca i moduli attualmente caricati.|Legge le info da `/proc/modules`.|
|`insmod`|Carica un modulo.|Richiede il **percorso completo** (es. `insmod /lib/modules/.../driver.ko`).|
|`rmmod`|Rimuove un modulo.|Fallisce se il modulo è usato da un altro processo.|
|**`modprobe`**|Il tool "intelligente" (Best Practice).|Risolve automaticamente le **dipendenze**.|


## Perché usare `modprobe`?
A differenza di `insmod`, `modprobe` è consapevole delle dipendenze. Se il "Driver A" ha bisogno del "Driver B" per funzionare:
- `modprobe DriverA`: Carica sia B che A.
- `modprobe -r DriverA`: Rimuove il modulo (equivale a `rmmod`).
    
## Pillola per l'Esame: Moduli e Dipendenze
Perché `modprobe` sappia quali moduli dipendono da altri, legge un file chiamato `modules.dep`. Se installi un nuovo modulo manualmente, devi aggiornare questo database con il comando:

```
sudo depmod -a
```

> **Curiosità:** Hai menzionato che `/sys` è usato da software non-root. Esatto! Molti tool di monitoraggio (come quelli per la temperatura) leggono `/sys` proprio perché non hanno bisogno di permessi speciali per consultare le proprietà dell'hardware.

---
## Collegamenti
- Torna al corso: [[Dashboard Udemy morroLinux Linux]]