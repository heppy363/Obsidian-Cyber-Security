---
tipo: nota_lezione
corso: "Dashboard H-NET"
tags: [progetto, hNet, Completed]
creato: 2026-02-24 22:31
---

# 📝 Lezione: Componentistica UPS
**Corso:** [[Dashboard H-NET]]

---
## Contenuto

### 1. Per il PC Personale (Windows)
Il modello **Epyc NYTRO 1500VA (circa 145€)** è la scelta migliore.
- **Software:** Utilizza un software chiamato _ViewPower_.
- **Funzionamento:** Colleghi l'UPS al PC tramite il cavo USB incluso. Nel software imposti: _"Spegni il PC quando la batteria scende sotto il 20%"_ (o dopo X minuti).
- **Sicurezza:** Il software forza la chiusura delle applicazioni aperte e spegne Windows correttamente, evitando danni al file system.

### 2. Per l'Home Lab (Mini PC + Server di calcolo)
Qui la situazione è più complessa perché hai più macchine attaccate a un solo UPS. Ti serve il modello **VulTech UPS1500VA-PURE (circa 150€)** o il **Green Cell 1500VA**.
- **Il Problema:** L'UPS ha una sola porta USB, ma tu hai 4 macchine (3 mini PC + 1 server).
- **La Soluzione (NUT - Network UPS Tools):**
    1. Colleghi l'USB dell'UPS al **Server di calcolo** (che farà da "Master").
    2. Installi un software gratuito chiamato **NUT** (molto comune su Linux/Proxmox).
    3. Il Server Master comunica agli altri 3 Mini PC (i "Slave") via rete locale che la corrente è saltata.
    4. Tutte le macchine iniziano la procedura di shutdown contemporaneamente.

### 3. Per il NAS Ugreen
L'UPS dedicato della Ugreen da 120W è già predisposto per comunicare direttamente con il sistema operativo del NAS (UGOS).
- **Integrazione:** Basta collegare il cavo USB dell'UPS alla porta USB del NAS. Nel pannello di controllo del NAS troverai la sezione "Hardware e Alimentazione" dove potrai attivare lo spegnimento automatico o la "Modalità provvisoria".

### Riassunto della Strategia di Shutdown

|Linea|Dispositivo "Master"|Software Consigliato|Configurazione|
|---|---|---|---|
|**PC Personale**|Il tuo PC (Windows)|**ViewPower**|Shutdown diretto via USB|
|**Home Lab**|Server di Calcolo|**NUT (Network UPS Tools)**|Il Server spegne se stesso e i 3 mini PC via LAN|
|**NAS**|NAS Ugreen|**Nativo (UGOS)**|Shutdown automatico via USB dedicata|


### Cosa devi controllare prima dell'acquisto:
1. **Porte USB:** Assicurati che ogni UPS che compri (Epyc o VulTech) abbia la **porta USB di comunicazione** (non solo quelle di ricarica per i cellulari). I modelli che ti ho indicato ce l'hanno.
2. **Cavi di rete:** Per lo spegnimento dell'Home Lab, lo switch deve essere collegato allo stesso UPS dei server, altrimenti se manca corrente lo switch si spegne, la rete cade e il "Master" non può dire ai "Mini PC" di spegnersi!

## Collegamenti
- Torna al corso: [[Dashboard H-NET]]