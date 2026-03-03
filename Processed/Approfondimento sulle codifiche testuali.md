---
tipo: nota_lezione
corso: "Programmazione"
tags: [uni, programmazione, appunti, Completed]
creato: 2026-03-03 21:33
---

# 📝 Lezione: Approfondimento sulle codifiche testuali 
**Corso:** [[Programmazione]]

---
## Contenuto
## 1. ASCII (7-bit)
Nata negli anni '60, l'**ASCII** (_American Standard Code for Information Interchange_) è la "madre" di tutte le codifiche moderne.
- **Funzionamento:** Utilizza **7 bit** per ogni carattere. Questo significa che può rappresentare un totale di 27=128 simboli.
- **Caratteristiche:**
    - I codici da **0 a 31** sono "caratteri di controllo" (non stampabili), come il _Null_, il _Bell_ (un segnale acustico) o il _Line Feed_ (vai a capo).
    - I codici da **32 a 127** includono lo spazio, la punteggiatura, i numeri (0-9) e l'alfabeto inglese (maiuscolo e minuscolo).
- **Peculiarità:** È estremamente efficiente in termini di spazio, ma ha un limite invalicabile: **non esistono accenti** o caratteri non inglesi. Per un computer ASCII puro, parole come "caffè" o "perché" sono impossibili da codificare correttamente.

---
## 2. ASCII Esteso e ISO-8859 (8-bit)
Per superare i limiti dei 7 bit, si è passati all'uso dell'intero **Byte (8 bit)**.
- **Funzionamento:** Utilizza **8 bit**, raddoppiando le combinazioni disponibili a 28=256.
- **Caratteristiche:**
    - I primi 128 caratteri restano identici all'ASCII originale.
    - I successivi 128 (da 128 a 255) vengono usati per simboli matematici, grafici e, soprattutto, **lettere accentate**.
- **Peculiarità (Il problema dei "Code Pages"):** Poiché 256 caratteri non bastano per tutte le lingue del mondo, sono nate diverse varianti chiamate "pagine di codice".
    - **ISO-8859-1 (Latin-1):** Usata in Europa Occidentale (include `ò`, `è`, `á`).
    - **ISO-8859-5:** Usata per l'alfabeto cirillico.
- **Il disastro dei "Mojibake":** Se salvavi un file con ISO-8859-1 e lo aprivi con un programma che usava ISO-8859-5, le tue lettere accentate diventavano caratteri russi a caso.
---
## 3. UNICODE: L'Integrazione Universale
Per risolvere il caos delle pagine di codice, è stato creato il consorzio **Unicode**. L'obiettivo è assegnare un numero univoco (chiamato **Code Point**) a ogni singolo carattere di ogni lingua, passata o presente.
I Code Point di Unicode sono scritti solitamente in esadecimale con il prefisso `U+`. Ad esempio, la "A" è `U+0041`, mentre l'emoji della pizza 🍕 è `U+1F355`.
Esistono diversi modi (trasformazioni) per scrivere questi numeri in bit:
### UTF-32 (4 Byte fissi)
- **Come funziona:** Ogni singolo carattere occupa sempre **32 bit** (4 byte).
- **Caratteristiche:** È semplicissimo per il computer (ogni carattere ha la stessa dimensione), ma è **estremamente inefficiente**: un testo inglese occuperebbe il quadruplo dello spazio rispetto all'ASCII, poiché quasi tutti i bit sarebbero zeri inutilizzati.
### UTF-16 (2 o 4 Byte)
- **Come funziona:** Usa blocchi di 16 bit. I caratteri più comuni occupano 2 byte, quelli rarissimi 4.
- **Peculiarità:** È il formato interno usato da **Windows** e **Java**.
### UTF-8 (Lunghezza Variabile - Lo Standard del Web)
È la codifica più intelligente e utilizzata oggi al mondo.
- **Come funziona:** Usa da **1 a 4 byte** per carattere.
- **Caratteristiche e Peculiarità:**
    1. **Retrocompatibilità:** Se un file contiene solo caratteri ASCII (inglese), il file UTF-8 è **identico** bit per bit a un file ASCII. Questo lo ha reso lo standard universale.
    2. **Efficienza:** Usa solo 1 byte per l'alfabeto latino, 2 byte per arabo o greco, 3 byte per cinese/giapponese e 4 byte per emoji e simboli rari.
    3. **Self-Synchronizing:** Se un byte viene corrotto durante la trasmissione, il computer può capire dove inizia il carattere successivo senza perdere tutto il resto del testo.

---
### Confronto di Riepilogo
**Curiosità per i tuoi appunti:** Quando vedi in un sito web dei quadratini bianchi o dei punti di domanda al posto delle lettere, significa che il browser sta cercando di leggere un file codificato in un modo (magari UTF-8) interpretandolo con una tabella diversa (magari ASCII), oppure che il font che stai usando non ha "disegnato" il simbolo corrispondente a quel codice Unicode.

---
## Collegamenti
- Torna al corso: [[Programmazione]]