---
tipo: nota_lezione
corso: "Dashboard Udemy morroLinux Linux"
tags: [progetto, Linux, Udemy, morroLinux, certificazioni, Completed]
creato: 2026-03-25 23:12
---

# 📝 Lezione: FAT 32
**Corso:** [[Dashboard Udemy morroLinux Linux]]

---
## Contenuto
## Perché FAT32 è ancora ovunque?
Sebbene limitato rispetto a _ext4_ o _XFS_, FAT32 (File Allocation Table 32) è lo standard universale per l'interoperabilità.

## 1. Il ruolo cruciale: La Partizione EFI (ESP)
Nelle moderne architetture **UEFI**, il firmware della scheda madre non è in grado di leggere file system complessi come NTFS o ext4 nelle fasi iniziali.
- **Lo standard:** UEFI specifica che la partizione di boot (**ESP - EFI System Partition**) deve essere formattata in **FAT32**.
- **Contenuto:** Qui risiedono i file `.efi` (come il bootloader GRUB) che il firmware carica per avviare Linux.

## 2. Caratteristiche e Limiti Tecnici
Per l'esame, ricorda questi numeri e vincoli:
- **Dimensione massima del file:** **4 GB**. Se provi a scaricare un'immagine ISO di un DVD (es. 4.7 GB) su una chiavetta FAT32, l'operazione fallirà.
- **Dimensione massima della partizione:** Tecnicamente fino a 2 TB (con settori da 512 byte) o 8 TB.
- **Permessi POSIX:** **Inesistenti**. FAT32 non supporta i permessi Linux (`chmod`, `chown`). Quando monti una partizione FAT32 su Linux, tutti i file sembreranno appartenere all'utente che l'ha montata.
- **Frammentazione:** Non essendo un file system "intelligente", soffre molto di frammentazione rispetto ai file system moderni di Linux.

## 3. Gestione da Terminale Linux
Per lavorare con FAT32 su Linux (ad esempio per preparare una chiavetta di boot o una partizione EFI), si usano i seguenti comandi:
- **Creazione:** `mkfs.vfat -F 32 /dev/sdX1` (Il flag `-F 32` forza il formato a 32-bit).
- **Verifica/Riparazione:** `fsck.vfat /dev/sdX1` (Equivalente del vecchio _chkdsk_ di Windows).
- **Identificazione:** `blkid` ti mostrerà il `TYPE="vfat"`.

## Tabella Comparativa Rapida

|Caratteristica|FAT32 (vfat)|ext4 (Linux Default)|
|---|---|---|
|**Max File Size**|4 GB|16 TB|
|**Journaling**|No (Rischio corruzione se salta la corrente)|Sì (Recupero rapido dai crash)|
|**Permessi**|No|Sì (Owner, Group, Others)|
|**Uso Principale**|EFI Boot, USB Keys, SD Card|OS Linux, Server, Dati|


> **Nota per** Ricorda che in `/etc/fstab`, FAT32 viene identificato con il modulo **`vfat`**.

---
## Collegamenti
- Torna al corso: [[Dashboard Udemy morroLinux Linux]]