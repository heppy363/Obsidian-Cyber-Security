---
aliases:
  - Completate
tags:
  - Completed
  - H-net
---
--- 
## Nozioni
### 1. Configurazione del Bridge su Proxmox (VLAN Aware)
Di default, Proxmox crea un bridge standard (`vmbr0`) che si comporta come uno switch non gestito. Dobbiamo attivare l'intelligenza.
- **Accedi a Proxmox** (VLAN 10, porta 8006).
- Vai su **System > Network**.
- Modifica `vmbr0` (o il bridge principale):
    - Assicurati che sia associato alla porta fisica corretta (es. `eno1`).
    - **Fondamentale:** Spunta la casella **"VLAN Aware"**.
    - Applica le impostazioni e riavvia la rete (o il nodo).
**Cosa succede ora?** Grazie a questa spunta, Proxmox smetterà di ignorare le etichette (tag) 802.1Q e permetterà a pfSense di gestire le VLAN direttamente attraverso quel bridge.
### 2. Configurazione delle VM e dei Container (LXC)
Ora che il bridge è "intelligente", assegnare una macchina a una rete specifica è semplicissimo. Non devi più configurare le VLAN dentro ogni singola VM, lo fai dall'interfaccia di Proxmox:
- **Mini PC 1 (Reverse Proxy):** Nelle impostazioni **Network** della VM, imposta il **VLAN Tag** a `20`. Ora quella VM vive solo nella DMZ.
- **Mini PC 2 (Gitea):** Imposta il **VLAN Tag** a `30`. Ora il servizio è isolato nella rete sviluppo.
- **PC Personale (Admin):** Se crei una VM per i tuoi test personali, imposta il tag a `10`.
### 3. Il setup sullo switch Netgear GS116E
Mentre Proxmox è pronto, lo switch deve essere configurato in modo speculare. Nelle specifiche del tuo GS116E, abbiamo visto che supporta perfettamente lo standard **802.1Q**.
- **Porta Trunk (es. Porta 16):** Deve essere impostata come **Tagged (T)** per le VLAN 10, 20, 30, 40. Questo è il "canale" dove Proxmox e pfSense parlano con lo switch.
- **Porte Access:** Se colleghi un dispositivo che non gestisce le VLAN (come il tuo PC fisso), imposta la porta come **Untagged (U)** sulla VLAN 10.
### 4. Gestione dello Storage (NAS)
Dato che entrambi i mini PC devono vedere il NAS (VLAN 40) per i backup e i dati S3:
1. In Proxmox, vai su **Datacenter > Storage**.
2. Aggiungi un target **NFS** o **SMB**.
3. Usa l'IP del NAS che hai definito in pfSense (es. `10.0.40.10`).
4. Grazie alla **capacità di switching di 32 Gbps** del GS116E, Proxmox potrà fare il backup delle VM a piena velocità senza che il tuo sito web (VLAN 20) ne risenta.
### Perché questo software è perfetto per il tuo hardware?
Il **GS116E** ha una tabella degli indirizzi MAC da **8.000 voci**. Questo è vitale con Proxmox: ogni VM e ogni Container che crei ha il suo indirizzo MAC virtuale. Uno switch economico andrebbe in crisi ("dimenticando" dove sono i pacchetti), mentre il tuo Netgear gestirà migliaia di dispositivi virtuali senza battere ciglio.



## Link 
1) 