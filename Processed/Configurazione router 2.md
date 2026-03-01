---
tipo: nota_lezione
corso: "Dashboard H-NET"
tags: [progetto, hNet, Completed]
creato: 2026-02-26 21:43
---

# 📝 Lezione: Configurazione router 2
**Corso:** [[Dashboard H-NET]]

---
## Contenuto
### 1. La scelta del PC: Lenovo ThinkCentre M720q Tiny
Dopo aver valutato i modelli più vecchi (M710q, M910q, M910x), abbiamo scelto l'**M720q** per tre motivi fondamentali:
- **Compatibilità garantita:** A differenza dei modelli precedenti, l'M720q ha sempre il connettore PCIe saldato sulla scheda madre.
- **Potenza (i3-8100T):** Passiamo a 4 core fisici reali (8ª generazione), ideali per gestire il traffico Gigabit e pacchetti pesanti su pfSense.
- **Efficienza:** Il modulo "T" e l'alimentatore da **65W** assicurano consumi ridotti (10-12W in idle), perfetti per un dispositivo acceso 24/7.

### 2. L'espansione di rete: Scheda Silicom (Intel i350-T2)
Abbiamo individuato la scheda **Silicom PE2G2I35V**:
- Utilizza il chipset **Intel i350**, il "gold standard" per pfSense grazie alla stabilità dei driver.
- Offre **due porte Gigabit** supplementari, permettendoti di dedicare la scheda Intel alla WAN e alla LAN, lasciando la porta integrata del PC per emergenza o management.

### 3. Il componente chiave: Riser PCIe 01AJ929
Abbiamo verificato la compatibilità del pezzo meccanico:
- Il codice **01AJ929** è quello corretto per la serie **Tiny5** (M720q).
- È l'adattatore indispensabile per installare fisicamente la scheda di rete "sdraiata" all'interno del case ultra-compatto del Lenovo.

### 4. Analisi dei costi e fattibilità
Siamo riusciti a far rientrare tutto nel budget previsto:
- **PC completo** (RAM 8GB, SSD 128GB, Alimentatore 65W): ~120€
- **Riser PCIe 01AJ929**: ~20€
- **Scheda Intel i350-T2**: ~35-40€
- **Totale**: **~175-180€**

---
## Collegamenti
- Torna al corso: [[Dashboard H-NET]]