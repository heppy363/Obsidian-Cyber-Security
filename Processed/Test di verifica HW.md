---
tipo: nota_lezione
corso: "Dashboard H-NET"
tags: [progetto, hNet, Completed]
creato: 2026-02-22 12:34
---

# 📝 Lezione: Test di verifica HW
**Corso:** [[Dashboard H-NET]]

---
## Contenuto

#### **1. Cronologia degli Interventi e Troubleshooting**
**Fase A: Analisi Compatibilità Iniziale**
- **Verifica RAM:** È stata confermata la necessità di utilizzare memorie **RDIMM ECC Registered** per la scheda madre Supermicro, escludendo l'uso delle schede consumer (ASUS/Intel X79) che non avrebbero supportato tale tipologia di memoria.
- **Verifica Socket:** Confermata la compatibilità del socket LGA 2011 "Square ILM" per il dissipatore EKL.

**Fase B: Diagnostica Segnali Acustici (Beep Codes)** Durante i primi avvii, il sistema ha presentato diversi segnali di errore:
- **Errore 1 (2 bip brevi + 1 bip):** Identificato come mancata inizializzazione della memoria o assenza di segnale video. Risolto installando la GPU GTX 1050.
- **Errore 2 (2 bip + pausa + 2 bip):** Identificato come "Circuit Test Failure" o errore critico di rilevamento RAM.

**Fase C: Procedura di Isolamento RAM e Reset** Per risolvere il blocco al boot (schermo nero e assenza di risposta del tasto Caps Lock):
1. **Reset CMOS:** Rimozione della batteria tampone e scarico dell'energia residua per riportare il BIOS alle impostazioni di fabbrica.
2. **Test Modulo Singolo:** È stata avviata la procedura di test installando un solo banco di RAM alla volta nello slot primario (**DIMMA1**).
3. **Pulizia Contatti:** Pulizia dei contatti dorati dei moduli RAM per eliminare residui che impedivano la corretta conducibilità.

**Fase D: Identificazione del Guasto**
- **Rilevamento banco difettoso:** Attraverso il test incrociato degli 8 moduli, è stato individuato **un banco di RAM da 16GB non funzionante**.
- **Risultato:** Rimosso il modulo guasto, il sistema ha completato con successo la fase di POST (Power-On Self-Test) con **112 GB** di memoria funzionante.

#### **2. Verifiche di Corretto Montaggio**
- **Pressione Socket:** Abbiamo monitorato la pressione del dissipatore sul socket LGA 2011, assicurandoci che non fosse eccessiva per non causare micro-flessioni della scheda madre (causa comune di mancata lettura dei canali RAM).
- **Alimentazione CPU:** Verificata la corretta inserzione del connettore 8-pin EPS per fornire la potenza necessaria allo Xeon (TDP 130W).
- **Stato LED:** Confermata l'operatività del chip BMC tramite il LED verde lampeggiante ("Heartbeat") sulla scheda madre.

#### **3. Stato Attuale dell'Hardware**
- **BIOS:** Accessibile e configurato.
- **CPU:** Riconosciuta correttamente dal sistema.
- **RAM:** 112 GB riconosciuti e operativi in configurazione Quad-Channel (stabile).
- **Output Video:** Funzionante tramite scheda dedicata nello slot PCIe.




---
## Collegamenti
- Torna al corso: [[Dashboard H-NET]]