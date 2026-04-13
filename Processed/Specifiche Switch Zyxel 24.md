---
tipo: nota_lezione
corso: "Dashboard H-NET"
tags: [progetto, hNet, Completed]
creato: 2026-02-19 22:30
---

# 📝 Lezione: Specifiche Netgear GS116E
**Corso:** [[Dashboard H-NET]]

---
## Contenuto
## 1. Caratteristiche Hardware Fisiche
- **Porte:** 16 porte RJ45 10/100/1000 Mbps (Gigabit).
- **Chassis:** Interamente in **metallo**. È molto robusto e funge da dissipatore di calore.
- **Design Fanless (Senza Ventole):** È completamente silenzioso. Fondamentale se tieni il lab in una stanza dove vivi o dormi.
- **MTBF (Affidabilità):** Netgear dichiara oltre **2 milioni di ore** di funzionamento medio prima di un guasto. È un dispositivo fatto per restare acceso decenni.
## 2. Specifiche di Rete (Il "Cervello")
Questo switch non si limita a muovere i pacchetti, ma li gestisce:
- **Capacità di Switching:** 32 Gbps (significa che tutte le 16 porte possono andare a 1 Gbps contemporaneamente in download e upload senza rallentamenti).
- **Tabella Indirizzi MAC:** 8.000 voci (puoi collegare virtualmente migliaia di dispositivi tramite altri switch a valle senza che lui "dimentichi" dove sono).
- **Buffer di Pacchetti:** 512 KB (aiuta a gestire i picchi di traffico tra i tuoi DB e le BC-250).
## 3. Funzioni "Smart" Fondamentali per il tuo Lab
Ecco cosa useremo concretamente nel tuo progetto:
- **VLAN (802.1Q):** Questa è la funzione regina. Ti permette di segmentare lo switch. Ad esempio:
    - Porte 1-4: Rete Domestica.
    - Porte 5-10: Rete DB/Produzione (10.10.x.x).
    - Porte 11-16: Rete Gestione/BC-250.
    - _Anche se sono nello stesso switch fisico, non potranno parlarsi a meno che non lo decida pfSense._
- **QoS (Quality of Service):** Puoi dare la priorità al traffico dei tuoi Database o dei servizi musicali rispetto, ad esempio, a un download pesante, evitando "scatti" nello streaming.
- **Link Aggregation (LACP statico):** Se il tuo futuro NAS ha due porte LAN, puoi collegarle entrambe allo switch per avere un canale da **2 Gbps**.
- **IGMP Snooping:** Fondamentale per il tuo server multimediale. Evita che il traffico video multicast "inondi" tutte le porte dello switch, inviandolo solo a chi lo sta effettivamente guardando.
## 4. Gestione e Software
Il GS116E si gestisce in due modi:
1. **Interfaccia Web:** Digiti l'IP dello switch nel browser e hai una dashboard completa (molto comoda).
2. **ProSAFE Plus Utility:** Un software Windows dedicato per trovarlo in rete anche se non conosci l'IP o se hai fatto errori di configurazione.
3. Che cosa e una VLAN [[Che cosa e una VLAN]]
4. Gestione delle VLAN si tratta di tutto quello che riguarda la categorizzazione delle rete e la loro struttura, 

---
## Collegamenti
- Torna al corso: [[Dashboard H-NET]]