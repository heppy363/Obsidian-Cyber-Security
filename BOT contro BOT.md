---
tipo: nota_lezione
corso: "Dashboard H-NET"
tags: [progetto, hNet, Completed]
creato: 2026-02-28 20:15
---

# 📝 Lezione: BOT contro BOT 
**Corso:** [[Dashboard H-NET]]

---
## Contenuto

## 1. Il Progetto della "Scatola dell'Infinito"
Per realizzarlo, hai bisogno di tre componenti che lavorano insieme:
1. **Il Portiere (Rilevamento):** Identifica se chi bussa è un umano o un bot.
2. **Lo Specchio (Redirezione):** Sposta il bot in un'area isolata senza fargli capire il trucco.
3. **Il Generatore di Allucinazioni (LLM):** Crea contenuti infiniti e credibili, ma falsi.

## 2. Come Implementarlo (Livello Tecnico)
### Fase A: Identificazione del Bot
Puoi usare diverse tecniche per capire chi "intrappolare":
- **User-Agent:** Molti bot si identificano (es. `python-requests`, `Go-http-client`).
- **Comportamento:** Un umano non visita 50 pagine in 2 secondi. Se qualcuno lo fa, è un candidato per la Scatola.
- **Honeypot Link (Il trucco classico):** Inserisci nel tuo sito un link invisibile agli umani (nascosto con i CSS), ma visibile ai bot. Se qualcuno clicca quel link, è sicuramente un bot e finisce dritto nella Scatola dell'Infinito.
### Fase B: La Redirezione
Invece di bloccare l'IP, il tuo server (Node.js, Python/Flask, o anche tramite regole di Nginx) risponde servendo una pagina speciale.
- **Esempio in pseudo-codice:**
    > SE (richiesta arriva da IP_sospetto O clicca_link_nascosto) ALLORA: mostra `infinite_box.html` invece di `index.html`.
### Fase C: Generazione del Contenuto "Marcio"
Qui entra in gioco l'IA. Non vuoi usare un modello costoso come GPT-4 per ogni richiesta del bot (ti costerebbe una fortuna).
- **Soluzione Economica:** Usa un modello locale leggero (come **Llama 3** o **Mistral** via Ollama) sul tuo PC o server.
- **Il Prompt:** Istruisci l'IA così: _"Sei un generatore di contenuti per un sito di [Tuo Argomento]. Genera un articolo lungo 500 parole che sembri professionale ma contenga dati scientifici inventati, date storiche errate e nomi di persone inesistenti."_

## 3. Rendere la Scatola "Infinita"
Il vero tocco di classe è impedire al bot di uscire.
- **Link Circolari:** In fondo a ogni pagina generata dall'IA, inserisci 3-4 link a nuovi articoli (es. `/infinite-box/articolo-4582`).
- **Generazione On-the-fly:** Quando il bot clicca su uno di quei link, il tuo server genera un nuovo contenuto al volo usando l'IA.
- **Risultato:** Il bot crederà di aver trovato una miniera d'oro di informazioni e continuerà a scavare per ore, sprecando banda e risorse, mentre tu ti godi i log del server.

## Attenzione ai "Danni Collaterali"
Prima di accendere la Scatola, ricorda due regole d'oro:
1. **Escludi i Motori di Ricerca:** Assicurati che Google, Bing e DuckDuckGo non finiscano nella trappola (controlla i loro IP ufficiali), altrimenti il tuo sito sparirà dal web reale.
2. **Costi API:** Se usi modelli IA a pagamento (via API), un bot molto veloce potrebbe consumare il tuo credito in pochi minuti. Usa sempre un modello locale o metti un limite massimo di generazioni.

---
## Collegamenti
- Torna al corso: [[Dashboard H-NET]]