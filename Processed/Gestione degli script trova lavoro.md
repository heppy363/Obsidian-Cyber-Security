---
aliases:
  - Completate
tags:
  - Completed
  - cercatoreLavoro
  - progettiPersonali
---
--- 
## Nozioni
### 1. Script A & B: Sourcing e Filtering (Il cercatore)
Poiché vogliamo evitare i costi di Apify, useremo **Playwright** per fare "scraping" diretto su Google Maps.
- **Logica:** L'agente apre `google.com/maps`, cerca la parola chiave (es. "Ristorante Milano"), e scorre la lista lateralmente.
- **Dati estratti:** Nome, Indirizzo, Sito Web (se presente).
- **Filtro Immediato:** Se il selettore del sito web manca, lo marchiamo nel DB come `TARGET_NEW`. Se c'è, lo passiamo allo Script C.

### 2. Script C: Deep Scan (L'ispettore tecnico)
Questo task riceve l'URL e fa un'analisi "sotto il cofano".
- **Mobile Friendly:** Controlliamo se esiste `<meta name="viewport">`. Se manca, il sito è un disastro su smartphone (ottimo pitch di vendita).
- **WHOIS (Età):** Useremo la libreria `python-whois`. È gratuita. Ci dice quando è stato registrato il dominio. Se ha più di 10 anni, probabilmente il design è obsoleto.
- **PageSpeed:** Useremo la libreria `LHCI` o chiameremo l'API di Google (che ha un piano gratuito enorme).
```
@task
def deep_scan(url):
    # Controllo Mobile con Playwright
    # Controllo Età con whois.whois(url)
    # Controllo Performance con PageSpeed API
    return {
        "mobile": True,
        "age_years": 8,
        "speed_score": 45
    }
```
### 3. Script D: AI Processing (Il copywriter)
Qui decidiamo come approcciare il cliente. Per stare a **costo zero**, ti consiglio di installare **Ollama** sul tuo PC. Ti permette di usare modelli come **Llama 3** o **Mistral** localmente.
- **Input:** Tutti i dati raccolti (es. "Sito del 2016, velocità 30/100, non responsive").
- **Output:** Un JSON che contiene il "Pain Point" (il problema principale) e una bozza di mail.
```
@task
def generate_ai_pitch(data):
    # Chiamata locale a Ollama (Costo 0)
    prompt = f"L'azienda {data['name']} ha un sito lento ({data['speed']}). Scrivi un motivo convincente per cui dovrebbero rifarlo."
    return response_from_ollama
```
### 4. Script E: Delivery (Il postino)
Per l'invio, SendGrid e Mailgun hanno piani gratuiti (circa 100 email al giorno).
- **Importante:** Non inviare email a raffica. Prefect può programmare l'invio di una mail ogni 10-15 minuti per evitare di finire nello spam.
### Lo Schema del Database (PostgreSQL)
Prima di scrivere il codice, dobbiamo preparare il "contenitore" dei dati. Ecco come dovrebbe apparire la tua tabella principale:
|**Campo**|**Tipo**|**Note**|
|---|---|---|
|`id`|SERIAL|ID univoco.|
|`business_name`|TEXT|Nome attività.|
|`city_area`|TEXT|es: "Milano - 10km".|
|`has_website`|BOOLEAN|Risultato Script B.|
|`tech_report`|JSONB|Risultati Script C (velocità, età, mobile).|
|`ai_pitch`|TEXT|Il testo generato da Ollama/GPT.|
|`status`|TEXT|`LEAD`, `ANALYZED`, `EMAILED`, `REJECTED`.|

### Perché questo approccio ti salva?
1. **Modularità:** Se Google Maps cambia la grafica e lo Script A si rompe, non perdi i dati dello Script C già fatti.
2. **Economia:** Usando Playwright (per Maps) e Ollama (per AI), le tue uniche spese sono la connessione internet.
3. **Scalabilità:** Domani vuoi cercare a Roma invece che a Milano? Cambi solo un parametro nel "Trigger".


## Link 
1) 