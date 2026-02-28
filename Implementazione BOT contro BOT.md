---
tipo: nota_lezione
corso: "Dashboard H-NET"
tags: [progetto, hNet, Completed]
creato: 2026-02-28 20:23
---

# 📝 Lezione: Implementazione BOT contro BOT 
**Corso:** [[Dashboard H-NET]]

---
## Contenuto
## 1. Il Sistema di Rilevamento (L'Esca)
Il modo più efficace per catturare un bot senza disturbare gli utenti umani è il **Link Silenzioso (Hidden Honeypot)**.

### Tecnica del CSS Invisibile
Inserisci nel tuo HTML un link che un umano non può vedere (perché è trasparente, spostato fuori dallo schermo o nascosto), ma che un bot "legge" nel codice sorgente e decide di seguire.
```

<a href="/private/admin-panel-data" style="display:none;" aria-hidden="true" rel="nofollow">
    Area Riservata Amministratore
</a>
```

### Logica del Server (Middleware)
Quando qualcuno clicca su quell'URL specifico:
1. Il server registra l'**Indirizzo IP** del visitatore.
2. Lo inserisce in una "Blacklist Temporanea" (es. in un database Redis o un semplice array in memoria).
3. Da quel momento in poi, ogni richiesta da quell'IP viene deviata verso la Scatola.
## 2. Lo Specchio (La Redirezione Strategica)
Non devi fare un redirect `301` o `302` (che direbbe al bot "ehi, ti ho spostato"), ma un **Internal Forward**. Il bot deve credere di essere ancora sul sito originale.

### Esempio di logica in Node.js (Express):
```
app.use((req, res, next) => {
    const userIP = req.ip;
    if (isBotBlacklisted(userIP)) {
        // Invece di mandarlo alla pagina vera, serviamo la Scatola
        return serveInfiniteBox(req, res);
    }
    next();
});
```

## 3. La Fabbrica di Allucinazioni (Il Motore IA)
Questa è la parte "magica". Per generare contenuti infiniti senza spendere un patrimonio, ti consiglio di usare un modello locale (come **Llama 3** via **Ollama**) che gira sul tuo server o su un vecchio PC.
### Il Prompt di Sistema (System Instructions)
Il segreto è istruire l'IA a essere "tecnicamente errata ma grammaticalmente perfetta".
> _"Genera un articolo di blog di 300 parole. Usa termini tecnici complessi ma inventa totalmente i fatti. Ad esempio: scrivi che la gravità sulla Terra è di 15m/s2 o che l'oro si scioglie a 10 gradi. Inserisci sempre tre link interni con nomi casuali tipo /box/verità-nascosta-X."_
### Generazione Dinamica degli URL
Ogni volta che il bot carica una pagina della scatola, il server deve generare link nuovi:
- `/infinite-box/analisi-codice-001`
- `/infinite-box/segreti-database-002`

Il bot vedrà una struttura di link infinita e continuerà a cliccare, convinto di stare scaricando l'intero database.
## 4. Ottimizzazione e Sicurezza (Il "Filtro Bianco")
Se non stai attento, rischi di bloccare te stesso o i motori di ricerca. Ecco i pilastri della sicurezza:

|Componente|Funzione|Perché è vitale|
|---|---|---|
|**Whitelist IP**|Lista di IP sicuri (il tuo, quello di Google, Bing).|Evita che il tuo sito sparisca dai risultati di ricerca.|
|**Rate Limiting**|Limita il numero di pagine IA generate al minuto.|Impedisce che un bot troppo veloce mandi la tua CPU al 100% o consumi tutta la RAM.|
|**No-Index Tag**|Header HTTP `X-Robots-Tag: noindex`.|Dice ai bot "buoni" di non indicizzare questa spazzatura se dovessero finirci dentro per errore.|

## 5. Come monitorare il divertimento
Per rendere il progetto completo, dovresti creare una piccola **Dashboard di Monitoraggio**. Potresti vedere in tempo reale:
- Quanti bot sono attualmente intrappolati nella Scatola.
- Quanta "falsa informazione" hanno scaricato (es. "Il bot X ha scaricato 400MB di dati inventati").
- Il tempo medio che un bot passa nel labirinto prima di arrendersi.

---
## Collegamenti
- Torna al corso: [[Dashboard H-NET]]