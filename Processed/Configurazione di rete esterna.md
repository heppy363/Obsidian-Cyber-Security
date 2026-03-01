---
tipo: nota_lezione
corso: "Dashboard H-NET"
tags: [progetto, hNet, Completed]
creato: 2026-02-27 21:40
---

# 📝 Lezione: Configurazione di rete esterna 
**Corso:** [[Dashboard H-NET]]

---
## Contenuto

### 1. Schema di Collegamento Fisico
Il tuo laboratorio sarà un'isola all'interno della rete domestica:
1. **Cavo Ethernet:** Collega una porta LAN del router ISP alla porta **WAN** (Intel i350) del tuo Lenovo M720q.
2. **Cavo Ethernet:** Dalla porta **LAN** (Intel i350) del Lenovo vai allo switch **Netgear GS116E**.
3. **Dispositivi Lab:** Collega il tuo PC per Obsidian, i tuoi server o altri dispositivi del lab solo allo switch Netgear.

### 2. Gestione degli Indirizzi IP (Evitare conflitti)
Per far sì che pfSense non "litighi" con il router dell'operatore, devi assicurarti che usino linguaggi (subnet) diversi.
- **Rete Casa (Router ISP):** Probabilmente usa `192.168.1.1`. Il tuo Lenovo riceverà un indirizzo da questa rete sulla sua porta WAN (es. `192.168.1.50`).
- **Rete Lab (pfSense):** Devi impostare la LAN del Lenovo su una rete completamente diversa, ad esempio **`10.0.0.1`**.

In questo modo, tutto quello che colleghi allo switch Netgear prenderà un indirizzo tipo `10.0.0.x` e sarà invisibile e protetto rispetto al resto della casa.

### 3. Configurazione "Double NAT"
Visto che non puoi mettere il router ISP in bridge, ti troverai in una situazione di **Double NAT**.
- **Per il Lab:** Non è un problema. Navigherai su internet e scaricherai aggiornamenti senza accorgertene.
- **Accesso dall'esterno:** Se un domani vorrai accedere al tuo lab mentre sei fuori casa (tramite VPN), dovrai fare un "Port Forwarding" sul router dell'ISP verso l'indirizzo IP del Lenovo.

### 4. Il vantaggio di questa scelta
- **Indipendenza:** Se rompi qualcosa facendo esperimenti su pfSense (succede!), il Wi-Fi di casa continuerà a funzionare e nessuno si lamenterà.
- **Sicurezza:** Il tuo homelab è dietro due firewall (quello ISP e pfSense). È una cassaforte.
- **VLAN dedicate:** Sul tuo switch Netgear potrai comunque creare VLAN (es. una per i server, una per i test) che rimarranno confinate dentro il tuo lab.




---
## Collegamenti
- Torna al corso: [[Dashboard H-NET]]
- [[Gestione degli accessi esterni minimo]]