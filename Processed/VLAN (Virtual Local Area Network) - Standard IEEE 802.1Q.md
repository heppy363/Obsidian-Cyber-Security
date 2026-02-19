---
tipo: nota_lezione
corso: "Dashboard CompTIA Network+"
tags: [progetto, CompTIANetwork, certificazioni, Completed]
creato: 2026-02-19 15:44
---

# 📝 Lezione: VLAN (Virtual Local Area Network) - Standard IEEE 802.1Q
**Corso:** [[Dashboard CompTIA Network+]]

---
## Contenuto
Le VLAN permettono di segmentare una rete fisica in più reti logiche indipendenti.
- **A cosa servono:** Immagina un ufficio con i reparti "Contabilità" e "Ospiti". Non vuoi che un ospite possa accedere ai server della contabilità. Invece di comprare due switch separati e tirare due set di cavi, usi uno switch **Managed** (gestito) e crei due VLAN.
- **Come funzionano (Tagging):** Quando un frame si muove all'interno dello switch tra porte della stessa VLAN, non succede nulla di speciale. Ma se deve passare attraverso un cavo che collega due switch (chiamato **Trunk**), lo switch aggiunge un "tag" (un'etichetta) al frame.
- **Il Tag 802.1Q:** È un campo di **4 byte** inserito tra il MAC sorgente e il campo EtherType. Contiene il **VLAN ID** (un numero da 1 a 4094).
- **Vantaggi:** * **Sicurezza:** I dati sono isolati.
    - **Riduzione del traffico:** I broadcast (es. ARP) vengono inviati solo ai membri della stessa VLAN, non a tutta l'azienda.

---
## Collegamenti
- Torna al corso: [[Dashboard CompTIA Network+]]