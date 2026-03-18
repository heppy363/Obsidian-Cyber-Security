---
tipo: nota_lezione
corso: "Dashboard Networking Basics"
tags: [progetto, certificazioni, networkingBasics, Completed]
creato: 2026-03-16 15:55
---

# 📝 Lezione: Tipi di componenti della rete e connessioni
**Corso:** [[Dashboard Networking Basics]]

---
## Contenuto
## 1. Dispositivi Finali (End Devices / Hosts)
Sono i dispositivi con cui l'utente interagisce direttamente. In una rete, questi sono sia l'origine che la destinazione dei dati.
- **Esempi:** Laptop, PC desktop, Smartphone, Stampanti di rete, Tablet, Server.
- **Concetto chiave:** Ogni dispositivo finale ha un indirizzo (come l'IP) per essere identificato univocamente nella rete.

## 2. Dispositivi Intermedi (Intermediate Devices)
Sono i "vigili urbani" della rete. Il loro compito è connettere i dispositivi finali e garantire che i dati viaggino correttamente da un punto all'altro.
- **Esempi:** * **Switch:** Collega i dispositivi all'interno di una stessa rete locale (LAN).
    - **Router:** Collega reti diverse tra loro e decide il percorso migliore per i dati verso Internet.
    - **Wireless Access Point (WAP):** Fornisce connettività Wi-Fi.
    - **Firewall:** Protegge la rete filtrando il traffico (fondamentale per il tuo obiettivo da Pentester).

## 3. Mezzi di Rete (Network Media)
È il canale fisico (o invisibile) su cui viaggiano i dati.
- **Rame (Cavi Ethernet):** Economico e comune per brevi distanze.
- **Fibra Ottica:** Altissima velocità e lunghe distanze.
- **Wireless (Onde Radio):** Per la mobilità.

---

## Il punto di vista del Sistemista
Per rispondere al dubbio di Kishori: le sue note passano dal laptop al desktop perché entrambi sono collegati a un **dispositivo intermedio** (probabilmente uno Switch o un Access Point aziendale) che instrada i dati verso un **Server** centrale, dove le informazioni vengono salvate e rese disponibili a tutti gli altri computer della clinica.


- [[Client and server]]
- [[Componenti di una rete]]
- [[ISP]]
- [[Domande e risposte networking base]]

---
## Collegamenti
- Torna al corso: [[Dashboard Networking Basics]]