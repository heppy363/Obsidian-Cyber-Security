---
tipo: nota_lezione
corso: "Programmazione"
tags: [uni, programmazione, appunti, Completed]
creato: 2026-03-03 20:54
---

# 📝 Lezione: software
**Corso:** [[Programmazione]]

---
## Contenuto
Il Software è l'insieme di istruzioni logiche che dicono all'hardware cosa fare.
### 2.1 Software di Sistema (Il Sistema Operativo)
Il **Sistema Operativo (SO)** funge da intermediario tra l'utente e l'hardware (User ↔ SW Applicativo ↔ **SO** ↔ HW).
- **Kernel:** Il cuore del SO. Gestisce la CPU (scheduling dei processi), la memoria RAM (paginazione) e l'accesso ai file.
- **Esempi:** Windows (Kernel NT), macOS (basato su Unix/Darwin), Linux (Kernel Open Source).
- **Utility Software:** Programmi "di servizio" come antivirus, strumenti di deframmentazione o compressione (ZIP/RAR). Essi ottimizzano le performance senza essere parte del "lavoro finale" dell'utente.
### 2.2 Strumenti di Sviluppo e Traduzione
Poiché l'hardware capisce solo il **Linguaggio Macchina** (sequenze di 0 e 1), il codice scritto dai programmatori deve essere tradotto.
1. **Assembler:** Traduce il linguaggio Assembly (quasi identico al linguaggio macchina ma leggibile dall'uomo) in codice binario.
2. **Compilatori (es. C, C++):** Analizzano l'intero codice sorgente e generano un file **eseguibile** (.exe). Sono efficienti perché la traduzione avviene una sola volta.
3. **Interpreti (es. Python, PHP):** Traducono ed eseguono il codice riga per riga. Sono più flessibili per il debug ma generalmente più lenti dei compilati.
### 2.3 Software Applicativo
Sono i programmi destinati all'utente finale per svolgere compiti specifici.
- **Produttività:** Word, Excel, Obsidian.
- **Comunicazione:** Client Email (Outlook, Thunderbird), Browser Web (Chrome, Firefox).
- **Multimediale:** Video editor, player musicali.

---
## Collegamenti
- Torna al corso: [[Programmazione]]