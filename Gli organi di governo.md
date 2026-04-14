---
tipo: nota_lezione
corso: "Concorso pubblici"
tags: [progetto, concorsiPubblici, Completed]
creato: 2026-04-13 21:09
---

# 📝 Lezione: Gli organi di governo
**Corso:** [[Concorso pubblici]]

---
## Contenuto
In un Comune, il potere non è concentrato in un unico punto, ma diviso per bilanciare le funzioni. Immaginalo come un'architettura **Client-Server** dove ogni componente ha permessi e task specifici.

### 1. Il Consiglio Comunale (The "Architecture & Policy" Layer)
È l'organo di **indirizzo e controllo politico-amministrativo**. Non si occupa della gestione quotidiana, ma decide le "regole del gioco".
- **Chi sono:** Consiglieri eletti dai cittadini (il numero varia in base alla popolazione).
- **Cosa fanno (Main Task):** Approvano gli atti fondamentali. Se non passa dal Consiglio, il Comune non può muoversi su:
    - Statuti e Regolamenti.
    - Bilanci (previsionale e consuntivo).
    - Piani urbanistici (es. dove si può costruire).
    - Istituzione di tributi (tasse locali).
- **Logica:** È un organo collegiale (si vota e vince la maggioranza).
- [[Approfondimento Consiglio Comunale]]

### 2. La Giunta Comunale (The "Executive/Runtime" Layer)
È l'organo **esecutivo**. Collabora con il Sindaco nell'attuazione degli indirizzi generali.
- **Chi sono:** Il Sindaco + gli **Assessori** (nominati dal Sindaco, spesso esperti in materie specifiche come Bilancio, Scuola, Urbanistica).
- **Cosa fanno (Main Task):** Svolgono tutto ciò che la legge o lo Statuto non riservano espressamente al Consiglio o al Sindaco.
    - Approvano progetti di opere pubbliche.
    - Decidono l'organizzazione degli uffici.
    - Approvano le variazioni di bilancio d'urgenza.
- [[La giunta comunale]]

### 3. Il Sindaco (The "Root/Superuser")
È il vertice dell'amministrazione, legale rappresentante dell'ente e ufficiale di Governo.
- **Funzioni amministrative:** Nomina gli Assessori, convoca la Giunta, nomina i responsabili degli uffici.
- **Funzioni di Stato:** Si occupa di anagrafe, stato civile, leva militare e pubblica sicurezza.
- **Ordinanze:** Ha il potere di emettere comandi d'urgenza (`sudo command`) per emergenze sanitarie o di igiene pubblica.
	- [[Preseidente del consiglio VS Sindaco]]

## Workflow degli Atti: Delibere vs Determine
Per l'orale è fondamentale capire la differenza tra gli "output" di questi organi:

|Atto|Chi lo firma?|Cosa contiene?|
|---|---|---|
|**Delibera di Consiglio**|Il Presidente del Consiglio|Scelte strategiche e regolamenti (es. "Cambiamo il regolamento asili").|
|**Delibera di Giunta**|Il Sindaco (o vice)|Scelte esecutive (es. "Approviamo il progetto tecnico per l'asilo").|
|**Determina (o Det.)**|Il Dirigente/Responsabile|Gestione pura (es. "Compro 10 sedie per l'asilo con questi soldi").|

---
## Collegamenti
- Torna al corso: [[Concorso pubblici]]
- [[Come gli organi di governo interagiscono]]