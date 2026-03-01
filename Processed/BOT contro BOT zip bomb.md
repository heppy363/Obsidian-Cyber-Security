---
tipo: nota_lezione
corso: "Dashboard H-NET"
tags: [progetto, hNet, Completed]
creato: 2026-02-28 20:40
---

# 📝 Lezione: BOT contro BOT zip bomb
**Corso:** [[Dashboard H-NET]]

---
## Contenuto
### 1. La Strategia del "Binary Flood"

L'idea è di inviare dati che sembrano archivi compressi o file di database (`.sql.gz` o `.zip`), ma che contengono in realtà sequenze di byte casuali che non possono essere compressi ulteriormente (o che si espandono enormemente se il bot prova a decomprimerli).

---

### 2. Il Codice Potenziato (Fase "Overload")

Aggiungiamo una funzione per generare stream di dati binari e modifichiamo la rotta principale.
```python 
import os
from flask import Response

# --- NUOVA FUNZIONE: GENERATORE DI ZAVORRA BINARIA ---
def generate_binary_junk(size_mb=50):
    """Genera blocchi di dati casuali per saturare la memoria del bot"""
    for _ in range(size_mb):
        # Invia 1MB di dati casuali alla volta per non saturare la TUA RAM
        yield os.urandom(1024 * 1024)

@app.route('/infinite-box/<path:subpath>')
def infinite_box(subpath):
    bot_ip = request.remote_addr
    bot_data = r.hgetall(f"bot:{bot_ip}")
    
    if not bot_data:
        return "Accesso Negato", 403

    depth = r.hincrby(f"bot:{bot_ip}", "depth", 1)
    
    # --- LOGICA DI OVERLOAD (Profondità > 500) ---
    if depth > 500:
        r.publish('bot_logs', f"🔥 OVERLOAD: Il bot {bot_ip} è troppo profondo ({depth}). Invio zavorra binaria.")
        
        # Generiamo un nome file credibile per ingannare il bot
        filename = f"backup_full_part_{random.randint(100, 999)}.sql.gz"
        
        # Rispondiamo con uno stream binario invece di una pagina HTML
        return Response(
            generate_binary_junk(size_mb=100), # 100MB di spazzatura a ogni richiesta
            mimetype='application/octet-stream',
            headers={"Content-Disposition": f"attachment; filename={filename}"}
        )

    # --- LOGICA STANDARD (Sotto le 500 pagine) ---
    delay = min(1.0 + (depth * 0.2), 15.0)
    r.publish('bot_logs', f"🕵️  Bot {bot_ip} in esplorazione. Profondità: {depth}")
    time.sleep(delay)

    # (Qui prosegue il codice precedente con la generazione IA...)
    return render_template_string(TEMPLATE_IA, ...)
```

### 3. Perché questa tecnica è devastante
1. **Saturazione del Disco:** Molti bot sono configurati per scaricare automaticamente file che sembrano backup o archivi. Se ne invii uno da 100MB a ogni richiesta, e il bot ne fa 10 al secondo, riempirai i suoi dischi (o quelli del server dell'attaccante) in pochissimo tempo.
2. **Consumo di Banda:** L'attaccante pagherà per il traffico dati in uscita (se usa cloud come AWS/Azure). Tu stai usando la loro stessa velocità contro di loro.
3. **Blocco dei Processi:** Se il bot tenta di analizzare il file alla ricerca di testo o password (o se prova a decomprimerlo), la sua CPU andrà al 100% cercando di processare dati casuali criptograficamente sicuri (che non hanno pattern).
### 4. Il tocco finale: L'Errore "Esasperante"
Per rendere il tutto più credibile, ogni tanto (diciamo il 10% delle volte) potresti simulare un errore di connessione interrotto a metà download.
> **Logica:** Il bot ha scaricato 90MB su 100MB, poi la connessione cade. Molti bot sono programmati per **riprovare da capo**. Questo crea un loop infinito di download falliti che consuma banda all'infinito senza mai ottenere un file completo.
### Riepilogo del tuo "Arsenale"
- **Livello 1-50:** L'IA lo confonde con dati falsi.
- **Livello 51-500:** Il Tarpit lo rallenta rendendo lo scraping lentissimo.
- **Livello 501+:** Il Binary Flood prova a saturare il suo hardware.

---
## Collegamenti
- Torna al corso: [[Dashboard H-NET]]