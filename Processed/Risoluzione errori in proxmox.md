---
tipo: nota_lezione
corso: "Dashboard H-NET"
tags: [progetto, hNet, Completed]
creato: 2026-02-23 21:33
---

# 📝 Lezione: Risoluzione errori in proxmox
**Corso:** [[Dashboard H-NET]]

---
## Contenuto
#### **1. Superamento del blocco video (Schermo Nero)**
- **Problema:** Una volta avviata la chiavetta, lo schermo diventava nero impedendo di vedere l'installer.
- **Intervento:** È stata modificata la riga di comando di avvio di Proxmox premendo il tasto **`e`** nel menu principale.
- **Soluzione:** È stato aggiunto il parametro **`nomodeset`** alla riga del kernel. Questo ha disattivato i driver video avanzati, forzando l'uso della grafica base del chip integrato Supermicro e permettendo la visualizzazione dell'interfaccia di installazione.
#### **2. Configurazione dei parametri di rete**
- **Scelta dell'interfaccia:** È stata selezionata la scheda di rete attiva (identificata come `eno1` o `nic0`), verificando che il link fosse "UP".
- **Hostname:** È stato assegnato il nome al nodo (FQDN), mantenendo la struttura richiesta (es. `pve.fritz.box`).
- **Indirizzo IP Statico:** È stato impostato l'indirizzo **192.168.178.171** (con maschera `/24`), assicurando che il server avesse un indirizzo fisso e non cambiasse a ogni riavvio.
- **Gateway e DNS:** Impostati sull'indirizzo del router Fritz!Box (**192.168.178.1**) per garantire l'uscita su internet.

#### **3. Finalizzazione sul disco**
- **Target:** È stato selezionato l'**SSD SanDisk** come disco di destinazione per il sistema operativo e i file di sistema di Proxmox.
- **Installazione:** Completata la procedura automatica e riavviato il sistema.

#### **4. Troubleshooting dell'accesso Web (Post-Installazione)**
- **Problema:** L'interfaccia era raggiungibile da smartphone ma non dal PC principale.
- **Causa 1 (Indirizzo):** Tentativo di accesso all'IP `.100` invece del `.171` corretto impostato durante l'installazione.
- **Causa 2 (Software di rete):** Presenza di **Hamachi** sul PC, che creava conflitti di instradamento impedendo al browser di "vedere" l'IP locale del server.
- **Risoluzione:** Accesso tramite l'URL completo **`https://192.168.178.100:8006`** dopo aver verificato la raggiungibilità della rete locale.


---
## Collegamenti
- Torna al corso: [[Dashboard H-NET]]