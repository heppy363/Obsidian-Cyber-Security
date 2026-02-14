---
aliases:
  - Completate
tags:
  - Completed
  - CompTIAnetwork
  - Certificati
---
--- 
## Nozioni
`Esposizione di come si calcolo il CRC ovvero il valore che va inserito nel FRS del livello 2`
> per i calcoli si tiene in considerazione lo standard IEEE 802.03 a 32 bit


Il concetto fondamentale del intera operazione matematica e quello dello _XRO_ esclusivo _SENZA_ il carry quindi:
- 0⊕0=0
- 1⊕1=0
- 0⊕1=1
- 1⊕0=1

### Passaggi per il calcolo
##### 1. La Rappresentazione Polinomiale
Ogni sequenza di bit può essere vista come un polinomio dove i bit sono i coefficienti. Se il tuo messaggio è `1101`, il polinomio M(x) sarà:

$$
1x^3+1x^2+0x^1+1x^0⇒x3+x2+1
$$
Il **Polinomio Generatore G(x)** è uno standard fisso (es. il CRC-32 usato in Ethernet). Per il nostro esempio, usiamo un divisore semplice: `1011` (x3+x+1). Il suo grado n è **3** (perché la potenza massima è x3).[[Spiegazione standar G(X)]]
##### 2. Traslazione (Padding)
Prima di dividere, dobbiamo fare spazio per il resto. Aggiungiamo al messaggio tanti zeri quanti ne indica il grado n del generatore.
- Messaggio originale: `1101`
- Grado n=3: aggiungiamo tre zeri ⇒ `1101000`
##### 3. La Divisione Bit a Bit (Algoritmo XOR)
Questa è la parte dove spesso ci si confonde. Nella divisione binaria per il CRC:
1. Si guarda il primo bit a sinistra.
2. Se è **1**, si scrive **1** nel quoziente e si esegue lo **XOR** tra il divisore e i bit del messaggio.
3. Se è **0**, si scrive **0** nel quoziente e si esegue lo **XOR** con una stringa di zeri.
4. Si "abbassa" il bit successivo (proprio come nelle divisioni normali) e si ripete.
#### Esempio Pratico: `1101000` diviso `1011`
```
1110  (Quoziente - spesso ignorato nel CRC)
    __________
1011| 1101000
      1011     <-- XOR (perché il primo bit è 1)
      ----
      01100    <-- Risultato XOR + abbasso uno '0'
       0000    <-- Il primo bit era 0, quindi XOR con zeri
       ----
       11000   <-- Risultato + abbasso uno '0'
       1011
       ----
       01110   <-- Risultato + abbasso l'ultimo '0'
        1011
        ----
        0101   <-- RESTO FINALE (CRC)
```
Il resto è **101**, che è il nostro CRC.
##### 4. Costruzione del Frame e Verifica
Il mittente sostituisce i tre zeri iniziali con il resto appena calcolato. Il frame inviato sarà: `1101` + `101` = **`1101101`**.
**Perché al destinatario deve venire zero?** Matematicamente, è come se avessimo fatto: Messaggio−Resto. In aritmetica modulo 2, sommare e sottrarre sono la stessa cosa (lo XOR è l'inverso di se stesso). Quindi, se il destinatario divide `1101101` per `1011`, la divisione finirà esattamente con **resto 000**.

##### Perché si usa questo metodo invece di una semplice somma?
Una somma (checksum) potrebbe non rilevare errori se due bit si invertono contemporaneamente annullandosi a vicenda. La divisione polinomiale (CRC) è molto più potente: riesce a rilevare quasi il **100%** degli errori di tipo "burst" (scariche di rumore che colpiscono più bit consecutivi), tipici dei cavi in rame.


> **Curiosità:** Se durante il volo un bit cambia (es. il frame diventa `1101111`), la divisione al destinatario non darà più zero. Il sistema "capisce" che c'è stato un errore e scarta il frame.


## Link 
1) 