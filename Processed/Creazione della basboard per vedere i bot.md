---
tipo: nota_lezione
corso: "Dashboard H-NET"
tags: [progetto, hNet, Completed]
creato: 2026-02-28 20:36
---

# 📝 Lezione: Creazione della basboard per vedere i bot 
**Corso:** [[Dashboard H-NET]]

---
## Contenuto
## 1. Il Codice Aggiornato con Monitoraggio Real-time

Useremo il sistema **Pub/Sub (Publish/Subscribe)** di Redis. Ogni volta che un bot compie un'azione, il server "pubblica" un messaggio e il logger lo stampa istantaneamente.

``` python
import time
import random
import threading
import redis
from flask import Flask, request, render_template_string

app = Flask(__name__)

# Connessione Redis
r = redis.Redis(host='localhost', port=6379, decode_responses=True)
p = r.pubsub()

# --- IL LOGGER IN TEMPO REALE ---
def redis_logger():
    """Thread separato che ascolta i log di Redis e li stampa a video"""
    pubsub = r.pubsub()
    pubsub.subscribe('bot_logs')
    print("--- [LOGGER] Sistema di monitoraggio 'Scatola dell'Infinito' Attivo ---")
    for message in pubsub.listen():
        if message['type'] == 'message':
            print(f" LOG: {message['data']}")

# Avviamo il logger in un thread parallelo
threading.Thread(target=redis_logger, daemon=True).start()

# --- LOGICA DEL SERVER ---

@app.route('/')
def home():
    # Esca per i bot: link nascosto
    return """
    <h1>Benvenuti nell'Archivio</h1>
    <a href="/access/keys" style="display:none;">Area Riservata</a>
    """

@app.route('/access/keys')
def trap_trigger():
    bot_ip = request.remote_addr
    # Registra il bot in Redis
    r.hset(f"bot:{bot_ip}", mapping={"depth": 0, "identity": "Sospetto Crawler"})
    # Pubblica il log
    r.publish('bot_logs', f"🔴 ALLERTA: Bot catturato! IP: {bot_ip} ha toccato l'esca.")
    return "Redirect...", 302, {'Location': '/infinite-box/start'}

@app.route('/infinite-box/<path:subpath>')
def infinite_box(subpath):
    bot_ip = request.remote_addr
    
    # Verifica se è un bot noto
    if not r.exists(f"bot:{bot_ip}"):
        return "Accesso Negato", 403

    # Incrementa profondità e recupera dati
    depth = r.hincrby(f"bot:{bot_ip}", "depth", 1)
    
    # Calcolo ritardo (Tarpit)
    delay = min(1.0 + (depth * 0.2), 10.0) 
    
    # Log dell'azione
    r.publish('bot_logs', f"🕵️  Bot {bot_ip} sta esplorando: /{subpath} (Profondità: {depth}, Ritardo: {delay}s)")
    
    time.sleep(delay) # Rallenta il bot

    # Genera link casuali per l'infinito
    links = [f"data_node_{random.getrandbits(16)}" for _ in range(5)]
    
    return render_template_string("""
        <body style="background:#000; color:#0f0;">
            <h2>Nodo di Sistema: {{ subpath }}</h2>
            <p>Dati decriptati: {{ content }}</p>
            <ul>
                {% for l in links %}
                <li><a href="/infinite-box/{{ l }}" style="color:#0f0;">Sotto-processo {{ l }}</a></li>
                {% endfor %}
            </ul>
        </body>
    """, subpath=subpath, content=f"Dato segreto #{random.randint(1,1000)}", links=links)

if __name__ == '__main__':
    app.run(port=5000)
```

## Gemini ha detto
Ottima idea. Vedere i log in tempo reale trasforma questo esperimento in una sorta di "centro di comando" della difesa attiva. Per farlo, creeremo un **thread separato** nel tuo script Python che monitora Redis e stampa sulla console ogni movimento del bot.
Ecco come potenziare il sistema per includere il monitoraggio in tempo reale e una logica di "trappola" ancora più profonda.

## 1. Il Codice Aggiornato con Monitoraggio Real-time

Useremo il sistema **Pub/Sub (Publish/Subscribe)** di Redis. Ogni volta che un bot compie un'azione, il server "pubblica" un messaggio e il logger lo stampa istantaneamente.

```Python
import time
import random
import threading
import redis
from flask import Flask, request, render_template_string

app = Flask(__name__)

# Connessione Redis
r = redis.Redis(host='localhost', port=6379, decode_responses=True)
p = r.pubsub()

# --- IL LOGGER IN TEMPO REALE ---
def redis_logger():
    """Thread separato che ascolta i log di Redis e li stampa a video"""
    pubsub = r.pubsub()
    pubsub.subscribe('bot_logs')
    print("--- [LOGGER] Sistema di monitoraggio 'Scatola dell'Infinito' Attivo ---")
    for message in pubsub.listen():
        if message['type'] == 'message':
            print(f" LOG: {message['data']}")

# Avviamo il logger in un thread parallelo
threading.Thread(target=redis_logger, daemon=True).start()

# --- LOGICA DEL SERVER ---

@app.route('/')
def home():
    # Esca per i bot: link nascosto
    return """
    <h1>Benvenuti nell'Archivio</h1>
    <a href="/access/keys" style="display:none;">Area Riservata</a>
    """

@app.route('/access/keys')
def trap_trigger():
    bot_ip = request.remote_addr
    # Registra il bot in Redis
    r.hset(f"bot:{bot_ip}", mapping={"depth": 0, "identity": "Sospetto Crawler"})
    # Pubblica il log
    r.publish('bot_logs', f"🔴 ALLERTA: Bot catturato! IP: {bot_ip} ha toccato l'esca.")
    return "Redirect...", 302, {'Location': '/infinite-box/start'}

@app.route('/infinite-box/<path:subpath>')
def infinite_box(subpath):
    bot_ip = request.remote_addr
    
    # Verifica se è un bot noto
    if not r.exists(f"bot:{bot_ip}"):
        return "Accesso Negato", 403

    # Incrementa profondità e recupera dati
    depth = r.hincrby(f"bot:{bot_ip}", "depth", 1)
    
    # Calcolo ritardo (Tarpit)
    delay = min(1.0 + (depth * 0.2), 10.0) 
    
    # Log dell'azione
    r.publish('bot_logs', f"🕵️  Bot {bot_ip} sta esplorando: /{subpath} (Profondità: {depth}, Ritardo: {delay}s)")
    
    time.sleep(delay) # Rallenta il bot

    # Genera link casuali per l'infinito
    links = [f"data_node_{random.getrandbits(16)}" for _ in range(5)]
    
    return render_template_string("""
        <body style="background:#000; color:#0f0;">
            <h2>Nodo di Sistema: {{ subpath }}</h2>
            <p>Dati decriptati: {{ content }}</p>
            <ul>
                {% for l in links %}
                <li><a href="/infinite-box/{{ l }}" style="color:#0f0;">Sotto-processo {{ l }}</a></li>
                {% endfor %}
            </ul>
        </body>
    """, subpath=subpath, content=f"Dato segreto #{random.randint(1,1000)}", links=links)

if __name__ == '__main__':
    app.run(port=5000)
```
## 2. Perché usare Redis per i Log?
Utilizzare il sistema Pub/Sub di Redis invece di un semplice `print()` ha vantaggi enormi in un'architettura reale:
1. **Disaccoppiamento:** Il server web (Flask) si occupa solo di servire le pagine. Il logger potrebbe girare su un altro computer o in un'altra finestra del terminale.    
2. **Scalabilità:** Se avessi 10 server web, tutti potrebbero inviare i log allo stesso canale Redis, permettendoti di monitorare l'attacco globale da un'unica console.
3. **Storico:** Puoi usare Redis non solo per i log in tempo reale, ma anche per salvare le statistiche (es: _"Quante pagine ha visitato l'IP X in totale?"_).

## 3. Strategie Avanzate per "Inquinare" il Bot
Dato che vuoi rendere il sito **facilmente accessibile** ma ingannevole, ecco tre tocchi di classe:
- **Il File `robots.txt` Invertito:** Solitamente dici ai bot cosa _non_ visitare. Qui scriverai: `Allow: /infinite-box/` Questo attira i bot che seguono le regole, portandoli dritti nella trappola.
- **Sitemap Gigante:** Crea un file `/sitemap.xml` che contiene 50.000 link che puntano tutti alla Scatola dell'Infinito. I crawler "divoreranno" questi link e rimarranno bloccati per giorni.
- **Header HTTP Ingannevoli:** Invia header come `Server: Microsoft-IIS/6.0` (una versione vecchia e vulnerabile). I bot di attacco crederanno di aver trovato un server facile da hackerare e si accaniranno ancora di più. 

### Cosa vedrai sulla console:
Mentre il bot naviga, la tua console inizierà a scorrere così:
> `LOG: 🔴 ALLERTA: Bot catturato! IP: 192.168.1.15 ha toccato l'esca.` `LOG: 🕵️ Bot 192.168.1.15 sta esplorando: /start (Profondità: 1, Ritardo: 1.2s)` `LOG: 🕵️ Bot 192.168.1.15 sta esplorando: /data_node_4521 (Profondità: 2, Ritardo: 1.4s)`
---
## Collegamenti
- Torna al corso: [[Dashboard H-NET]]