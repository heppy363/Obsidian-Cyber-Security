---
tipo: nota_lezione
corso: "Dashboard Udemy morroLinux Linux"
tags: [progetto, Linux, Udemy, morroLinux, certificazioni, Completed]
creato: 2026-03-30 22:01
---

# 📝 Lezione: Cambio di runlevel System V init
**Corso:** [[Dashboard Udemy morroLinux Linux]]

---
## Contenuto

### 1. Il vecchio mondo: `/etc/inittab` (SysVinit)
In questo file si definisce il comportamento del sistema. La sintassi è `id:runlevels:action:process`.
- **id**: Un nome breve (es. `id` per l'init default, `tty1` per il terminale).
- **runlevels**: I livelli in cui l'azione è attiva (es. `345`).
- **action**:
    - `initdefault`: Imposta il runlevel all'avvio.
    - `respawn`: Se il processo muore, riavvialo (tipico delle login console).
    - `wait`: Avvia e aspetta che finisca prima di procedere.
    - `once`: Avvialo una sola volta all'entrata nel livello.
    - `ctrlaltdel`: Definisce cosa succede premendo la combinazione di tasti.

### 2. Cambiare Runlevel "al volo"
Hai mostrato tre modi per farlo, tutti validi per l'esame:
1. **`telinit [0-6]`**: Il comando standard per dire a `init` di cambiare stato.
2. **`init [0-6]`**: Spesso un alias o un link a telinit.
3. **`systemctl isolate [target]`**: Il modo moderno per Systemd (es. `systemctl isolate multi-user.target`).

**Verifica:**
- `runlevel`: Mostra `[Precedente] [Attuale]`. Se vedi `N 5`, non c'è stato un cambio da quando il sistema è acceso.
- `who -r`: Un'alternativa più dettagliata per vedere l'orario del cambio.

### 3. Gli Script di Avvio (`/etc/init.d/` e `rcX.d`)
Questa è la parte dove molti studenti si confondono, ma la tua spiegazione sui link simbolici è chiarissima:
- **`/etc/init.d/`**: Contiene gli script reali (es. lo script per avviare SSH).
- **`/etc/rc[0-6].d/`**: Contiene i link simbolici che puntano a `/etc/init.d/`.
    - **S** (Start): Avvia il servizio.
    - **K** (Kill): Ferma il servizio.
    - **Numero (00-99)**: L'ordine di priorità. `S01` parte prima di `S99`.

### 4. Tool di Gestione (LPI Exam Essentials)
Per non creare i link a mano (rischioso!), si usano questi strumenti:
- **`chkconfig`** (Tipico di RedHat/CentOS vecchi):
    - `chkconfig --list`: Vedi tutti i servizi e i loro stati nei runlevel.
    - `chkconfig --level 35 httpd on`: Abilita il server web nei livelli 3 e 5.
- **`update-rc.d`** (Tipico di Debian/Ubuntu vecchi):
    - `update-rc.d ssh defaults`: Crea i link standard.
- **`ntsysv` / `sysv-rc-conf`**: Interfacce grafiche "ncurses" (quelle blu che hai mostrato).
- **`systemctl`** (Il presente):
    - `systemctl enable/disable [servizio]`: Per decidere se deve partire al boot.


---
### Analisi dei Log e Parametri (Extra)
Hai citato un file fondamentale: **`/proc/cmdline`**. È una "miniera d'oro" per l'esame: leggendolo puoi vedere esattamente quali parametri sono stati passati dal Bootloader (GRUB) al Kernel al momento dell'avvio (inclusi i parametri di rete o il runlevel forzato).

---
## Collegamenti
- Torna al corso: [[Dashboard Udemy morroLinux Linux]]