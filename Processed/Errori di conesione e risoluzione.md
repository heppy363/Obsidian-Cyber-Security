---
tipo: nota_lezione
corso: "Dashboard H-NET"
tags: [progetto, hNet, Completed]
creato: 2026-03-22 15:57
---

# 📝 Lezione: Errori di connesione e risoluzione
**Corso:** [[Dashboard H-NET]]

---
## Contenuto
Il file `/etc/network/interfaces` è il cuore del tuo server. La configurazione corretta per la tua rete (subnet 178) è questa:
## Il file `/etc/network/interfaces`


```
auto lo
iface lo inet loopback

# La tua scheda fisica (senza IP, serve solo da ponte)
iface nic0 inet manual

# Il bridge (Ponte) che dà vita ai tuoi container
auto vmbr0
iface vmbr0 inet static
    address 192.168.178.100/24    # IP statico del tuo server
    gateway 192.168.178.1         # L'indirizzo del tuo router (Fritz!Box)
    bridge-ports nic0             # Collega il bridge alla scheda fisica
    bridge-stp off
    bridge-fd 0
```

## Comandi di emergenza (da console fisica):
- `nano /etc/network/interfaces`: Per modificare la rete.
- `ifup vmbr0`: Per attivare la rete dopo una modifica.
- `ip addr`: Per verificare se il server ha preso l'IP corretto.
- `ping 8.8.8.8`: Per testare se il server "vede" internet.

---
## Collegamenti
- Torna al corso: [[Dashboard H-NET]]