---
aliases:
  - Completate
tags:
  - Completed
  - proxmox
  - Linux
---
--- 
## Nozioni
``Se XFS è il "gigante dei dati" nato per il calcolo pesante, **EXT4 (Fourth Extended File System)** è il cavallo di battaglia del mondo Linux. È il file system di default per la stragrande maggioranza delle distribuzioni (Ubuntu, Debian, Fedora).``

Mentre XFS punta tutto sul parallelismo estremo, EXT4 è progettato per un equilibrio perfetto tra **retrocompatibilità, affidabilità e velocità** su scala medio-grande.

## 1. L'Evoluzione: Dal blocco all'Extent
Il salto fondamentale tra EXT3 e EXT4 è stato il passaggio dalla mappatura basata su blocchi a quella basata su **Extent**.
- **In EXT3:** Ogni file era una lista di blocchi singoli. Per un file di 1GB (256.000 blocchi da 4KB), il sistema doveva gestire una tabella enorme di puntatori.
- **In EXT4:** Si usa l'algoritmo degli **Extent**. Un extent è un singolo descrittore che dice: "Dato X, prendi i prossimi n blocchi contigui".
    - Un singolo extent in EXT4 può mappare fino a 128MB di spazio contiguo.
    - Questo riduce drasticamente la dimensione degli Inode e velocizza la lettura di file grandi.

## 2. Struttura Dati: Htree (Hashed B-Tree) per le Directory
Mentre XFS usa B+ Trees ovunque, EXT4 utilizza una struttura chiamata **Htree** specificamente per indicizzare le directory molto popolose.
- **Il problema:** Cercare un file in una cartella con 100.000 file in modo lineare richiederebbe troppo tempo (O(n)).
- **La soluzione:** L'Htree è una versione specializzata di un B-Tree che usa l'**hashing** del nome del file come chiave.
    - Questo permette di trovare l'indirizzo dell'Inode di un file con una complessità quasi costante O(1) o logaritmica molto bassa, rendendo EXT4 estremamente veloce nella gestione di server web o cache di posta.

## 3. Algoritmo di Allocazione: Multi-Block Allocation (mballoc)
In EXT3, l'allocatore di blocchi poteva decidere dove mettere un solo blocco alla volta. EXT4 introduce **mballoc**:
1. Quando il kernel deve scrivere dei dati, mballoc analizza la richiesta totale.
2. Invece di chiamare l'allocatore 1000 volte per 1000 blocchi, effettua una **singola allocazione** per l'intero gruppo di blocchi.
3. **Ottimizzazione:** Questo riduce enormemente il carico sulla CPU e, combinato con la _Delayed Allocation_ (simile a quella di XFS), garantisce che i file siano scritti nel modo più contiguo possibile sul disco fisico.

## 4. Journaling: Il Checksum del Journal
EXT4 è uno dei file system più sicuri grazie al **Journal Checksumming**.
Il journaling (diario) serve a riprendersi dai crash, ma cosa succede se il diario stesso viene scritto male a causa di un guasto hardware?
- **Algoritmo:** EXT4 calcola un checksum (un "riassunto" matematico) di ogni transazione del journal.
- Se dopo un crash il checksum non corrisponde, il sistema sa che il journal è corrotto e non tenta di applicare modifiche errate, evitando di distruggere i dati per "ripararli".

## 5. Caratteristiche "Legacy" e Flessibilità
A differenza di XFS, EXT4 conserva alcune strutture classiche che lo rendono più flessibile per l'utente comune:
- **Block Groups:** Il disco è diviso in gruppi di blocchi, ognuno con la sua tabella degli Inode e la sua bitmap. Questo limita la distanza che la testina di un HDD deve percorrere tra i metadati e i dati.
- **Online Deframmentation:** EXT4 supporta lo strumento `e4defrag`, che permette di deframmentare singoli file o l'intero file system mentre è montato e in uso.
- **Ridimensionamento:** Puoi espandere o **restringere** un volume EXT4 (XFS non può essere ristretto).

## Link 
1) 