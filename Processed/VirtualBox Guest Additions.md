---
tipo: nota_lezione
corso: "Dashboard Udemy morroLinux Linux"
tags: [progetto, Linux, Udemy, morroLinux, certificazioni, Completed]
creato: 2026-03-18 23:10
---

# 📝 Lezione: VirtualBox Guest Additions
**Corso:** [[Dashboard Udemy morroLinux Linux]]

---
## Contenuto
## Cosa sono le VirtualBox Guest Additions?
Le **Guest Additions** sono un pacchetto di software e driver che vengono installati **dentro** il sistema operativo ospite (Guest). Servono a ottimizzare le prestazioni e a permettere un'integrazione fluida tra Host e Guest.
> **Importante:** A differenza del pacchetto "Extension Pack" (che si installa sull'Host), le Guest Additions si installano singolarmente su ogni macchina virtuale.

##  Funzionalità Principali

Senza questi driver, la tua VM Linux girerà in modo "limitato". Ecco cosa sbloccano:
- **Integrazione del mouse:** Il puntatore non rimane "intrappolato" dentro la finestra della VM; puoi spostarlo liberamente tra desktop fisico e virtuale.
- **Cartelle Condivise (Shared Folders):** Permettono di scambiare file tra il tuo PC (es. Windows) e la VM Linux come se fosse un disco locale o un mount di rete.
- **Video Acceleration:** Supporto per la risoluzione dinamica (se ridimensioni la finestra di VirtualBox, la risoluzione di Linux cambia automaticamente) e accelerazione 3D.
- **Appunti Condivisi (Shared Clipboard):** Copia e incolla di testo e file tra Host e Guest (e viceversa).
- **Trascina e rilascia (Drag and Drop):** Spostamento fisico di file trascinandoli con il mouse.
- **Sincronizzazione Oraria:** La VM mantiene l'ora esatta sincronizzandosi costantemente con l'Host.

##  Procedura di Installazione su Linux (Lato Terminale)
Per l'esame LPI è fondamentale sapere che le Guest Additions non sono un semplice `.exe`, ma spesso richiedono la compilazione di moduli del kernel.
## 1. Preparazione del sistema
Prima di installarle, servono i tool di compilazione e gli header del kernel:
- **Su Debian/Ubuntu:** `sudo apt install build-essential dkms linux-headers-$(uname -r)`
- **Su Red Hat/Fedora:** `sudo dnf install kernel-devel kernel-headers make gcc dkms`
## 2. Montaggio del "Disco" virtuale
VirtualBox fornisce le Guest Additions sotto forma di un file immagine `.iso`.
1. Dal menu della finestra VM: **Dispositivi** -> **Inserisci l'immagine del CD delle Guest Additions**.
2. Nel terminale Linux, monta il CD (solitamente in `/media/cdrom` o `/mnt`).
## 3. Esecuzione dello script
Bisogna eseguire lo script di installazione con privilegi di root:

```
sudo sh /media/cdrom/VBoxLinuxAdditions.run
```
Dopo l'installazione, è sempre necessario un **reboot** per caricare i nuovi driver nel kernel.
## Cartelle Condivise e Permessi (Punto Critico LPI)
Una volta installate le Guest Additions, per accedere alle cartelle condivise su Linux, il tuo utente deve far parte di un gruppo specifico.
Se provi ad accedere a una cartella condivisa e ricevi "Permesso negato", devi aggiungere il tuo utente al gruppo **vboxsf**:

```
sudo usermod -aG vboxsf nome_utente
```
_(Ricorda: dopo questo comando devi disconnetterti e rientrare affinché i permessi siano attivi)._

## 📝 Riepilogo per lo studio
- **Dove si installano?** Solo nel Guest.
- **Cosa servono?** Performance video, mouse, cartelle condivise, clipboard.
- **Requisito Linux:** Kernel headers e compilatore (gcc/make).
- **Gruppo utente:** `vboxsf`.

---
## Collegamenti
- Torna al corso: [[Dashboard Udemy morroLinux Linux]]