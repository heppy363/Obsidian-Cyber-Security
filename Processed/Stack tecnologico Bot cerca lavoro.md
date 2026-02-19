---
tipo: nota_lezione
corso: "Bot cerca lavoro"
tags: [progetto, progettiPersonale, Completed]
creato: 2026-02-19 10:47
---

# 📝 Lezione: Stack tecnologico Bot cerca lavoro
**Corso:** [[Bot cerca lavoro]]

---
## Contenuto
### 1. Core Language & Orchestration
- **Linguaggio:** **Python 3.10+**. È lo standard per automazione e dati.
- **Orchestratore di Task:** **Prefect** o **Dagster**. Perché? Gestiscono i tentativi falliti (retry), la schedulazione (ogni 2/3 giorni) e ti danno una dashboard per vedere se i bot si sono bloccati.
- Docker
### 2. Sourcing & Scraping (Il "Motore")
Estrarre dati da Google Maps o dai siti non è banale per via dei bot-detection.
- **Ricerca Aziende:** **Apify (Google Maps Scraper)**. Invece di scrivere tu lo scraper per Maps (che Google blocca subito), usa le API di Apify. Ti restituiscono JSON pronti con coordinate, categoria e URL del sito.
- **Web Scraper (per i siti trovati):** **Playwright** (in modalità _headless_). È più veloce di Selenium e gestisce meglio i siti moderni in React/Angular.
- **Bypass dei Blocchi:** **Bright Data** o **ZenRows**. Se devi scansionare centinaia di siti, hai bisogno di proxy residenziali rotativi, altrimenti il tuo IP verrà bannato in 10 minuti.
### 3. Analisi "Level Up" (Web Vitals & Tech Stack)
- **Performance:** **Google PageSpeed Insights API**. È gratuita (entro certi limiti) e ti restituisce i dati reali sui Web Vitals. Puoi estrarre il punteggio "Performance" e usarlo nel tuo pitch.
- **Tecnologia del Sito:** **Wappalyzer API** o la libreria Python `builtwith`. Ti dice se il sito è in WordPress 4.0 (vecchio!), se usa jQuery del 2012 o se non ha un sistema di analytics.
### 4. Il Cervello: AI & Categorizzazione
- **LLM:** **OpenAI API (GPT-4o-mini)**. È molto economico e perfetto per:
    - Leggere il testo estratto dal sito e riassumere cosa fa l'azienda.
    - Scrivere la "Cold Email" personalizzata basandosi sui difetti trovati (es: "Ho visto che il tuo sito non è ottimizzato per mobile...").
- **Data Extraction:** **Instructor** (libreria Python). Ti permette di forzare l'output di GPT in modelli Pydantic (JSON strutturati), così il tuo log sarà sempre pulito.
### 5. Database & Storage
- **Database:** **PostgreSQL** con estensione **PostGIS** (se vuoi fare query geografiche avanzate, tipo "trovami tutti i lead nel raggio di X senza doverlo ricalcolare").
- **Log Finale:** **Pandas** per generare il file CSV/Excel o integrazione con le **Google Sheets API** per avere un foglio condiviso sempre aggiornato.
### Architettura del Flusso (Esempio per uno Sviluppatore)
1. **Script A (Trigger):** Inserisci `Milano, 10km`. Lo script chiama l'API di Apify.
2. **Script B (Filtering):** Prendi i risultati. Se `website == null` -> Tag: `NEW_SITE_REQUIRED`. Se `website != null` -> Passa allo Script C.
3. **Script C (Deep Scan):** Playwright apre il sito. Controlla:
    - Presenza tag `meta name="viewport"` (Mobile friendly?).
    - Chiamata a PageSpeed API per il punteggio.
    - Analisi WHOIS per l'età del dominio.
4. **Script D (AI Processing):** Passi i dati a GPT-4: _"Analizza questi dati: [Sito lento, Età 10 anni, Settore Ristorante]. Genera un oggetto JSON con un testo di approccio per il proprietario."_
5. **Script E (Delivery):** Invio tramite **SendGrid** o **Mailgun** API.

- [[Gestione delle task]]
- [[Integrazione API costo zero]]
- [[Gestione delle email trova lavoro]]

---
## Collegamenti
- Torna al corso: [[Bot cerca lavoro]]