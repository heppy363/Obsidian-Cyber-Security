---
tipo: nota_lezione
corso: "Programmazione"
tags: [uni, programmazione, appunti, Completed]
creato: 2026-03-03 21:24
---

# 📝 Lezione: Esempio di floating point 
**Corso:** [[Programmazione]]

---
## Contenuto
Prendiamo come esempio il numero decimale: **−12,625**

---
### Passo 1: Conversione in binario del valore assoluto
Dobbiamo convertire separatamente la parte intera e la parte frazionaria di 12,625.
1. **Parte intera (12):** * 12/2=6 (resto 0)
    - 6/2=3 (resto 0)
    - 3/2=1 (resto 1)
    - 1/2=0 (resto 1)
    - Risultato: 11002​
2. **Parte frazionaria (0,625):** Si moltiplica per 2 e si prende la parte intera.
    - 0,625×2=1,25 (prendo 1, resta 0,25)
    - 0,25×2=0,5 (prendo 0, resta 0,5)
    - 0,5×2=1,0 (prendo 1, resta 0)
    - Risultato: 1012​

Quindi, 12,62510​=1100,1012​

---
### Passo 2: Normalizzazione
In binario, un numero è normalizzato se si presenta nella forma 1,f×2e. Dobbiamo quindi spostare la virgola a sinistra finché non rimane solo un "1" prima della virgola.
- Da 1100,101 spostiamo la virgola di **3 posizioni** a sinistra:
- Otteniamo: 1,100101×23
Da qui estraiamo due informazioni critiche:
- La **Mantissa** (la parte dopo la virgola): `100101`
- L'**Esponente** grezzo: 3

---

### Passo 3: Compilazione dei 32 bit
#### 1. Bit di Segno (1 bit)
Il numero originale è −12,625 (negativo).
- **Segno = 1** (Se fosse stato positivo sarebbe stato 0).
#### 2. Esponente Polarizzato (8 bit)
Lo standard IEEE 754 non usa il complemento a 2 per l'esponente, ma un **eccesso (bias) di 127**.
- Calcolo: 127+Esponente grezzo=127+3=130
- Convertiamo 130 in binario: 10000010
- **Esponente = 10000010**
#### 3. Mantissa (23 bit)
Prendiamo la parte frazionaria della normalizzazione (`100101`) e aggiungiamo tanti zeri a destra fino a coprire i 23 bit richiesti.
- **Mantissa = 10010100000000000000000**

---

### Risultato Finale (Rappresentazione in Memoria)
Unendo i pezzi otteniamo la sequenza di 32 bit:

---

### Perché si usa il "Bias" di 127?
Si usa per permettere alla CPU di confrontare velocemente due numeri a virgola mobile. Se l'esponente fosse in complemento a 2, i numeri negativi (esponenti molto piccoli) sembrerebbero numeri binari molto grandi, confondendo i circuiti di confronto. Con il bias di 127, l'esponente più piccolo possibile (2−126) diventa quasi zero, e quello più grande diventa quasi 255, mantenendo un ordine lineare facile da gestire per l'hardware.

---
## Collegamenti
- Torna al corso: [[Programmazione]]