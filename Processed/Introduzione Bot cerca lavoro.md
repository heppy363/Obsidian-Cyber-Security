---
tipo: nota_lezione
corso: "Bot cerca lavoro"
tags: [progetto, progettiPersonale, Completed]
creato: 2026-02-19 10:45
---

# 📝 Lezione: Introduzione Bot cerca lavoro
**Corso:** [[Bot cerca lavoro]]

---
## Contenuto
`Si tratta di un sistema automatico per la ricerca di potenziali clienti in ambito di creazione di siti web o e-commers` 

### L'Idea 
Si tratta di un agente autonomo che scandaglia il web alla ricerca di potenziali clienti per il contatto e successivo preventivo di siti web o e-commers, il punto fondamentale e quello di inserire un area geografica e al interno di essa mi cerca tutte le attivita commerciali alle quali puo servire un sito web il tutto sotto un range di KM ad esempio Milano 10 KM e da si procede. 
### Funzioni 
1) Impostazione di range area geografica 
2) Trovare se esiste un sito web o meno 
3) Constatare la data di creazione del sito web 
	1) serve per capire se si puo procedere con un possibile refactoring o meno dello stesso 
4) Suddvidere le attivita per categoria quindi in base agli interessi 
5) Riassunzione completa ogni 2/3 giorni genera un file di log con tutte le informazioni 
	1) Nome del azienda 
	2) Ramo in cui opera 
	3) Se ha o meno un sito web 
	4) La data di creazione del sito web stesso 

### Come strutturerei il flusso di lavoro (Workflow)
Per far funzionare questo agente autonomo, avresti bisogno di integrare diverse tecnologie:
1. **Sourcing (L'input Geografico):** Utilizzerei l'API di **Google Maps (Places API)**. Ti permette di definire il centro (es. Milano) e il raggio (10km). Ti restituisce nome azienda, indirizzo, categoria e, se presente, l'URL del sito.
2. **Validazione (Il filtro):** Se il campo "website" è vuoto nel database di Google, l'azienda è un **Lead Prioritario** (non ha un sito).
3. **Analisi Tecnica (Il Refactoring):** Se il sito esiste, l'agente deve interrogarlo:
    - **Data di creazione:** Si può usare il protocollo **WHOIS** (per la registrazione del dominio) o, meglio ancora, le API di **Wayback Machine** per vedere quando il sito ha iniziato a essere attivo.
    - **Tecnologia:** Usare strumenti come _Wappalyzer_ (via API) per capire se usano un vecchio WordPress o tecnologie obsolete.
4. **Categorizzazione:** Sfruttare un LLM (come GPT-4o o Claude) per analizzare la descrizione dell'attività e decidere se è un target "Premium" (es. un ristorante stellato senza sito) o "Low priority".

---
## Collegamenti
- Torna al corso: [[Bot cerca lavoro]]