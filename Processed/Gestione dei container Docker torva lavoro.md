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
Utilizzare Docker ti permette di non "sporcare" il tuo sistema operativo con database o dipendenze complesse e di rendere l'agente trasportabile su qualsiasi server o PC.
Ecco la configurazione del tuo file `docker-compose.yml`:

### 1. Container Database (PostgreSQL)
- **Servizio:** `db`
- **Scopo:** È la memoria a lungo termine dell'agente. Qui vengono salvati i lead, i risultati di PageSpeed, i testi dell'AI e lo stato di ogni contatto (es. "già contattato").
- **Perché:** Senza questo, se spegni il PC, perdi tutto il lavoro di ricerca fatto nei giorni precedenti.
### 2. Container Orchestratore (Prefect Server)
- **Servizio:** `prefect-server`
- **Scopo:** È il "cervello" gestionale. Ti fornisce la Dashboard Web per vedere se i tuoi script stanno girando, quali sono falliti e quanti lead hai trovato.
- **Perché:** Gestisce la schedulazione (es. "fai partire la ricerca ogni lunedì alle 09:00").
### 3. Container AI Locale (Ollama)
- **Servizio:** `ollama-ai`
- **Scopo:** Fa girare i modelli linguistici (LLM come Llama 3 o Mistral) sul tuo hardware.
- **Perché:** È la chiave per il **costo zero**. Invece di pagare OpenAI per ogni mail generata, interroghi questo container che risponde gratuitamente sfruttando la tua CPU/GPU.
### 4. Container Worker (L'Agente Python)
- **Servizio:** `agent-worker`
- **Scopo:** Questo è il container dove risiede il tuo codice Python. È quello che effettivamente "fa le cose": apre Playwright per Google Maps, analizza i siti e invia le mail.
- **Perché:** Mantiene le dipendenze (Playwright, browser headless, librerie Python) isolate e pronte all'uso.
### 5. Container Cache (Redis) - _Opzionale ma consigliato_
- **Servizio:** `redis`
- **Scopo:** Serve a Prefect e ai tuoi scraper per memorizzare dati temporanei velocemente.
- **Perché:** Aiuta a gestire le code di messaggi se decidi di scalare la ricerca su molte città contemporaneamente.

|**Container**|**Immagine Base**|**Risorse utilizzate**|**Costo**|
|---|---|---|---|
|**Database**|`postgres:15`|Bassa (RAM/Disco)|Gratis|
|**Orchestratore**|`prefecthq/prefect`|Media (RAM)|Gratis|
|**AI Locale**|`ollama/ollama`|Alta (CPU/GPU)|Gratis|
|**Worker**|`python:3.10-slim`|Media (RAM per i browser)|Gratis|
|**Cache**|`redis:alpine`|Bassissima (RAM)|Gratis|
## Link 
1) 