---
tipo: nota_lezione
corso: "Dashboard H-NET"
tags: [progetto, hNet, Completed]
creato: 2026-03-16 21:05
---

# 📝 Lezione: Layer di anonimato
**Corso:** [[Dashboard H-NET]]

---
## Contenuto
## Creazione del Bridge Isolato (Il "Vat" di contenimento)

Di default, Proxmox usa `vmbr0` per collegare le macchine alla tua rete domestica (LAN). Noi creeremo un secondo bridge che non ha un'interfaccia fisica associata. Questo bridge sarà una rete interna dove le macchine possono parlarsi ma **non** possono uscire su internet da sole.
1. Vai su **Proxmox Web UI** -> Seleziona il tuo **Nodo** -> **System** -> **Network**.
2. Clicca su **Create** -> **Linux Bridge**.
3. Nome: `vmbr1` (o quello che preferisci).
4. **IPv4/CIDR:** Lascialo vuoto (non vogliamo che l'host Proxmox abbia un IP su questa rete sensibile).
5. **Bridge ports:** Lascia vuoto.
6. Clicca su **Create** e poi su **Apply Configuration**.


## 2. Setup del Gateway (La "Dogana")
Dobbiamo creare una VM che faccia da ponte tra `vmbr0` (Internet reale) e `vmbr1` (Rete anonima). Ti consiglio una VM **Debian leggera** o **pfSense**. Useremo Debian per la massima flessibilità da sistemista.
1. Crea una VM Debian.
2. **Hardware -> Network Device:**
    - `net0`: Collegato a `vmbr0` (prenderà l'IP dal tuo router/ISP).
    - Aggiungi un secondo device `net1`: Collegato a `vmbr1`.
3. All'interno della VM, configura `net1` con un IP statico, ad esempio `10.0.0.1/24`. Questo sarà il **Gateway** per tutti i tuoi futuri container di attacco.

## 3. Configurazione del Tunnel (VPN + Kill-Switch)
Sulla VM Gateway, dobbiamo installare il client VPN (Wireguard o OpenVPN) e configurare il firewall in modo che, se la VPN cade, il traffico si blocchi istantaneamente.
**Logica del Firewall (iptables/nftables):**
1. Permetti il traffico da `vmbr1` (rete interna) verso l'interfaccia della VPN (es. `tun0` o `wg0`).
2. **Nega** tutto il traffico da `vmbr1` verso `vmbr0` (l'interfaccia fisica dell'ISP).
3. Esegui il NAT (Masquerade) solo sull'interfaccia VPN.

In questo modo, se la VPN si disconnette, l'interfaccia virtuale sparisce e i pacchetti provenienti dai container non sapranno dove andare, morendo dentro la VM Gateway. Il tuo ISP vedrà solo un flusso criptato verso un unico server VPN.

## 4. Il tocco dell'esperto: DNS Leak Protection
L'errore del neofita è usare i DNS di Google o dell'ISP. Il bersaglio non ti vedrà, ma il tuo ISP saprà che stai risolvendo l'host `sito-target-pentest.com`.
- Sulla VM Gateway, installa **Unbound** o configura i DNS della VPN.
- Assicurati che i container su `vmbr1` ricevano via DHCP (o staticamente) come server DNS solo l'IP della VM Gateway (`10.0.0.1`).

---

## 5. Test di "Tenuta"
Prima di creare la "baracca" dei container:
1. Crea un container di test collegato solo a `vmbr1`.
2. Imposta come Gateway `10.0.0.1`.
3. Esegui un `curl ifconfig.me`: deve restituire l'IP della VPN.
4. Spegni la VPN sulla VM Gateway e riprova il curl: **deve andare in timeout**. Se naviga, hai un "leak" e l'anonimato è compromesso.

## Riassunto Architetturale
- **Internet** <--> **ISP** <--> **Proxmox (vmbr0)** <--> **VM Gateway (VPN)** <--> **Proxmox (vmbr1)** <--> **Container d'attacco**

- 


---
## Collegamenti
- Torna al corso: [[Dashboard H-NET]]