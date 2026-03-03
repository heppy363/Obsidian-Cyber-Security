---
tipo: nota_lezione
corso: "Programmazione"
tags: [uni, programmazione, appunti, Completed]
creato: 2026-03-03 20:53
---

# 📝 Lezione: hardware
**Corso:** [[Programmazione]]

---
## Contenuto
L'Hardware rappresenta la componente fisica (toccabile) di un sistema informatico. Quasi tutti i computer moderni si basano sull'**Architettura di von Neumann**, che prevede un'unità di elaborazione, una memoria e canali di comunicazione (bus).
### 1.1 CPU (Central Processing Unit)
La CPU è il "cervello" del computer. Il suo compito è eseguire il ciclo **Fetch-Decode-Execute** (Prelievo, Decodifica, Esecuzione delle istruzioni).
- **Componenti Interni:** Si divide in **ALU** (Arithmetic Logic Unit) per i calcoli matematici e logici, e **CU** (Control Unit) per coordinare le operazioni.
- **Registri:** Piccole memorie ad altissima velocità interne alla CPU (es. il Program Counter che punta alla prossima istruzione).
- **Nota Storica:** L'**ENIAC** (1945) fu uno dei primi computer general-purpose, ma era basato su valvole termoioniche e non aveva il concetto di "programma memorizzato" come i PC moderni.
- ogni CPU ha il suo [[Il Set di Istruzioni (ISA - Instruction Set Architecture)]]

### 1.2 La Gerarchia di Memoria
Il sistema gestisce i dati attraverso diversi livelli, bilanciando velocità e capacità.
- **RAM (Random Access Memory):**
    - **Volatilità:** Perde i dati senza alimentazione.
    - **Accesso Casuale:** Il tempo per accedere a una cella di memoria è costante (O(1)), indipendentemente dalla sua posizione fisica.
    - **Ruolo:** Contiene il codice del Sistema Operativo e i dati dei programmi in esecuzione.
- **Memoria di Massa (Storage):**
    - **Persistenza:** Utilizza tecnologie magnetiche (HDD) o flash (SSD) per mantenere i dati permanentemente.
    - **SSD vs HDD:** Gli SSD sono preferiti oggi per l'assenza di parti mobili e velocità di input/output (I/O) superiori.
- **Memorie Esterne:** Dispositivi collegati tramite bus seriali come l'**USB** (Universal Serial Bus) o **Thunderbolt**, trattati dal sistema come unità logiche rimovibili.
![[licensed-image.jpg]]
### 1.3 Periferiche di Input/Output (I/O)
- **Input:** Trasformano segnali fisici in dati digitali (Tastiera, Mouse, Microfono, Scanner).
- **Output:** Traducono dati digitali in segnali comprensibili all'utente (Monitor, Stampanti, Altoparlanti).
- **Dispositivi I/O Ibridi:** Le memorie di massa o le schede di rete sono considerati dispositivi di I/O poiché leggono (input) e scrivono (output) dati costantemente.



---
## Collegamenti
- Torna al corso: [[Programmazione]]