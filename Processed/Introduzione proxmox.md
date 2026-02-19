---
tipo: nota_lezione
corso: Proxmox
tags:
  - progetto
  - proxmox
  - Completed
  - Linux
creato: 2026-02-19 09:53
---

# 📝 Lezione: Introduzione proxmox
**Corso:** [[Proxmox]]

---
## Contenuto
### 1. Definizione Architetturale
Proxmox VE è una soluzione di virtualizzazione di classe enterprise **"Bare Metal"** basata su **Debian GNU/Linux**. È definita come piattaforma _iperconvergente_ (HCI - Hyper-Converged Infrastructure) perché integra in un unico stack software tre elementi che solitamente sono separati: **Calcolo (Virtualizzazione)**, **Storage (Software-Defined Storage)** e **Rete**.

### 2. Le due tecnologie di virtualizzazione (Il "Cuore")
A differenza di altri hypervisor, Proxmox offre una flessibilità duale:
- **KVM (Kernel-based Virtual Machine):** È un modulo del kernel Linux che trasforma il sistema in un hypervisor di Tipo 1. Permette la virtualizzazione completa (Hardware-assisted). Ogni VM ha il proprio hardware virtuale e il proprio kernel.
    - _Utilizzo:_ OS diversi da Linux (Windows, BSD) o quando è necessario un isolamento totale.
- **LXC (Linux Containers):** Una tecnologia di virtualizzazione a livello di sistema operativo. I container condividono il kernel dell'host ma mantengono file system e processi isolati.
    - _Utilizzo:_ Microservizi, applicazioni Linux leggere. Offre prestazioni quasi identiche al "fisico" con un overhead minimo.

### 3. Software-Defined Storage (SDS) e File System
La gestione del dato è l'aspetto più profondo di Proxmox. Supporta tecnologie avanzate per garantire integrità e performance:
- **ZFS:** Un file system combinato con un gestore di volumi logici. Offre protezione contro la corruzione dei dati, compressione in tempo reale e **Snapshot** istantanei.
- **Ceph:** È il fiore all'occhiello per i cluster. È uno storage distribuito che replica i dati su più server fisici. Se un server si rompe, i dati sono al sicuro sugli altri, permettendo la continuità operativa senza storage centralizzati costosi (come le SAN).
- **Thin Provisioning:** Capacità di allocare spazio virtuale superiore a quello fisico disponibile, ottimizzando le risorse.

### 4. Networking e Sicurezza
Proxmox utilizza i bridge Linux standard, ma permette configurazioni complesse:
- **Open vSwitch:** Per una gestione avanzata dei flussi di rete.
- **VLAN e Bonding:** Per aggregare più schede di rete (ridondanza/velocità) e segmentare il traffico.
- **Firewall Distribuito:** Proxmox include un firewall integrato basato su _netfilter_ che può essere configurato a livello di Cluster, di singolo Nodo o di singola VM/Container.

### 5. Alta Affidabilità e Cluster (High Availability)
In una configurazione a più nodi (minimo 3 per il quorum ideale), Proxmox gestisce il **Cluster Manager (pmxcfs)**:
- **Live Migration:** Spostamento di una VM accesa da un server all'altro senza interruzione del servizio (zero downtime).
- **Fencing:** Meccanismo di sicurezza che isola un nodo malfunzionante per prevenire la corruzione dei dati.
- **Proxmox Backup Server (PBS):** Un ecosistema separato (ma perfettamente integrato) che permette backup dedisegnati e crittografati, riducendo drasticamente il tempo di salvataggio grazie alla deduplicazione.

### 6. Aspetti Gestionali (Management)
- **Interfaccia Web (API-First):** Tutto ciò che vedi nell'interfaccia grafica è gestito tramite API REST. Questo permette automazioni spinte tramite script o strumenti come **Terraform** e **Ansible**.
- **RBAC (Role-Based Access Control):** Gestione granulare degli utenti. Puoi decidere chi può accendere una VM, chi può vederla e chi può gestirne il backup.

---
## Collegamenti
- Torna al corso: [[Proxmox]]