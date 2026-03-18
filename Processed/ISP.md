---
tipo: nota_lezione
corso: "Dashboard Networking Basics"
tags: [progetto, certificazioni, networkingBasics, Completed]
creato: 2026-03-16 16:09
---

# 📝 Lezione: ISP
**Corso:** [[Dashboard Networking Basics]]

---
## Contenuto

## 1. Il ruolo dell'ISP
L'**Internet Service Provider** è il ponte tra la tua rete locale e l'Internet globale. Gli ISP sono collegati tra loro in modo gerarchico per garantire che i dati prendano la strada più breve.
- **Servizi aggiuntivi:** Oltre alla connessione, molti ISP offrono hosting Web, email, archiviazione di rete (FTP) e supporto tecnico.
- **Internet Backbone:** È la "superstrada" dell'informazione, composta da cavi in **fibra ottica** ad altissima velocità che collegano continenti e grandi città, anche sotto l'oceano.

## 2. Opzioni di Connessione per Utenti SOHO
Le tecnologie variano in base alla posizione geografica e all'infrastruttura esistente:

|Tecnologia|Caratteristiche Principali|Mezzo Fisico|
|---|---|---|
|**Cable**|Segnale dati sulla stessa rete della TV broadcast. Alta banda, sempre attiva.|Cavo Coassiale|
|**DSL**|Alta banda, sempre attiva, usa la linea telefonica. Divisa in 3 canali (voce, upload, download).|Doppino in Rame|
|**Cellular**|Usa la rete dei telefoni cellulari. Ottima per la mobilità o aree remote.|Onde Radio|
|**Satellite**|Richiede "linea di vista" libera verso il satellite. Ideale per zone rurali isolate.|Onde Radio / Parabola|
|**Dial-up**|Opzione economica e lenta. Richiede di "chiamare" l'ISP e occupa la linea telefonica.|Linea Telefonica|
|**Fiber**|La più veloce. Molte aree metropolitane hanno ora la fibra direttamente in casa.|Fibra Ottica|


## 3. Sicurezza della Connessione
Cisco sottolinea un punto vitale per un aspirante sistemista:
- **Connessione Diretta (Modem):** Collegare un singolo PC direttamente a un modem è **pericoloso** perché il computer è esposto direttamente alle minacce di Internet.
- **Integrated Router:** È la soluzione standard. Il router agisce come **firewall**, fornisce indirizzi IP interni (DHCP) e integra uno switch e un Access Point Wi-Fi, creando una barriera di sicurezza tra te e l'ISP.

---

## Analisi tecnica per il tuo obiettivo

Visto che vuoi diventare un **Pen Tester**, questo modulo ti insegna dove finisce la tua "giurisdizione" e inizia quella del provider. Quando analizzerai una rete, dovrai sempre identificare se il router/firewall è configurato correttamente o se ci sono dispositivi esposti direttamente (come nel caso del modem singolo), che rappresentano la vulnerabilità più grave.

---
## Collegamenti
- Torna al corso: [[Dashboard Networking Basics]]