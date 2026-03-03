---
tipo: nota_lezione
corso: "Programmazione"
tags: [uni, programmazione, appunti, Completed]
creato: 2026-03-03 21:40
---

# 📝 Lezione: Il Ciclo di Macchina Fetch-Decode-Execute
**Corso:** [[Programmazione]]

---
## Contenuto
Questo ciclo avviene miliardi di volte al secondo (la frequenza in **GHz** del tuo PC indica proprio quanti cicli di clock avvengono in un secondo).
1. **Fetch (Prelievo):** La CPU consulta un registro speciale chiamato **Program Counter (PC)**, che contiene l'indirizzo della prossima istruzione in RAM. L'istruzione viene copiata dalla RAM all'interno della CPU (nel registro delle istruzioni).
2. **Decode (Decodifica):** L'unità di controllo (CU) analizza i bit ricevuti. Deve capire se quel codice binario significa "somma", "scrivi" o "salta".
3. **Execute (Esecuzione):** L'operazione viene compiuta. Se è un calcolo, entra in gioco l'**ALU (Arithmetic Logic Unit)**. Il risultato può essere memorizzato in un registro o inviato nuovamente alla RAM.

- [[Sistemi di ottimizzazione per il ciclo Fetch-Decode-Execute]]

---
## Collegamenti
- Torna al corso: [[Programmazione]]