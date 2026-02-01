---
aliases:
  - Completate
tags:
  - Completed
  - progettiPersonali
  - Linux
---
--- 
## Nozioni

## Panoramica
Si tratta di una tecnica che trasforma la scheda di rete del PC host in un vero e proprio ponte, quindi di fatto andiamo a disabilitare il sistema di NAT (la macchina avra un suo indirizzo ip fisso), dato che il router non risolvera l'indirizzo da privato a pubblico ma la macchina stessa ne avra uno. 
**Caratteristiche e Utilizzi Principali:**
- **Trasparenza:** Il dispositivo in bridge non modifica i pacchetti dati, agendo solo a livello di collegamento (MAC address).
- **[IP Passthrough](https://www.google.com/search?client=firefox-b-d&q=IP+Passthrough&ved=2ahUKEwiyvZ-Fh7aSAxVbnf0HHbcCJWcQgK4QegQIAxAC):** Il modem/router principale passa l'indirizzo IP pubblico direttamente al router secondario o al dispositivo connesso.
- **Semplificazione Reti:** Connette due LAN separate, facendole apparire come un'unica rete.
- **Virtualizzazione:** Nelle macchine virtuali, la modalità bridge permette alla VM di apparire come un host fisico separato sulla rete, ottenendo un IP dalla stessa subnet del computer ospitante.
- **Wireless Bridge:** Collega due segmenti di rete tramite Wi-Fi per estendere la portata, utile per lunghi raggio. 
	- ne aumenta il raggio dato che la rete si unifica anche se utilizzi piu router.

La modalità bridge è particolarmente utile quando si desidera utilizzare un router di terze parti più performante, lasciando al modem dell'ISP solo il compito di interfaccia fisica

## Configurazione di una macchina virtuale in modalita Bridge WMwear 
1) Andare in Settings -> Network Adapter
2) Selezionare l'opzione **Bridged** 
	1) Spuntare -> Connect at power on (al accensione fa tutto in automatico)
3) Operazioni sulla macchina virtuale quello che ci interessa e che la macchina virtuale sia sulla stessa rete della macchina host 
	1) Mettere un indirizzo IP fisso no DHC 
	2) Creazione del file di configurazione per il networkManager ```sudo nano /etc/netplan/00-installer-config.yaml```
	3) con la seguente configurazione della rete 
```
network:
  version: 2
  renderer: NetworkManager
  ethernets:
    ens33:
      dhcp4: no
      addresses:
        - 192.168.178.XXX/24
      routes:
        - to: default
          via: 192.168.178.1
      nameservers:
        addresses: [192.168.178.1, 8.8.8.8]
```
- Cambiare -> 192.168.178.XXX/24 con l'indirizzo previsto molto alto 
- Fare il relativo PING tra le due macchine e vedere se tutto funziona 


## Risoluzioni problemi generale 
1) Su macchina host in caso di whindows abiltiare tutti i tipi di pacchetti ICMPv4 (i ping) con questo comando 
```
netsh advfirewall firewall add rule name="Allow ICMPv4 Inbound" protocol=icmpv4:any,any dir=in action=allow
```
2) Disabilitare le altre schede di rete virtuali da 
3) Disabilitare Hyper-V il maledetto da un sacco di problemi nel caso ci siano altri hyper visor che usano lo stak di rete con questo comando 
```
Disable-WindowsOptionalFeature -Online -FeatureName Microsoft-Hyper-V-All
```
4) Cambiare il breadg della scheda di rete andare su _**Virtual Network Editor**_
	1) Clicca in basso su **Change Settings** (richiede permessi di amministratore).
	2) Seleziona la rete chiamata **VMnet0** (che di solito è impostata su _Bridged_).
	3) **Importante:** Sotto "Bridged to:", non lasciare "Automatic". Seleziona manualmente il nome della tua scheda di rete (es. _Killer Wi-Fi_ o _Intel Ethernet Connection_).
	4) Applica e chiudi.




## Link 
1) 