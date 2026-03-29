---
tipo: nota_lezione
corso: "Dashboard Udemy morroLinux Linux"
tags: [progetto, Linux, Udemy, morroLinux, certificazioni, Completed]
creato: 2026-03-26 22:53
---

# 📝 Lezione: Runleavel e diagnostica al boot
**Corso:** [[Dashboard Udemy morroLinux Linux]]

---
## Contenuto
## 1. Intervenire su GRUB (Modifiche al volo)

Quando premi `e` (edit) nel menu di GRUB, puoi modificare la riga che inizia con `linux` (o `kernel` sui sistemi vecchi):
- **Single User Mode:** Aggiungi `1`, `s`, oppure `single` alla fine della riga. Carica il sistema con solo il terminale root (richiede password root su molte distro).
	- [[approfondimento runlevel]]
- **Emergenza estrema:** `init=/bin/sh`. Questo non avvia il sistema di init (systemd), ma ti dà direttamente una shell root **senza chiedere password**. Utile per resettare la password di root dimenticata, ma ricorda che il filesystem sarà in sola lettura (usa `mount -o remount,rw /` per scrivere).
- **Specificare il Target:** Puoi scrivere direttamente il numero del runlevel (es. `3` o `5`) per ignorare il default.
## 2. Gestione Target con Systemd (Il nuovo standard)
Come hai notato, `/etc/inittab` è ormai un "fantasma". Ora comanda `systemctl`:
- **Vedere il default:** `systemctl get-default`
- **Cambiare il default:** `systemctl set-default multi-user.target` (equivale al runlevel 3).
- **Cambiare "ora":** `systemctl isolate graphical.target` (equivale al vecchio comando `init 5`).
- **Analisi dei link:** I runlevel classici esistono ancora come link simbolici in `/lib/systemd/system/runlevelX.target`.

## 3. Troubleshooting e Log (Dove guardare?)
Quando qualcosa non va, Linux scrive tutto nei "registri". Ecco la gerarchia da ricordare per l'LPI:
1. **`dmesg`**: Mostra il **buffer del kernel**. Fondamentale per vedere se l'hardware (USB, webcam, dischi) viene riconosciuto. Se colleghi qualcosa e non succede nulla, digita `dmesg | tail`.
2. **`/var/log/boot.log`**: Contiene i messaggi visualizzati _durante_ l'avvio (quelli con i vari `[ OK ]` o `[ FAILED ]`).
3. **`/var/log/messages`** (o `/var/log/syslog` su Debian/Ubuntu): Il log generico del sistema. Se un demone (es. Apache o SSH) fallisce, la risposta è qui.
4. **`journalctl`**: Lo strumento moderno per leggere i log di systemd.
    - `journalctl -b`: Log dell'ultimo boot.
    - `journalctl -u ssh`: Solo i log del servizio SSH.
    - `journalctl -f`: Segue i log in tempo reale (come `tail -f`).

## Esercizio di consolidamento per te
Visto che hai parlato di **`tail`** e **`head`**, ricorda che per l'esame è fondamentale sapere come estrarre parti specifiche di un file.
- _Esempio:_ Come faresti a vedere solo le righe dalla 10 alla 20 di `/var/log/messages` usando una combinazione di questi comandi?

_(Suggerimento: usa `head -n 20` e passa il risultato a `tail` via pipe `|`)_.

---
## Collegamenti
- Torna al corso: [[Dashboard Udemy morroLinux Linux]]