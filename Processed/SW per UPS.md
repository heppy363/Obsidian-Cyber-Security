---
tipo: nota_lezione
corso: "Dashboard H-NET"
tags: [progetto, hNet, Completed]
creato: 2026-02-24 22:48
---

# 📝 Lezione: SW per UPS 
**Corso:** [[Dashboard H-NET]]

---
## Contenuto
**NUT (Network UPS Tools)** è lo standard universale nel mondo Linux/Server per gestire lo spegnimento coordinato di più macchine. È un software "client-server" che permette a un solo UPS di parlare con decine di computer attraverso la tua rete locale.

## La Logica "Master-Slave" (Server e Client)
Dato che l'UPS ha una sola porta USB, non puoi collegarla a tutti e 4 i dispositivi (i 3 mini PC + il server di calcolo). Ecco la gerarchia:
1. **Il "Master" (Server di calcolo):** Colleghi il cavo USB dell'UPS a questa macchina. Il Server di calcolo "legge" lo stato della batteria.
2. **Gli "Slave" (I 3 Mini PC):** Questi non sono collegati fisicamente all'UPS, ma "ascoltano" il Server Master via Wi-Fi o Ethernet.
### Cosa succede quando salta la corrente?
1. L'UPS comunica al **Server Master** via USB: _"Batteria al 10%!"_.
2. Il **Server Master** invia un segnale di rete ai **3 Mini PC**: _"Spegnete tutto subito!"_.
3. I **Mini PC** eseguono lo shutdown sicuro.
4. Una volta che i Mini PC sono spenti, il **Server Master** spegne se stesso per ultimo.
## Come si configura (In breve)
Se usi **Proxmox, Debian o Ubuntu** sul tuo Home Lab, l'installazione è molto simile:
### Sul Server Master (quello con l'USB):
Dovrai installare il pacchetto e configurare il driver (solitamente `usbhid-ups`).
- Nel file `nut.conf` imposti `MODE=netserver`.

- Nel file `upsd.users` crei un utente e una password che i mini PC useranno per "autenticarsi" e leggere lo stato dell'UPS.

### Sui 3 Mini PC (gli Slave):
- Nel file `nut.conf` imposti `MODE=netclient`.
- Nel file `upsmon.conf` aggiungi una riga che punta all'IP del Server Master: `MONITOR ups@192.168.1.XX 1 utente password slave`

## Tre Regole d'Oro per far funzionare NUT
1. **Lo Switch deve essere sotto UPS:** Questa è la regola più importante. Se lo switch si spegne perché non è collegato alla batteria, il Server Master non può inviare il segnale di "Spegni tutto" ai mini PC via rete.
2. **IP Statici:** Il Server Master deve avere un indirizzo IP fisso (es. `192.168.1.100`), altrimenti i mini PC non sapranno a chi chiedere informazioni.
3. **Ordine di spegnimento:** Assicurati che il Server Master sia l'ultimo a spegnersi. Solitamente si imposta un piccolo ritardo (delay) per dare tempo ai mini PC di chiudere i processi pesanti.

---
## Collegamenti
- Torna al corso: [[Dashboard H-NET]]