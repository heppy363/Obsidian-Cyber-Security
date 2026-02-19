---
aliases:
  - Completate
tags:
  - Completed
  - Algoritmi
  - CompTIAnetwork
  - Certificati
---
--- 
## Nozioni
### 1. Il Concetto Base: Il Rilassamento (Relaxation)
Il concetto fondamentale dell'algoritmo è il **rilassamento degli archi**. Immagina di avere due nodi, **U** e **V**.
- Conosci già una distanza per arrivare a **V**, chiamiamola `D(V)`.
- Conosci la distanza per arrivare a **U**, `D(U)`.
- Esiste un arco che collega **U** a **V** con un peso `W`.

Il rilassamento dice: _Se la strada per arrivare a V passando da U è più breve della strada che già conosco per V, allora aggiorno il mio percorso._ **Formula:** `Se D(U) + W < D(V), allora D(V) = D(U) + W`.

### 2. I Passaggi dell'Algoritmo (Step-by-Step)
Supponiamo di avere un grafo con **V** nodi e **E** archi.
#### Fase 1: Inizializzazione
1. Si imposta la distanza del nodo sorgente (il router stesso) a **0**.
2. Si impostano le distanze di tutti gli altri nodi a **infinito** (∞).
3. Si crea una tabella di routing vuota o con i valori iniziali.

#### Fase 2: Iterazioni (Il cuore del calcolo)
L'algoritmo esegue il rilassamento di **tutti gli archi** del grafo per un numero di volte pari a **(V - 1)**. _Perché V-1?_ Perché il cammino più lungo possibile tra due nodi in un grafo senza cicli ha al massimo V−1 archi.
- **Iterazione 1:** Trova i cammini minimi lunghi al massimo 1 arco.
- **Iterazione 2:** Trova i cammini minimi lunghi al massimo 2 archi.
- ... e così via fino a **V-1**.

In ogni iterazione, il router esamina ogni singola connessione nota e aggiorna la sua tabella se trova una metrica inferiore.
#### Fase 3: Controllo dei Cicli Negativi (Opzionale nel Routing)
Dopo le V−1 iterazioni, l'algoritmo esegue un ultimo passaggio su tutti gli archi. Se è ancora possibile rilassare un arco (trovare una distanza minore), significa che esiste un **ciclo negativo** (un loop dove il costo diminuisce all'infinito).
- Nel routing standard questo non accade perché i costi (hop) sono sempre positivi, ma matematicamente è un passaggio cruciale.

### 3. Come il RIP applica Bellman-Ford
Nel contesto del protocollo RIP, l'algoritmo diventa **distribuito**.
1. **Vettore di Distanza:** Ogni router mantiene un vettore (un array) che contiene la distanza da sé stesso a tutte le reti conosciute.
2. **Scambio di Informazioni:** Ogni 30 secondi, il router invia il suo intero vettore ai vicini.
3. **Aggiornamento Locale:** Quando un router riceve il vettore dal vicino:
    - Aggiunge il costo per raggiungere quel vicino (nel RIP è sempre +1 hop) a tutte le distanze nel vettore ricevuto.
    - Confronta questi nuovi valori con la propria tabella attuale.
    - Se il nuovo valore è più basso, aggiorna la tabella e imposta quel vicino come "Next Hop".
    - Se il valore è uguale o superiore, non fa nulla (o aggiorna solo se il messaggio proviene dallo stesso Next Hop già in tabella, per gestire eventuali peggioramenti della linea).

### 4. Un Esempio Pratico
Immagina tre router: **A --- B --- C**.
1. All'inizio, **A** sa che la rete collegata a **C** è a distanza ∞.
2. **C** dice a **B**: "Raggiungo la mia rete locale a costo 0".
3. **B** riceve il messaggio, aggiunge 1 (il salto verso C) e aggiorna la sua tabella: "Rete C via B, costo 1".
4. Al prossimo ciclo, **B** dice ad **A**: "Raggiungo la rete C a costo 1".
5. **A** riceve il messaggio, aggiunge 1 e scrive: "Rete C via B, costo 2".

### 5. Punti di Forza e Debolezze
- **Semplicità:** Il router non ha bisogno di conoscere l'intera topologia della rete, deve solo fidarsi di ciò che dicono i vicini ("Routing by rumor").
- **Lentezza (Convergenza):** Poiché l'informazione deve propagarsi passo dopo passo (un'iterazione a ogni scambio), in reti grandi ci vuole molto tempo prima che tutti i router siano allineati.
- **Il problema del "Count to Infinity":** Se un link cade, i router potrebbero continuare ad aumentarsi il costo a vicenda in un loop infinito, motivo per cui il RIP imposta il limite massimo (infinito) a **15**.
![[algoritmodi1.jpg]]

### Complessita computazione 
- temporale (worst case) $O(V * E )$   
	- dove $V$ -> e il numero degli vertici e $E$ e il numero degli archi  
- Complessita spaziale $O(V)$ dato che e necessario memorizzare tutto il numero dei vertici 


 ## Link 
1) 