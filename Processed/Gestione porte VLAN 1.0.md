---
aliases:
  - Completate
tags:
  - Completed
  - VLAN
  - H-net
---
--- 
## Nozioni
### 1. Il concetto di "VLAN Trunk" verso Proxmox
Dato che su un singolo mini PC (Nodo Proxmox) farai girare servizi diversi (ad esempio, sul Mini PC 1 potresti avere il Reverse Proxy in una VM e un altro servizio di test in un'altra), la porta dello switch deve diventare un **Trunk**.
- **Configurazione Netgear:** La porta fisica dove colleghi il Mini PC non sarà più "Untagged", ma **"Tagged"** per le VLAN che quel nodo deve gestire.
- **Proxmox Bridge:** All'interno di Proxmox, creerai un `Linux Bridge` (vmbr0) impostato come **VLAN aware**. Questo permette a Proxmox di smistare i pacchetti taggati dallo switch direttamente alle VM corrette.
### 2. Analisi delle Porte Proxmox (Livello Gestione)
Oltre alle porte dei servizi che abbiamo già analizzato, dobbiamo aggiungere le porte per la gestione del cluster:
- **Porta 8006 (Web GUI):** Questa è la porta per accedere al pannello di controllo di Proxmox. Deve essere accessibile solo dalla **VLAN 10 (I Re)**.
- **Porta 22 (SSH):** Per la gestione profonda dei nodi.
- **Porta 5405/UDP e 5404/UDP (Corosync):** Se in futuro deciderai di unire i due mini PC in un "Cluster" per l'alta affidabilità (HA), queste porte serviranno ai due nodi per parlarsi costantemente.
### 3. Distribuzione Carichi e Backup sul NAS
Dato che userai un NAS con bucket S3 e probabilmente anche spazio disco per le VM:
- **Porta 2049 (NFS) o 445 (SMB):** Proxmox la userà per collegarsi al NAS (VLAN 40) per salvare i backup delle VM o le ISO dei sistemi operativi.
- **Ottimizzazione Switch:** Lo switch GS116E, grazie alla sua **capacità di switching di 32 Gbps**, gestirà senza problemi il traffico pesante durante i backup notturni delle VM sul NAS, senza disturbare il traffico internet del tuo blog.

| **Servizio**         | **Porta** | **Destinazione**    | **Accesso**            |
| -------------------- | --------- | ------------------- | ---------------------- |
| **Pannello Proxmox** | 8006      | Mini PC 1 & 2       | Solo VLAN 10 / VPN     |
| **Gitea (LXC/VM)**   | 3000      | Mini PC 2 (VLAN 30) | VPN -> Reverse Proxy   |
| **Backup VM**        | NFS/SMB   | NAS (VLAN 40)       | Interno (VLAN 30/40)   |
| **Storage S3**       | 9000      | NAS (VLAN 40)       | VM Pubbliche e Private |

## Link 
1) 