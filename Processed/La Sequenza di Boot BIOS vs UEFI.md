---
tipo: nota_lezione
corso: "Dashboard Udemy morroLinux Linux"
tags: [progetto, Linux, Udemy, morroLinux, certificazioni, Completed]
creato: 2026-03-25 23:08
---

# 📝 Lezione: La Sequenza di Boot BIOS vs UEFI
**Corso:** [[Dashboard Udemy morroLinux Linux]]

---
## Contenuto
## Architettura Legacy (BIOS/MBR)
1. **POST (Power-On Self Test):** Controllo hardware iniziale.
2. **MBR (Master Boot Record):** Il BIOS legge i primi **512 byte** del disco.
3. **Stage 1:** Il codice nell'MBR (molto piccolo) serve solo a puntare allo stage successivo.
4. **Stage 2:** Carica il Bootloader vero e proprio (es. GRUB Legacy o LILO), che poi avvia il Kernel.
5. **Chainloading:** Tecnica usata da GRUB per passare il controllo al bootloader di Windows (visto che GRUB non può avviare direttamente il kernel NT).
## Architettura Moderna (UEFI/GPT)
- **ESP (EFI System Partition):** Non usa più i settori "nascosti" come l'MBR, ma una partizione dedicata [[FAT 32]] che contiene file `.efi`.
- **Shell EFI:** UEFI è un mini-sistema operativo con driver e shell propria.
- **Secure Boot:** Funzionalità per avviare solo kernel firmati digitalmente.

## 2. Kernel e Initrd/Initramfs
Una volta che il Bootloader (GRUB) ha preso il controllo, carica due cose in RAM:
1. **Vmlinuz:** Il file del Kernel compresso.
2. **Initrd / Initramfs (Initial RAM Filesystem):**
    - È un filesystem temporaneo in RAM.
    - Contiene i **moduli (driver)** necessari per montare il vero filesystem `root` (es. driver per dischi RAID, LVM o file system ext4/xfs).
    - Senza questo, il kernel andrebbe in _Kernel Panic_ perché non saprebbe come "leggere" il resto del disco.
## 3. Il processo Init (PID 1)
Il kernel, finito il suo compito, lancia il primo processo dell'utente: `/sbin/init`.
- **SysVinit:** Il sistema classico basato su script sequenziali.
- **Upstart:** (Usato in vecchie Ubuntu) Introdotto il concetto di **Jobs** (event-based).
- **Systemd:** Lo standard attuale. `/sbin/init` è un link simbolico a systemd. Usa le **Units** (`.service`, `.target`, `.mount`).
> **Trucco per l'esame:** Se il sistema non parte, puoi passare al bootloader il parametro `init=/bin/sh` per ottenere una shell di emergenza saltando tutta la sequenza di init.

## 4. Tabella dei Runlevel (SysVinit)
Anche se **systemd** usa i "Targets", l'esame LPI richiede ancora la conoscenza dei runlevel classici:
- il ranlevel predefinito dei server e quello **3**
- [[approfondimento runlevel]]

|Livello|Nome / Stato|Descrizione|
|---|---|---|
|**0**|**Halt**|Spegnimento del sistema.|
|**1 / S**|**Single User**|Modalità manutenzione (solo root, no rete).|
|**2**|**Multiuser**|Multiutente, ma senza rete (raro).|
|**3**|**Full Multiuser**|Modalità testuale completa con rete (Standard per i Server).|
|**4**|**Unused**|Definibile dall'utente.|
|**5**|**X11**|Come il 3, ma con interfaccia grafica (Standard Desktop).|
|**6**|**Reboot**|Riavvio del sistema.|

![[Pasted image 20260325232156.png]]
- Come si nota tra BIOS e UEFi cambia radicalmente l'approccio anche a livello di codice in uno si usa assembly mentre nel altro abbiamo direttamente delle chiamata di "Funzioni" 


---
## Collegamenti
- Torna al corso: [[Dashboard Udemy morroLinux Linux]]