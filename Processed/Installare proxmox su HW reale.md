---
tipo: nota_lezione
corso: "Dashboard sistemi operativi"
tags: [progetto, sistemiOperativi, progettiPersonali, Completed]
creato: 2026-02-20 18:47
---

# 📝 Lezione: Installare proxmox su HW reale
**Corso:** [[Dashboard sistemi operativi]]

---
## Contenuto
### 1. Preparazione della Chiavetta Proxmox
Scarica l'ultima versione di **Proxmox VE ISO** dal sito ufficiale.
- **Usa Rufus:** Come abbiamo fatto per Ubuntu, usa la modalità **DD**.
- **Schema Partizione:** GPT.
- **Target:** UEFI.

### 2. Configurazione BIOS (Fondamentale per la Virtualizzazione)
Senza queste opzioni attive, Proxmox non potrà lanciare le macchine virtuali. Entra nel BIOS (**DEL**) e verifica:
- **Advanced > CPU Configuration:**
    - **Intel Virtualization Technology (VT-x):** Enabled.
    - **Intel VT-d:** Enabled.
- **Advanced > PCI Configuration:**
    - **SR-IOV:** Enabled (utile se vorrai passare la GTX 1050 direttamente a una VM).
### 3. L'Installazione di Proxmox
Inserisci la chiavetta e premi **F11** al boot per selezionarla (modalità UEFI).
1. **Target Hard Disk:** Seleziona l'**SSD SanDisk**. Clicca su "Options" e assicurati che il file system sia **ext4** (più semplice) o **ZFS** (se vuoi protezione avanzata dai dati corrotti, ma consuma più RAM).
2. **Management Network:** Seleziona la porta LAN che ha internet (`eno1`).
3. **Hostname:** Dai un nome al server (es. `server-luc.local`).
4. **IP Address:** Imposta un IP statico (es. `192.168.1.100`). **Segnatelo**, perché dopo l'installazione il server non avrà interfaccia grafica e potrai usarlo solo via browser da un altro PC.
5. Da stare attenti con il driver della scheda video puo dare probblmi 
### 4. Primo Accesso al Pannello di Controllo

Una volta finita l'installazione, scollega la chiavetta e riavvia. Lo schermo del server mostrerà una riga di comando nera con un indirizzo simile a: `https://192.168.1.100:8006`
- Vai su un altro PC (o smartphone) collegato alla stessa rete.
- Digita l'indirizzo nel browser.
- **Username:** `root`
- **Password:** Quella che hai scelto durante l'installazione.
### 5. Ottimizzazione Post-Installazione (Il tocco finale)
Appena entri, Proxmox ti darà un errore di "No Subscription". È normale. Per poter aggiornare il sistema senza pagare la licenza enterprise, apri la **Shell** di Proxmox nel browser e scrivi:


```
# Disabilita il repository enterprise e abilita quello gratuito
sed -i 's/pve-enterprise/pve-no-subscription/g' /etc/apt/sources.list.d/pve-enterprise.list
apt update && apt dist-upgrade -y
```

---
## Collegamenti
- Torna al corso: [[Dashboard sistemi operativi]]