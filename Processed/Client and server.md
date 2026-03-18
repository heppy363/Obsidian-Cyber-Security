---
tipo: nota_lezione
corso: "Dashboard Networking Basics"
tags: [progetto, certificazioni, networkingBasics, Completed]
creato: 2026-03-16 16:01
---

# 📝 Lezione: Client and server
**Corso:** [[Dashboard Networking Basics]]

---
## Contenuto
## 1. Ruoli dei Host: Client e Server
Ogni computer collegato a una rete che partecipa alla comunicazione è chiamato **Host**. Il ruolo che un host assume dipende dal **software** installato:
- **Server:** Sono computer dotati di software che permette loro di fornire informazioni (servizi) ad altri dispositivi sulla rete.
    - _Esempi:_ Server Email, Server Web, Server di File.
- **Client:** Sono computer dotati di software che permette loro di richiedere e visualizzare le informazioni ottenute dal server.
    - _Esempio:_ Un browser web (Chrome, Firefox) è un software client che richiede pagine a un server web.

## 2. Reti Peer-to-Peer (P2P)
Nelle reti P2P, un computer può fungere contemporaneamente sia da **client** che da **server**. Non esiste un server dedicato centrale.
- **Vantaggi:**
    - Facile da configurare e meno complessa.
    - Costi ridotti (non servono server dedicati costosi).
    - Ideale per compiti semplici come condividere una stampante o pochi file in una casa o piccolo ufficio.
- **Svantaggi:**
    - **Sicurezza:** Non c'è un'amministrazione centralizzata, quindi è più difficile proteggere i dati.
    - **Prestazioni:** Se un PC fa da server per altri, diventerà più lento per l'utente che lo sta usando.
    - **Scalabilità:** Non è adatta a grandi aziende; con troppi dispositivi diventa ingestibile.

## 3. Ruoli Multipli
Un singolo computer può eseguire più tipi di software client e server contemporaneamente. Ad esempio, mentre guardi una pagina web (Client Web), potresti avere una cartella condivisa con un collega (Server di File) e ricevere messaggi istantanei (P2P Application).

---

## Nota per il tuo percorso da Pentester

Le reti **P2P** sono spesso un "punto debole" nelle aziende. Poiché non c'è un controllo centrale (amministrazione centralizzata), è più facile per un attaccante trovare una cartella condivisa senza password o un PC non aggiornato che funge da server improvvisato. Nel tuo futuro lavoro, mappare queste relazioni sarà fondamentale per capire come muoverti all'interno di una rete.

---
## Collegamenti
- Torna al corso: [[Dashboard Networking Basics]]