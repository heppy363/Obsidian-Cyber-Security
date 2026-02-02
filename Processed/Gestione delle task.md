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
**Prefect** è un orchestratore di workflow (un "gestore di processi"). Immaginalo come un supervisore che sta sopra il tuo codice Python. Invece di far girare uno script che se incontra un errore "muore" e finisce lì, Prefect gestisce l'esecuzione pezzo per pezzo.
Ecco come funziona e perché è fondamentale per il tuo obiettivo di non spendere nulla.

---

### 1. Prefect è gratis?
**Sì.** Esistono due modi per usarlo:
1. **Prefect Cloud:** La versione ospitata da loro (ha un piano gratuito molto generoso).
2. **Prefect Self-Hosted (Consigliato per te):** È totalmente **Open Source**. Lo installi tramite `pip install prefect`, lanci un server locale sul tuo PC o server, e hai tutto il controllo senza pagare un centesimo.
### 2. A cosa serve `@task`?
In Python, una funzione è solo una funzione. Se aggiungi `@task` sopra, la trasformi in un "mattoncino" che Prefect può monitorare.
#### Esempio Pratico:
Senza Prefect, se il tuo codice crasha al sito n. 50, perdi tutto. Con `@task`, Prefect tiene traccia di cosa è successo.
```
from prefect import task, flow

@task(retries=3)  # <-- Se fallisce, riprova 3 volte GRATIS e in automatico
def controlla_sito(url):
    # Qui metti il tuo codice Playwright
    print(f"Sto analizzando {url}")
    # Se qui c'è un errore di rete, Prefect non fa crashare tutto lo script
    # ma riprova la funzione tra un po'.

@flow(name="Ricerca Lead Web") # <-- Questo è il "contenitore" di tutti i task
def main_flow():
    lista_siti = ["google.it", "sito-rotto.com", "esempio.it"]
    for sito in lista_siti:
        controlla_sito(sito)

if __name__ == "__main__":
    main_flow()
```

### 3. Perché ti serve per il tuo progetto?
Senza una libreria come Prefect, dovresti scrivere tu centinaia di righe di codice per gestire:
- **Logging:** Sapere esattamente a che ora è fallita la ricerca su "Milano 10km".
- **Schedulazione:** Far partire lo script ogni 3 giorni (Prefect ha un timer interno).
- **Gestione Errori:** Se un sito è lento, Prefect lo mette in "Failed" ma continua con il sito successivo. Senza Prefect, un errore non gestito blocca tutto il ciclo `for`.
### 4. Strategia "Zero Spese" per il tuo Stack
Dato che non vuoi spendere un centesimo, ecco come dobbiamo adattare le tecnologie che abbiamo discusso:
- **Linguaggio:** Python (Gratis).
- **Orchestratore:** Prefect Self-Hosted (Gratis).
- **Database:** PostgreSQL installato localmente (Gratis).
- **Browser:** Playwright (Gratis).
- **API Google Maps:** Qui c'è un trucco. Invece di pagare le API ufficiali o Apify, possiamo scrivere uno scraper "raw" che usa Playwright per simulare un utente su Google Maps e leggere i risultati. È più difficile da scrivere (va gestito bene il caricamento della pagina), ma è **100% gratis**
- **API AI (OpenAI):** Questo è l'unico punto dove è difficile scendere a zero, ma puoi usare **Ollama**. Ollama ti permette di far girare modelli come Llama 3 o Mistral **sul tuo computer** (se hai una buona scheda video o un Mac recente). Così l'analisi dei testi è gratis.
- **PageSpeed:** L'API di Google PageSpeed è gratuita fino a un numero molto alto di richieste.

- [[Gestione dei container Docker torva lavoro]]
## Link 
1) 