---
tipo: nota_lezione
corso: "Dashboard H-NET"
tags: [progetto, hNet, Completed]
creato: 2026-03-22 15:59
---

# 📝 Configurazione e creazione Utenti
**Corso:** [[Dashboard H-NET]]

---
## Contenuto
## Fase 1: Creazione degli Utenti (Il "Chi")
Invece di usare l'utente di sistema (`pam`), creiamo utenti specifici per Proxmox per una sicurezza totale.
1. Vai su **Datacenter** > **Permissions** > **Users**.
2. Clicca su **Add**:
    - **User name**: `Dome` (e poi ripeti per `Andre`).
    - **Realm**: Seleziona **Proxmox VE authentication server** (`pve`).
    - **Password**: Imposta una password sicura.
3. **Crea il Gruppo**: Vai su **Groups** > **Create**. Chiamalo `Amici`.
4. **Aggiungi utenti al gruppo**: Torna su **Users**, seleziona Dome (e Andre), clicca **Edit** e aggiungili al gruppo `Amici`.

## Fase 2: Creazione dei "Recinti" (I Pool)
La Pool è lo spazio privato dove ogni amico comanda senza vedere le macchine degli altri.
1. Vai su **Datacenter** > **Permissions** > **Pools**.
2. Clicca su **Create**:
    - ID: `Pool_Dome`
    - ID: `Pool_Andre`

## Fase 3: Assegnazione dei Permessi (Il "Cosa")
Questa è la parte più delicata. Dobbiamo dare i permessi in modo "chirurgico".
## A. Permessi Privati (Sulla Pool)
Ogni utente deve essere il capo del suo spazio.
- Vai su **Datacenter** > **Permissions** > **Add** > **Pool Permission**.
    - **Pool**: `Pool_Dome` | **User**: `Dome@pve` | **Role**: `Administrator`.
    - **Pool**: `Pool_Andre` | **User**: `Andre@pve` | **Role**: `Administrator`.

## B. Permessi Comuni (Sul Gruppo Amici)
Per evitare di ripetere tutto per ogni utente, usiamo il gruppo `Amici` per le risorse condivise.
- **Per i Dischi**: Add > Group Permission | Path: `/storage/local-lvm` | Group: `@Amici` | Role: `PVEDatastoreAdmin`.
- **Per le ISO**: Add > Group Permission | Path: `/storage/local` | Group: `@Amici` | Role: `PVEDatastoreUser`.
- **Per la Rete (Fondamentale)**: Add > Group Permission | Path: `/nodes` | Group: `@Amici` | Role: `PVEVMUser`.

## Fase 4: Sblocco della Creazione VM (Il "Come")
Per permettere loro di cliccare "Finish" senza errori di permessi (403):
1. **Permesso di Allocazione**: Vai su **Add** > **Group Permission**.
    - **Path**: `/vms` (scrivilo a mano).
    - **Group**: `@Amici`.
    - **Role**: `PVEVMAdmin` (o un ruolo custom con `VM.Allocate`).
    - **Propagate**: `true`.

## Fase 5: Regole d'Oro per gli Utenti
Perché tutto funzioni senza che ti chiamino ogni 5 minuti, i tuoi amici devono seguire queste regole quando creano una macchina:
1. **Selezionare la Pool**: Nel primo tab della creazione (**General**), devono obbligatoriamente selezionare la loro pool (`Pool_Dome` o `Pool_Andre`) dal menu a tendina.
2. **Scegliere lo Storage**: Nel tab **Disks**, devono assicurarsi di selezionare lo storage dove hanno i permessi (`local-lvm`).
3. **Login**: Al momento dell'accesso, devono selezionare **Proxmox VE authentication server** come Realm.

## Sicurezza e VPN (Tailscale)
- I tuoi amici si collegano tramite l'IP Tailscale del tuo server: `https://[IP-TAILSCALE]:8006`.
- Non serve aprire porte sul router.
- Tramite le **ACL di Tailscale** (opzionale), puoi decidere che i loro PC possano parlare _solo_ con l'IP di Proxmox e non con gli altri tuoi dispositivi di casa.

---
## Collegamenti
- Torna al corso: [[Dashboard H-NET]]
- [[Aggiunta di utenti per server di calcolo 1]]
