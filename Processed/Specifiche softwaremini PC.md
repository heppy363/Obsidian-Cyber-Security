---
aliases:
  - Completate
tags:
  - Completed
  - H-net
---
--- 
## Nozioni
## 1. Installazione e Base Sistema (Proxmox VE)
Su entrambi i mini PC installerai Proxmox. Questo ti permette di astrarre l'hardware: se un servizio ha bisogno di più potenza, puoi spostarlo da un mini PC all'altro senza cambiare cavi.
- **File System:** Usa **ZFS** se i mini PC hanno dischi SSD di buona qualità; offre protezione dai dati corrotti e snapshot istantanee.
- **Networking (Il Bridge):** Devi configurare il bridge di rete (`vmbr0`) come **VLAN Aware**. Senza questa spunta, Proxmox non capirebbe i "tag" provenienti dal tuo switch Netgear.
- **Storage Esterno:** Collegherai Proxmox al tuo NAS tramite protocollo **NFS o iSCSI** per archiviare i backup e le ISO dei sistemi operativi.
## 2. Configurazione dei Servizi (VM vs Container)
Dovrai decidere come distribuire i software che hai menzionato:
### Mini PC 1 (La Porta sull'Esterno)
- **VM Reverse Proxy (Nginx Proxy Manager/Traefik):** Sarà l'unica macchina nella **VLAN 20 (DMZ)**. Riceve il traffico web e lo smista.
- **LXC Container (Sito Web/Blog):** Usare un container (LXC) qui è ideale perché è leggerissimo e isolato.
### Mini PC 2 (Sviluppo e Risorse Private)
- **LXC Gitea:** Lo terrai nella **VLAN 30 (Sviluppo)**. Essendo un servizio interno, non avrà accesso diretto da internet.
- **LXC Media Server (Plex/Jellyfin):** Questo container avrà bisogno di accedere al NAS (VLAN 40) per i film e la musica.
    - _Nota:_ Qui entra in gioco l'**IGMP Snooping** del tuo GS116E per gestire il traffico multicast dei media senza intasare la rete.
## 3. Gestione e Manutenzione
Per far sì che tutto giri come un orologio, userai questi strumenti software:
- **Proxmox Backup Server (PBS):** Potresti installarlo come VM per gestire i backup incrementali sul tuo NAS.
- **Portainer (Opzionale):** Se decidi di usare Docker dentro le VM di Proxmox, Portainer ti dà un'interfaccia grafica facile per gestire i tuoi container.
- **Monitoraggio (Port 8006):** Accederai alle dashboard di Proxmox solo dalla **VLAN 10 (I Re)** o tramite la **VPN di pfSense**.
## 4. Perché lo switch GS116E è fondamentale qui?
Mentre i tuoi mini PC fanno "girare" tutto questo software, lo switch Netgear lavora nell'ombra:
1. **VLAN Tagging (802.1Q):** Permette a una singola scheda di rete del mini PC di trasportare il traffico di 10 diverse VM su VLAN diverse.
2. **Performance:** Con una capacità di switching di **32 Gbps**, lo switch assicura che il backup di una VM su Proxmox non rallenti il caricamento del tuo sito web o il tuo lavoro su Gitea.
3. **Affidabilità:** Essendo **fanless** e in **metallo**, può gestire il carico costante di due nodi Proxmox senza surriscaldarsi, garantendo la continuità dei tuoi servizi.

## Link 
1) 