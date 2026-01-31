---
aliases:
  - Completate
tags:
  - Completed
  - Esadecimale
  - videoYT
---
--- 
## Nozioni
YouTube oggi usa complessi algoritmi di _Machine Learning_ per suggerire contenuti basandosi sul tuo comportamento (cronologia, tempo di visione, interazioni).  
Questo porta spesso a una **perdita di controllo** su ciò che guardi — sei “guidato” da ciò che massimizza il _watch time_, non da ciò che vuoi effettivamente vedere.
L’obiettivo è **recuperare il controllo** e **seguire solo ciò che scegli tu**, senza passare dall’algoritmo.  
Questo è possibile con il vecchio ma ancora potente **RSS (Really Simple Syndication)**.

### Cos’è un feed RSS di YouTube
Ogni canale YouTube (anche playlist o ricerca) ha un proprio **feed RSS**, cioè un file XML aggiornato automaticamente con i nuovi video.  
Tu puoi “iscriverti” a questo feed usando un **lettore RSS** (RSS client), invece di usare l’interfaccia di YouTube o l’algoritmo.

##### Struttura di un feed RSS YouTube
Un feed RSS è un file XML accessibile via URL.  
Esempio per un canale YouTube:
```
https://www.youtube.com/feeds/videos.xml?channel_id=UCxxxxxxxxxxxx
```
Oppure per una playlist:
```
https://www.youtube.com/feeds/videos.xml?playlist_id=PLxxxxxxxxxxxx
```

Oppure per una ricerca (meno affidabile, ma possibile tramite servizi esterni tipo `https://rssbox.herokuapp.com/` o `https://fetchrss.com/`).

#### Come ottenere l’ID del canale YouTube
1. Vai sul canale YouTube.
2. Apri la pagina e copia l’URL.
    - Se è del tipo:  
        `https://www.youtube.com/channel/UCabc123xyz...` → **l’ID è tutto ciò dopo “channel/”**
    - Se è del tipo:  
        `https://www.youtube.com/@nomecanale` → vai su  
        `https://www.youtube.com/@nomecanale/about`  
        e visualizza sorgente pagina (`Ctrl+U`), poi cerca `channelId`.

```
"channelId":"UCabc123xyz..."
```
Ora puoi creare il tuo feed RSS:
```
https://www.youtube.com/feeds/videos.xml?channel_id=UCabc123xyz...
```

### Lettori RSS (client) su Linux

1. **Elfeed (per Emacs)**
Uno dei client RSS più potenti, integrato nell’ecosistema Emacs.
##### Installazione
Se hai già Emacs:
```
M-x package-install RET elfeed RET
```
Configurazione base (`~/.emacs` o `~/.emacs.d/init.el`)
```
(setq elfeed-feeds
      '("https://www.youtube.com/feeds/videos.xml?channel_id=UCxxxxxxxxxxxx"
        "https://www.youtube.com/feeds/videos.xml?channel_id=UCyyyyyyyyyyyy"))
```
#### Uso
- Apri Elfeed: `M-x elfeed`
- Aggiorna i feed: `G`
- Scorri i video: frecce su/giù
- Apri un video nel browser: `RET`  
    (usa il link diretto a YouTube senza suggerimenti)
✅ Vantaggio: totale controllo, interfaccia testuale, nessuna tracciabilità, integrazione con player esterni (es. `mpv`).

2. **Newsboat (CLI RSS reader)**
Perfetto per chi ama la riga di comando. Leggerissimo e funzionale.
##### Installazione
Su Debian/Ubuntu:
```
sudo apt install newsboat
```
Su Arch:
```
sudo pacman -S newsboat
```
###### Configurazione (`~/.newsboat/urls`)
Aggiungi i tuoi feed YouTube:
```
https://www.youtube.com/feeds/videos.xml?channel_id=UCxxxxxxxxxxxx
https://www.youtube.com/feeds/videos.xml?channel_id=UCyyyyyyyyyyyy
```

Uso
```
newsboat
```

Comandi principali:
- `r` → aggiorna tutti i feed
- `Enter` → apri l’articolo/video nel browser
- `q` → esci
✅ Puoi anche aprire i video direttamente in **mpv** senza browser:  
Aggiungi a `~/.newsboat/config`:

```
macro v set browser "mpv %u"; open-in-browser; set browser "xdg-open %u"
```

Così con `v` apri il video direttamente in **mpv**, senza YouTube UI.

3. **GUI client (interfaccia grafica)**

Se preferisci qualcosa di visivo:
- **Liferea** → semplice, classico, supporta YouTube feed.
```
sudo apt install liferea
```
**Akregator** (KDE)
```
sudo apt install akregator
```
Entrambi ti permettono di aggiungere feed, organizzare canali, e visualizzare anteprime video.



## Link 
1) 