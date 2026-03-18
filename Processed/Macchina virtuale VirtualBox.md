---
tipo: nota_lezione
corso: "Dashboard Udemy morroLinux Linux"
tags: [progetto, Linux, Udemy, morroLinux, certificazioni, Completed]
creato: 2026-03-18 22:59
---

# 📝 Lezione: Macchina virtuale VirtualBox
**Corso:** [[Dashboard Udemy morroLinux Linux]]

---
## Contenuto
Quando configuri una Scheda di Rete (Network Adapter) in una VM, stai definendo come il "cavo virtuale" della macchina guest si collega al mondo reale.

## 1. NAT (Network Address Translation)
È la modalità predefinita. La VM si trova dietro un "router virtuale" creato da VirtualBox.
- **Come funziona:** La VM riceve un indirizzo IP privato (solitamente `10.0.2.x`). Quando la VM vuole andare su Internet, VirtualBox "traduce" il suo traffico usando l'indirizzo IP del tuo computer fisico (l'Host).
- **Visibilità:**
    - **VM -> Internet:** Sì.
    - **Internet -> VM:** No (protetta dal NAT).
    - **Host -> VM:** No (a meno di non configurare il _Port Forwarding_).
- **Caso d'uso:** Ideale quando hai solo bisogno che la VM scarichi aggiornamenti o navighi, senza che nessuno dall'esterno debba collegarsi ad essa.


## 2. Scheda con Bridge (Bridged Networking)
In questa modalità, la VM diventa un "membro paritario" della tua rete fisica.
- **Come funziona:** VirtualBox si collega direttamente alla tua scheda di rete fisica (Wi-Fi o Ethernet). La VM chiede un indirizzo IP direttamente al tuo router di casa o dell'ufficio.
- **Visibilità:**
    - **VM -> Internet:** Sì.
    - **Host <-> VM:** Sì, comunicano come se fossero due PC separati collegati allo stesso switch.
    - **Altri PC della rete -> VM:** Sì, possono "pingare" la VM o connettersi ai suoi servizi.
- **Caso d'uso:** Necessario se stai configurando un **Server** (Web, Database) che deve essere raggiungibile da altri dispositivi nella tua rete locale.

## 3. Rete Solo Host (Host-Only Adapter)
Crea una rete privata ed esclusiva tra il tuo computer (Host) e le tue macchine virtuali.
- **Come funziona:** Viene creata una scheda di rete virtuale sull'Host (es. `vboxnet0`). Le VM collegate a questa rete non passano attraverso la scheda fisica dell'Host.
- **Visibilità:**
    - **VM -> Internet:** **No**.
    - **Host <-> VM:** Sì (comunicazione diretta).
    - **VM <-> VM:** Sì (se collegate allo stesso adapter host-only).
- **Caso d'uso:** Massima sicurezza. Utile per laboratori di test dove vuoi comunicare con la VM via SSH dall'Host, ma non vuoi che la VM sia esposta a Internet o viceversa.

## Tabella Comparativa Rapida

|Modalità|Accesso Internet|VM visibile dall'Host|VM visibile dalla LAN|
|---|---|---|---|
|**NAT**|✅ Si|❌ No (solo via Port Forward)|❌ No|
|**Bridged**|✅ Si|✅ Si|✅ Si|
|**Host-Only**|❌ No|✅ Si|❌ No|
|**Internal**|❌ No|❌ No|❌ No|

## Concetti Chiave per l'Esame LPI
- **Port Forwarding (Inoltro Porte):** Se usi il NAT ma vuoi comunque accedere alla VM (es. via SSH sulla porta 22), devi istruire VirtualBox: _"Tutto il traffico che arriva sul mio PC fisico alla porta 2222, giralo alla porta 22 della VM"_.
- **Promiscuous Mode:** In modalità Bridged, potresti dover attivare la "Modalità Promiscua" per permettere alla scheda virtuale di analizzare tutto il traffico di rete (utile per sniffing o analisi di rete).
- **MAC Address:** Ogni scheda virtuale ha un indirizzo MAC univoco generato da VirtualBox. Se cloni una VM, ricordati di **rigenerare il MAC address** per evitare conflitti di rete.

---
## Collegamenti
- Torna al corso: [[Dashboard Udemy morroLinux Linux]]