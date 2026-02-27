---
tipo: nota_lezione
corso: "Dashboard H-NET"
tags: [progetto, hNet, Completed]
creato: 2026-02-27 21:35
---

# 📝 Lezione: Configurazione fisica minima 
**Corso:** [[Dashboard H-NET]]

---
## Contenuto
### 1. Collegamento Fisico (Layer 1)
Il flusso del segnale sarà questo:
1. **Muro → Router ISP**: Il cavo della fibra o DSL entra nel router del tuo operatore.
2. **Router ISP → Lenovo M720q (pfSense)**: Colleghi un cavo Ethernet da una porta LAN del router ISP alla porta che sceglierai come **WAN** sulla tua scheda Intel i350.
3. **Lenovo M720q → Switch Netgear GS116E**: Colleghi un cavo dalla seconda porta della scheda Intel (**LAN**) a una porta qualsiasi dello switch Netgear (es. la porta 1).
4. **Switch Netgear → Tuoi Dispositivi**: PC, access point Wi-Fi, server e altri dispositivi vanno tutti collegati allo switch Netgear.

### 2. Configurazione del Router ISP (Fondamentale)
Per evitare problemi di "Doppio NAT" (che possono dare noie ai giochi online o alle VPN), hai due opzioni sul router del tuo operatore:
- **Opzione A (Consigliata): Modem Passthrough / Bridge Mode.** Se il tuo router ISP lo permette, disattiva la parte router e passa l'IP pubblico direttamente al Lenovo.
- **Opzione B (DMZ):** Se non puoi metterlo in bridge, assegna un IP statico alla WAN del Lenovo (es. `192.168.1.2`) e imposta quell'IP come **DMZ** nelle impostazioni del router ISP. Questo invierà tutto il traffico direttamente a pfSense.
- **Ricorda:** Disattiva il Wi-Fi del router ISP per evitare interferenze, visto che ora la tua rete sarà gestita dal Lenovo.

### 3. Logica delle Sottoreti (IP Adressing)
Per non fare confusione, le due reti devono avere numeri diversi:
- **Rete ISP (WAN):** Probabilmente sarà `192.168.1.x`.
- **Rete Tua (LAN - pfSense):** Imposta pfSense su una classe diversa, ad esempio `10.0.0.1` o `192.168.10.1`.
- In questo modo, il Lenovo farà da "muro" e proteggerà tutto quello che sta dietro (nello switch e nei tuoi dispositivi).

### 4. Il ruolo dello Switch Netgear GS116E
Visto che hai uno switch "Managed", la vera magia inizia con le **VLAN**. In futuro potrai fare questo:
- **VLAN 10 (Main):** Per il tuo PC principale e Obsidian.
- **VLAN 20 (IoT):** Per lampadine smart o dispositivi meno sicuri (che non potranno "vedere" il tuo PC).
- **VLAN 30 (Guest):** Per gli amici che vengono a trovarci.

### Primo step quando avrai tutto:
1. Installa pfSense sul Lenovo.
2. Quando ti chiede "Assign Interfaces", identifica le porte della Intel i350.
3. Collega il PC direttamente alla porta LAN del Lenovo per fare la prima configurazione via browser (solitamente su `192.168.1.1` di default, ma cambialo se il router ISP usa lo stesso indirizzo).



---
## Collegamenti
- Torna al corso: [[Dashboard H-NET]]
- [[Configurazione di rete esterna]]