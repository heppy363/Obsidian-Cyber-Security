---
tipo: nota_lezione
corso: "Dashboard H-NET"
tags: [progetto, hNet, Completed]
creato: 2026-03-16 22:06
---

# 📝 Lezione: Configurazione pratica primo attacco 
**Corso:** [[Dashboard H-NET]]

---
## Contenuto
## 1. Setup Infrastruttura Proxmox (Il Ferro)
Prima di creare le macchine, devi preparare il "terreno" di rete.
1. **Login Proxmox Web UI** > Seleziona il nodo (es. `pve`).
2. **System > Network > Create > Linux Bridge**:
    - **Name:** `vmbr1`
    - **IPv4/CIDR & Gateway:** Lascia VUOTO.
    - **Bridge ports:** Lascia VUOTO.
    - **Comment:** "Rete Isolata Attacco".
3. **Apply Configuration**. (Ora hai un bus di rete che non va su internet).

## 2. Configurazione VM Gateway (La Dogana)
Crea una VM Debian 12 (512MB RAM, 1 CPU).
## A. Hardware
- **Net0:** collegata a `vmbr0` (Internet ISP).

- **Net1:** collegata a `vmbr1` (Rete Interna).

## B. Configurazione OS
Accedi come root e modifica `/etc/network/interfaces`:
```
auto eth0
iface eth0 inet dhcp

auto eth1
iface eth1 inet static
    address 10.0.0.1
    netmask 255.255.255.0
```

Applica: `systemctl restart networking` o `ip link set eth1 up`.
## C. Installazione e Configurazione Tor
```
apt update && apt install tor -y
nano /etc/tor/torrc
```
Aggiungi in fondo:
```
VirtualAddrNetworkIPv4 10.192.0.0/10
AutomapHostsOnResolve 1
TransPort 10.0.0.1:9040
DNSPort 10.0.0.1:5353
```
Riavvia: `systemctl restart tor`.
## D. Script Kill-Switch e Routing (Il "Cuore")
Crea `/root/gateway_init.sh`:
```
#!/bin/bash
echo 1 > /proc/sys/net/ipv4/ip_forward
iptables -F
iptables -t nat -F

# Redirezione traffico verso Tor
iptables -t nat -A PREROUTING -i eth1 -p udp --dport 53 -j REDIRECT --to-ports 5353
iptables -t nat -A PREROUTING -i eth1 -p tcp --syn -j REDIRECT --to-ports 9040

# Kill-switch: impedisce ai container di uscire in chiaro via eth0
iptables -A FORWARD -i eth1 -o eth0 -j REJECT
iptables -A FORWARD -i eth1 -j ACCEPT # Permette forwarding interno se serve
```
Rendilo eseguibile: `chmod +x /root/gateway_init.sh` e mettilo nel crontab (`@reboot`) o lancialo a mano.



---
## Collegamenti
- Torna al corso: [[Dashboard H-NET]]