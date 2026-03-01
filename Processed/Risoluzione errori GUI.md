---
tipo: nota_lezione
corso: "Dashboard H-NET"
tags: [progetto, hNet, Completed]
creato: 2026-02-28 23:08
---

# 📝 Lezione: Risoluzione errori GUI 
**Corso:** [[Dashboard H-NET]]

---
## Contenuto
### 🛠 Sezione 1: Risoluzione Errori GUI e Repository

All'inizio, l'interfaccia web di Proxmox restituiva errori JavaScript (es. `Proxmox.Utils is undefined`) e `500 No such file`. Il problema era causato da repository Enterprise bloccati che impedivano il corretto aggiornamento dei pacchetti.

#### **1.1 Rimozione blocchi Enterprise**
Abbiamo disabilitato i nuovi file di configurazione `.sources` (introdotti con Debian Trixie) che richiedevano una licenza a pagamento:
```
mv /etc/apt/sources.list.d/ceph.sources /etc/apt/sources.list.d/ceph.sources.bak
mv /etc/apt/sources.list.d/pve-enterprise.sources /etc/apt/sources.list.d/pve-enterprise.sources.bak
```

#### **1.2 Ripristino dei file corrotti**
Per sistemare la GUI, abbiamo forzato la reinstallazione dei componenti dell'interfaccia:
```
apt-get update
apt-get install --reinstall pve-manager proxmox-widget-toolkit -y
systemctl restart pveproxy
```


---
## Collegamenti
- Torna al corso: [[Dashboard H-NET]]
- [[installare VPN su proxmox versione 1.0]]