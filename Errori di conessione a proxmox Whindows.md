---
tipo: nota_lezione
corso: "Dashboard H-NET"
tags: [progetto, hNet, Completed]
creato: 2026-03-22 15:58
---

# 📝 Lezione: Errori di conessione a proxmox Whindows
**Corso:** [[Dashboard H-NET]]

---
## Contenuto
Se il PC principale smette di vedere il server ma il telefono ci arriva, il problema è la **cache di rete** di Windows.
## Procedura di sblocco rapido:
Apri il **Terminale (Admin)** e incolla questi comandi uno dopo l'altro:
1. **Pulizia DNS:** `ipconfig /flushdns` (Dimentica i vecchi indirizzi salvati).
2. **Reset dei Socket:** `netsh winsock reset` (Ripristina il catalogo delle connessioni).
3. **Reset IP:** `netsh int ip reset` (Reinstalla lo stack TCP/IP).
4. **Pulizia ARP:** `arp -d *` (Cancella la tabella degli indirizzi fisici dei dispositivi in rete).

> [!IMPORTANT] **Il segreto dell'HTTPS:** Ricorda che Windows spesso blocca Proxmox se non scrivi l'indirizzo esatto. Salva nei preferiti: `https://192.168.178.100:8006` (L'**S** e la porta **8006** sono obbligatori).

---
## Collegamenti
- Torna al corso: [[Dashboard H-NET]]