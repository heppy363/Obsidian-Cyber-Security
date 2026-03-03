---
tipo: nota_lezione
corso: "Programmazione"
tags: [uni, programmazione, appunti, Completed]
creato: 2026-03-03 21:38
---

# 📝 Lezione: Il Set di Istruzioni (ISA - Instruction Set Architecture)
**Corso:** [[Programmazione]]

---
## Contenuto
La CPU non "capisce" i concetti; reagisce a impulsi elettrici. L'**Instruction Set** è l'interfaccia tra hardware e software: definisce quali operazioni la CPU può compiere fisicamente.
- **Specificità:** Ogni famiglia di processori ha il suo set (es. **x86** per Intel/AMD, **ARM** per smartphone o processori Apple Silicon). Un programma compilato per x86 non girerà su ARM senza una traduzione, perché i "comandi binari" hanno significati diversi.
- **Tipi di istruzioni:**
    - **Aritmetico-logiche:** Somma, sottrazione, confronti logici (AND, OR).
    - **Trasferimento dati:** Spostare un valore dalla RAM a un registro della CPU o viceversa.
    - **Controllo del flusso:** Saltare a un'altra istruzione (fondamentale per i cicli `if` e `loop`).

---
## Collegamenti
- Torna al corso: [[Programmazione]]