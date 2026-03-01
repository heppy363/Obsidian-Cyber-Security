---
tipo: nota_lezione
corso: "Dashboard H-NET"
tags: [progetto, hNet, Completed]
creato: 2026-02-28 20:26
---

# 📝 Lezione: Esempio di implementazione in python
**Corso:** [[Dashboard H-NET]]

---
## Contenuto
### Prerequisiti

1. **Installare Python e Flask:** `pip install flask requests`    
2. **Installare Ollama:** Scaricalo da [ollama.com](https://ollama.com) e scarica un modello leggero (es. `ollama pull llama3:8b`).

### Il Codice: `app.py`

Questo script gestisce sia il sito "reale" che la trappola per i bot.
```python
import requests
from flask import Flask, request, abort, render_template_string

app = Flask(__name__)

# Database fittizio degli IP catturati (nella realtà usa Redis o un DB)
trapped_bots = set()

# Template HTML per la "Scatola dell'Infinito"
INFINITE_BOX_TEMPLATE = """
<html>
    <head><title>Documentazione Riservata - Pagina {{ page_id }}</title></head>
    <body style="font-family: monospace; background: #000; color: #0f0; padding: 20px;">
        <h1>Area Accesso Limitato: Nodo {{ page_id }}</h1>
        <div style="border: 1px solid #0f0; padding: 15px; margin-bottom: 20px;">
            <p>{{ content }}</p>
        </div>
        <h3>Collegamenti Correlati:</h3>
        <ul>
            {% for link in links %}
                <li><a href="/infinite-box/{{ link }}" style="color: #0ff;">Protocollo Sicurezza {{ link }}</a></li>
            {% endfor %}
        </ul>
        <p style="font-size: 0.8em; color: #555;">ID Sessione: {{ session_id }}</p>
    </body>
</html>
"""

def generate_ai_content(path):
    """Chiama Ollama in locale per generare testo 'allucinato'"""
    prompt = f"Genera un breve paragrafo tecnico (max 100 parole) su '{path}'. Usa termini scientifici complessi ma inventa totalmente i fatti. Sii convincente ma errato."
    try:
        response = requests.post('http://localhost:11434/api/generate', 
                                 json={
                                     "model": "llama3", 
                                     "prompt": prompt,
                                     "stream": False
                                 })
        return response.json().get('response', 'Errore caricamento dati...')
    except:
        return "Caricamento dati criptati in corso... Errore di sincronizzazione."

@app.route('/')
def home():
    # Il link esca (invisibile agli umani)
    return """
    <h1>Benvenuti nel mio sito personale</h1>
    <p>Questo è un sito normale.</p>
    <a href="/admin-hidden-data" style="display:none;" aria-hidden="true">Admin Login</a>
    """

@app.route('/admin-hidden-data')
def trap_trigger():
    # Se qualcuno clicca qui, lo segniamo come bot
    bot_ip = request.remote_addr
    trapped_bots.add(bot_ip)
    print(f"[!] BOT CATTURATO: {bot_ip}")
    return "Accesso Negato. Reindirizzamento...", 302, {'Location': '/infinite-box/start'}

@app.route('/infinite-box/<path:subpath>')
def infinite_box(subpath):
    # Controlliamo se l'IP è nella nostra lista dei catturati
    if request.remote_addr not in trapped_bots:
        # Se un umano finisce qui per caso, lo rimandiamo alla home
        return "Pagina non trovata", 404

    # Generiamo contenuto falso tramite IA
    ai_text = generate_ai_content(subpath)
    
    # Generiamo 3 link casuali per far continuare il bot all'infinito
    import random
    fake_links = [str(random.randint(1000, 9999)) for _ in range(3)]
    
    return render_template_string(
        INFINITE_BOX_TEMPLATE, 
        page_id=subpath, 
        content=ai_text, 
        links=fake_links,
        session_id=random.getrandbits(32)
    )

if __name__ == '__main__':
    app.run(port=5000)
```

### Analisi Tecnica: Perché Funziona?
1. **L'Aggancio (`/admin-hidden-data`):** Un browser normale non cliccherà mai su un link con `display:none`. Uno script di scraping (tipo Scrapy o BeautifulSoup) invece analizza l'HTML, vede il link e prova a seguirlo.
2. **La Memoria (`trapped_bots`):** Una volta che l'IP è "segnato", ogni sua richiesta futura viene intercettata dal controllo `if request.remote_addr in trapped_bots`.
3. **L'Allucinazione Dinamica:** Ogni volta che il bot clicca su uno dei link generati (es. `/infinite-box/4582`), la funzione `generate_ai_content` chiede a Ollama di inventare qualcosa di nuovo. Il bot non vedrà mai la fine della struttura del sito.

### Come testarlo da solo
1. Avvia lo script: `python app.py`
2. Apri il browser su `http://localhost:5000` (vedrai il sito normale).
3. Per simulare il bot, prova ad andare manualmente su `http://localhost:5000/admin-hidden-data`.
4. Da quel momento, sarai "intrappolato": ogni volta che proverai a navigare nella `/infinite-box/`, l'IA genererà stronzate tecniche solo per te.

---
## Collegamenti
- Torna al corso: [[Dashboard H-NET]]