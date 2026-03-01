---
tipo: nota_lezione
corso: "Dashboard H-NET"
tags: [progetto, hNet, Completed]
creato: 2026-02-28 23:09
---

# 📝 Lezione: installare VPN su proxmox versione 1.0
**Corso:** [[Dashboard H-NET]]

---
## Contenuto
Abbiamo scelto Tailscale per la sua filosofia "installa e dimentica", basata sul protocollo open source **WireGuard**.

#### **2.1 Installazione su Proxmox**

Il comando utilizzato per scaricare e configurare il repository ufficiale:
```
curl -fsSL https://tailscale.com/install.sh | sh
```

#### **2.2 Attivazione del Tunnel**
Per collegare il server alla tua rete privata:
1. Lancia il comando: `tailscale up`
2. Clicca sul link generato nel terminale per autenticarti con il tuo account Google.
3. Verifica l'IP assegnato (nel tuo caso: **100.100.65.11**): `tailscale ip -4`

### Sezione 3: Risoluzione problemi Dispositivi Mobili
Se l'app sul telefono mostra "Not Connected" o non permette di cliccare sui pulsanti fuori dal Wi-Fi:
1. **Permessi Dati:** Assicurarsi che l'app Tailscale abbia il permesso "Dati Cellulare" attivo nelle impostazioni dello smartphone.
2. **Configurazione VPN:** Consentire al sistema operativo di creare il profilo VPN quando richiesto dall'app.
3. **Risparmio Energetico:** Disattivare le ottimizzazioni batteria per Tailscale per evitare che il tunnel venga chiuso in background.

### 👥 Sezione 4: Condivisione con Amici (Luc, Martina, ecc.)
Per permettere ad altri utenti Linux di accedere senza dare loro le tue credenziali:
1. **Dalla Dashboard Web:** Vai su [Tailscale Admin](https://login.tailscale.com/admin/machines), clicca sui tre puntini `...` accanto al server `pve` e seleziona **Share**.
2. **Link di Invito:** Genera il link e invialo.
3. **Lato Amico (Linux):**
    - Installa Tailscale: `curl -fsSL https://tailscale.com/install.sh | sh`
    - Effettua il login: `sudo tailscale up`
    - Clicca sul link di invito per accettare la condivisione.
4. **Accesso finale:** L'amico aprirà il browser su `https://100.100.65.11:8006`.
---
## Collegamenti
- Torna al corso: [[Dashboard H-NET]]