---
tipo: nota_lezione
corso: Proxmox
tags:
  - progetto
  - proxmox
  - Completed
  - Algoritmi
creato: 2026-02-19 09:54
---

# 📝 Lezione: Algoritmo XSF B+ Trees
**Corso:** [[Proxmox]]

---
## Contenuto
`Il segreto di XFS risiede nell'abbandono delle strutture lineari a favore di strutture ad albero altamente ottimizzate.

## 1. Algoritmo di Allocazione: B+ Trees
A differenza di file system come ext2/ext3 che usano mappe di bit (bitmap) per tracciare i blocchi liberi, XFS utilizza due **B+ Trees** per ogni _Allocation Group_ (AG).
- **B+ Tree per Offset:** Organizza i blocchi liberi in base al loro indirizzo fisico. È fondamentale per trovare blocchi vicini a quelli già occupati (minimizzando i movimenti della testina del disco).
- **B+ Tree per Dimensione:** Organizza i blocchi liberi in base alla grandezza del "buco" disponibile.
    - **L'algoritmo:** Quando il kernel deve scrivere un file di 500MB, interroga l'albero per dimensione per trovare istantaneamente l'extent (spazio contiguo) più piccolo che possa contenere il file (**Best-fit algorithm**), evitando di spezzettarlo.

## 2. Gestione degli Inode: Allocazione Dinamica
In molti file system (come ext4), il numero di Inode (i descrittori dei file) è fisso al momento della formattazione. Se finisci gli inode, non puoi più creare file anche se hai spazio su disco.
XFS usa un algoritmo di **Allocazione Dinamica degli Inode**:
- Gli inode sono organizzati in **B+ Trees dedicati**.
- Vengono creati "chunks" di inode on-demand.
- **Algoritmo di lookup:** Grazie alla struttura ad albero, la ricerca di un file in una directory con milioni di elementi ha una complessità temporale di O(logn), rendendo l'accesso quasi istantaneo indipendentemente dalla dimensione della cartella.

## 3. Algoritmo di Delayed Allocation (Allocazione Ritardata)
Questo è forse l'algoritmo più intelligente di XFS. Invece di decidere dove scrivere i dati nel momento in cui l'applicazione chiama `write()`, XFS:
1. Riserva lo spazio nella memoria virtuale (RAM).
2. Mantiene i dati "sporchi" (non ancora scritti) in cache.
3. Solo quando il sistema deve fare il _flush_ (perché la RAM è piena o è passato troppo tempo), l'algoritmo analizza la dimensione totale del file accumulato e cerca il blocco di spazio contiguo perfetto.

**Risultato matematico:** Si massimizza la lunghezza degli _extents_ e si riduce drasticamente il numero di frammenti del file.

## 4. Concorrenza: L'algoritmo degli Allocation Groups
Qui passiamo dal calcolo sequenziale a quello parallelo. Se hai un server con 64 CPU, non vuoi che tutte aspettino che una singola tabella di allocazione si sblocchi.
XFS implementa un algoritmo di **locking granulare**:
- Il disco è diviso in N Allocation Groups.
- Ogni AG agisce come un file system indipendente con i propri lock.
- **Algoritmo di hashing:** Quando più processi scrivono contemporaneamente, XFS li indirizza verso AG diversi usando algoritmi di bilanciamento del carico, permettendo operazioni di scrittura parallele reali sull'hardware sottostante.

## 5. Algoritmo di Journaling (Log-structured)
Il journaling di XFS è "asincrono" e limitato ai **metadati**.
- Invece di scrivere subito le modifiche alla struttura del disco (che richiederebbe molti spostamenti della testina), XFS scrive le modifiche in un log circolare in modo sequenziale (molto veloce).
- Un processo in background (il _log manager_) si occupa poi di applicare queste modifiche alla struttura principale del file system con calma.
- In caso di crash, l'algoritmo di **Recovery** legge il log dall'ultima posizione nota e applica solo le operazioni mancanti, garantendo la coerenza in pochi secondi.

---
## Collegamenti
- Torna al corso: [[Proxmox]]