---
tipo: nota_lezione
corso: "Dashboard progetti personali"
tags: [progetto, progettiPersonali, Completed]
creato: 2026-03-01 14:34
---

# 📝 Lezione: Deplay su render
**Corso:** [[Dashboard progetti personali]]

---
## Contenuto

## Lato Cliente: Configurazione Account e Billing
_Il cliente deve eseguire questi passaggi per attivare l'infrastruttura._
1. **Creazione Account:** Vai su [dashboard.render.com](https://dashboard.render.com) e registrati (consigliato usare l'opzione "Sign up with GitHub" o con un'email aziendale).
2. **Impostazione Pagamento:** Vai nella sezione **Billing** e inserisci un metodo di pagamento. Questo è fondamentale per evitare che i servizi vadano in "sospensione" (sleep) dopo 15 minuti di inattività, garantendo che il sito sia sempre raggiungibile.
3. **Invito Collaboratore:**
    - Vai in **Settings** > **Team Members**.
    - Clicca su **Invite Member**.
    - Inserisci l'email del tuo sviluppatore e assegna il ruolo di **Admin** (necessario per gestire database e variabili d'ambiente).

## 🔴 Lato Developer: Gestione Codice e Deploy
_Questi sono i passaggi tecnici che gestirai tu una volta ricevuto l'invito._
1. **Preparazione Repository:** Assicurati che il codice sia su una repository GitHub (privata o pubblica).
2. **Collegamento GitHub-Render:**
    - Accetta l'invito al team del cliente via email.
    - Nella dashboard di Render, assicurati di aver selezionato il **Team del Cliente** dal menu a tendina in alto a sinistra.
    - Clicca su **New** > **Web Service**.
    - Connetti il tuo account GitHub. Se non vedi la repo, clicca su "Configure GitHub App" e dai i permessi di lettura per quella specifica repository.
3. **Configurazione Deploy:**
    - Imposta il **Build Command** (es: `npm install && npm run build`).
    - Imposta lo **Start Command** (es: `npm start` o `node server.js`).
    - Aggiungi le variabili d'ambiente (`.env`) nella sezione **Environment**.
4. **Automazione:** Una volta creato il servizio, ogni volta che farai un `git push` sulla branch principale (es: `main`), Render farà il deploy automatico senza che tu debba entrare nel pannello del cliente.

## 📋 Riepilogo Responsabilità

|Task|Responsabile|Perché?|
|---|---|---|
|**Costi Mensili**|Cliente|La fattura arriva direttamente a lui.|
|**Proprietà Dati**|Cliente|Se il rapporto di lavoro finisce, lui mantiene il servizio.|
|**Aggiornamenti Codice**|Developer|Basta un `git push` per aggiornare il sito live.|
|**Debug e Log**|Developer|Hai accesso alla console per vedere eventuali errori in tempo reale.|

---
## Collegamenti
- Torna al corso: [[Dashboard progetti personali]]
- [[DNS su render]]