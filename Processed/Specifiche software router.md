---
tipo: nota_lezione
corso: "Dashboard H-NET"
tags: [progetto, hNet, Completed]
creato: 2026-02-19 22:39
---

# 📝 Lezione: Specifiche software router
**Corso:** [[Dashboard H-NET]]

---
## Contenuto
## 1. Preparazione su Proxmox

Prima di installare pfSense, devi preparare i "tubi" (i bridge) su Proxmox che si collegheranno al tuo switch **Netgear GS116E**.
- **vmbr0 (WAN):** Sarà il bridge collegato alla porta fisica che riceve internet dal tuo modem.
- **vmbr1 (LAN/Trunk):** Sarà il bridge collegato alla porta dello switch Netgear (Porta 16). **Importante:** Spunta l'opzione **"VLAN aware"** nelle impostazioni del bridge su Proxmox. Questo permette a pfSense di inviare i pacchetti "taggati" allo switch.
## 2. Creazione della VM pfSense
Crea una nuova VM su Proxmox con queste specifiche:
- **CPU:** Almeno 2 core.
- **RAM:** 2GB (più che sufficienti per un lab).
- **Network:** Aggiungi due interfacce di rete: una su `vmbr0` (WAN) e una su `vmbr1` (LAN).
- **ISO:** Carica l'immagine ufficiale di pfSense Community Edition.
## 3. Configurazione Base (Wizard)
Una volta avviata la VM e completata l'installazione guidata su disco, accederai alla console.
1. **Assign Interfaces:** Identifica quale porta è la WAN e quale la LAN.
2. **Configurazione IP:** Assegna un IP statico alla LAN (es. `10.0.10.1`, che sarà il Gateway della tua **VLAN 10 Admin**).
3. **Accesso WebGUI:** Collega il tuo PC alla porta dello switch configurata per la VLAN 10 e digita l'IP nel browser.
## 4. Creazione delle VLAN su pfSense
Ora dobbiamo dire a pfSense che sulla porta LAN "viaggiano" più reti. Vai su **Interfaces > Assignments > VLANs**:
- **VLAN 20 (DMZ):** Tag `20`, interfaccia genitrice `LAN`.
- **VLAN 30 (Sviluppo):** Tag `30`, interfaccia genitrice `LAN`.
- **VLAN 40 (Storage):** Tag `40`, interfaccia genitrice `LAN`.
Dopo averle create, vai su **Interfaces > Assignments** e aggiungile cliccando sul tasto "+". Abilitale e assegna loro l'IP del Gateway (es. `10.0.20.1`, `10.0.30.1`, ecc.).
## 5. Abilitazione del DHCP Server
Per ogni VLAN (tranne forse quella dello Storage dove userai IP statici per il NAS), vai su **Services > DHCP Server**:
- Abilita il DHCP.
- Imposta il range di IP (es. `10.0.20.10` a `10.0.20.100`).
- **DNS:** Puoi usare quelli di Google/Cloudflare o configurare il DNS Resolver interno di pfSense.
## 6. Prime Regole di Firewall (Fondamentali)
Di base, pfSense blocca tutto. Devi creare le regole in **Firewall > Rules**:
1. **VLAN 10 (I Re):** Crea una regola "Pass" con _Source: VLAN 10 net_ e _Destination: Any_. Questo ti permette di navigare e vedere tutte le altre VLAN.
2. **VLAN 20 (DMZ):** Crea una regola "Pass" verso la WAN (Internet), ma una regola "Block" verso le altre VLAN locali (10 e 30).
3. **VLAN 30 (Sviluppo):** Come la DMZ, ma permetti l'accesso specifico verso l'IP del NAS (VLAN 40) sulla porta del database o S3.
## 7. Integrazione con lo Switch Netgear
Ora che pfSense è pronto a mandare i tag `20, 30, 40`, devi assicurarti che il **Netgear GS116E** li capisca.
- Accedi alla WebGUI del Netgear.
- Vai su **VLAN > 802.1Q > Advanced**.
- Imposta la porta collegata a Proxmox come **"T" (Tagged)** per le VLAN 20, 30 e 40.
- Imposta le porte dei Mini PC e del NAS come **"U" (Untagged)** nelle rispettive VLAN.

# Collegamento internet 
### 1. Regola "Pass All" per la VLAN 10

Di base pfSense blocca tutto. Per il tuo PC personale, devi creare una regola permissiva:
- Vai su **Firewall > Rules > VLAN10**.
- Clicca su **Add** (freccia su).
- **Action:** Pass.
- **Protocol:** Any.
- **Source:** VLAN10 net (questo copre il tuo PC fisso e il portatile).
- **Destination:** Any.
- Questa regola dice: "Tutto ciò che viene dalla VLAN 10 può andare ovunque (Internet e altre VLAN)".
### 2. Configurazione del NAT (Outbound)
Per navigare su Internet, i tuoi indirizzi IP privati (es. `10.0.10.x`) devono essere "tradotti" nell'indirizzo IP pubblico del tuo modem.
- Vai su **Firewall > NAT > Outbound**.
- Assicurati che sia selezionato **"Automatic outbound NAT rule generation"** (opzione predefinita).
- pfSense riconoscerà automaticamente la tua nuova VLAN 10 e creerà la regola per farla uscire su Internet tramite l'interfaccia WAN.
### 3. DNS per la navigazione
Perché il tuo PC possa aprire siti come Google o GitHub, ha bisogno di risolvere i nomi:
- In **Services > DHCP Server > VLAN10**, puoi inserire i DNS di Google (`8.8.8.8`) o Cloudflare (`1.1.1.1`).
- In alternativa, usa il **DNS Resolver** di pfSense (`10.0.10.1`) per avere maggiore privacy e velocità grazie alla cache locale.

### 4. Il vantaggio dello Switch Netgear
Mentre il tuo PC naviga o scarica file pesanti da Internet, il **Netgear GS116E** assicura che questo traffico non interferisca con gli altri servizi:
- **QoS (Quality of Service):** Se vuoi che il tuo PC abbia sempre la priorità massima rispetto ai Mini PC (ad esempio mentre giochi o sei in call), puoi impostare la priorità sulla porta fisica del tuo PC direttamente dal pannello del Netgear.
- **Affidabilità:** Grazie al design in metallo che dissipa il calore, lo switch non rallenta anche se la tua connessione internet è al massimo del carico.
### Riassunto della gerarchia
1. **PC Fisso:** Invia una richiesta web.
2. **Netgear GS116E:** Identifica il pacchetto come **VLAN 10** e lo manda alla porta **Trunk** di Proxmox/pfSense.
3. **pfSense:** Controlla la regola (Pass), traduce l'IP (NAT) e lo spara sulla **WAN** verso Internet.

---
## Collegamenti
- Torna al corso: [[Dashboard H-NET]]