---
tipo: nota_lezione
corso: "Dashboard H-NET"
tags: [progetto, hNet, Completed]
creato: 2026-02-25 18:51
---

# 📝 Lezione: Risoluzione problematica SW
**Corso:** [[Dashboard H-NET]]

---
## Contenuto
#### **1. Analisi del problema (Diagnostica)**

- **Sintomo:** Il server Proxmox era raggiungibile da smartphone (Wi-Fi) ma non dal PC fisso (Ethernet), nonostante fossero sulla stessa sottorete (`192.168.178.x`).
    
- **Errore rilevato:** Il comando `ping` restituiva _"Risposta da 192.168.178.166: Host di destinazione non raggiungibile"_. Questo indicava che il blocco era interno al PC fisso (il pacchetto non riusciva nemmeno a uscire verso il router).
    

#### **2. Identificazione del conflitto (Hamachi)**

- **Causa principale:** Tramite il comando `ipconfig` è stata rilevata la presenza di **Hamachi**. Le VPN mesh come Hamachi spesso creano schede di rete virtuali con priorità (metrica) più alta rispetto alla scheda fisica, "sequestrando" il traffico destinato agli IP locali e impedendo al PC di vedere il server Proxmox.
    

#### **3. Azioni correttive intraprese**

Per ripristinare la corretta comunicazione, abbiamo eseguito i seguenti passaggi:

- **Correzione dell'IP:** È stato verificato l'indirizzo IP corretto del server (`.171` invece del `.100` che Firefox stava tentando di usare inizialmente).
    
- **Disattivazione Servizi Virtuali:** È stato arrestato il servizio di Hamachi per liberare le rotte di rete occupate dal software.
    
- **Disabilitazione Scheda Virtuale:** Tramite il pannello `ncpa.cpl` (Connessioni di rete), è stata disabilitata fisicamente la scheda di rete virtuale di Hamachi per evitare che Windows continuasse a instradare i pacchetti nel tunnel virtuale anziché sulla rete locale fisica.
    
- **Pulizia della cache ARP e DNS:** Sono stati svuotati i record temporanei (`ipconfig /flushdns` e `arp -d`) per forzare Windows a cercare nuovamente l'indirizzo fisico (MAC address) della scheda madre Supermicro sulla rete locale.
    
- **Verifica Protocollo HTTPS:** È stato confermato l'uso obbligatorio del prefisso `https://` e della porta `:8006`, necessari per superare il controllo di sicurezza del browser.

---
## Collegamenti
- Torna al corso: [[Dashboard H-NET]]