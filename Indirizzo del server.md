### 1. Su Render (Dashboard)
Prima di tutto, devi comunicare a Render quale dominio intendi utilizzare.
1. Entra nel servizio statico che hai creato su Render.
2. Nel menu a sinistra, clicca su **Settings**.
3. Scorri fino alla sezione **Custom Domains**.
4. Clicca su **Add Custom Domain** e inserisci il nome del dominio (es: `www.nomedominio.it` oppure `nomedominio.it`).
5. Render ti mostrerà i valori DNS che dovrai inserire su Aruba (un record **CNAME** per il sottodominio www e un record **A** per il dominio principale).

### 2. Su Aruba (Pannello DNS)
Ora devi "puntare" il dominio verso i server di Render.
1. Accedi all'Area Clienti di Aruba e vai nel **Pannello di Controllo** del dominio.
2. Cerca la voce **Utility Dominio** > **Gestione DNS e Name Server**.
3. Clicca su **Gestisci**.
#### Configurazione per il sottodominio (WWW)
- Trova il record di tipo **CNAME** con host `www`.
- Modificalo (o crealo se non c'è) inserendo come valore l'indirizzo fornito da Render (solitamente è qualcosa tipo `tuo-sito.onrender.com`).
- **Nota:** Se Aruba ti obbliga a mettere un punto finale (es. `tuo-sito.onrender.com.`), mettilo.

#### Configurazione per il dominio principale (Root/Apex)
Se vuoi che il sito funzioni anche scrivendo solo `nomedominio.it` (senza www):
- Trova il record di tipo **A**.
- Modifica l'indirizzo IPv4 inserendo quello fornito da Render (lo trovi nella tabella dei Custom Domains sotto la voce "IP address").
- _Attenzione:_ Se ci sono più record "A" per lo stesso host vuoto, elimina quelli vecchi che puntano ad Aruba.

### 3. Verifica e Certificato SSL
- **Attesa:** Una volta salvate le modifiche su Aruba, potrebbero volerci da pochi minuti a qualche ora (propagazione DNS).
- **SSL automatico:** Non appena Render rileva che i DNS sono corretti, genererà automaticamente un certificato **SSL gratuito (HTTPS)** tramite Let's Encrypt. Non devi fare nulla su Aruba per il certificato.
- **Stato su Render:** Torna nella sezione "Custom Domains" di Render; vedrai una spunta verde quando tutto sarà configurato correttamente.