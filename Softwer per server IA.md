---
aliases:
  - Completate
tags:
  - Completed
  - H-net
  - IA
---
--- 
## Nozioni
`Tutto il softwer necessario per fare girare i miei modelli IA`
## Configurazione Software (Il tocco finale)
Una volta assemblato tutto, per farle lavorare insieme come un'unica "super-memoria":
1. **BIOS:** Abilita assolutamente **"Above 4G Decoding"** e metti il supporto PCIe su **Gen3**. Disabilita il **CSM**.
2. **OS:** Installa **Ubuntu Server**.
3. **Drivers:** Installa i driver NVIDIA serie "Data Center".
4. **Sommare la VRAM:**
    - Se usi **Ollama**: Non devi fare nulla. Ollama rileva le tre GPU (0, 1, 2) e distribuisce i "layer" del modello in automatico. Vedrai nei log qualcosa come: `Llama-3-70B: 28 layers on GPU0, 28 on GPU1, 24 on GPU2`.
    - **Velocità:** Poiché le P40 usano il bus PCIe per comunicare (non avendo NVLink), avrai una piccola perdita di prestazioni rispetto a una scheda singola gigante, ma con 72GB di VRAM potrai fare cose che nessun altro PC da 1000€ può fare.
## 1. Esporre le IA sulla tua rete (API)
Il software che installerai sul server (Ollama o LocalAI) di default ascolta solo le richieste che provengono dal server stesso (`localhost`). Per usarlo dal tuo PC fisso, devi "aprirlo".
### Come fare con Ollama:
Sull'Ubuntu Server, devi modificare la configurazione del servizio:
1. Digita: `sudo systemctl edit ollama.service`
2. Aggiungi queste righe sotto `[Service]`:
```

[Service]
Environment="OLLAMA_HOST=0.0.0.0"
Environment="OLLAMA_ORIGINS=*"
```
1. Salva e riavvia: `sudo systemctl daemon-reload && sudo systemctl restart ollama`
Ora il tuo server IA è in ascolto sulla porta `11434`. Se l'IP del tuo server è `192.168.1.50`, dal tuo PC fisso potrai interrogarlo semplicemente puntando a quell'indirizzo.
## 2. L'interfaccia grafica: Open WebUI
Invece di usare il terminale, installerai sul server **Open WebUI**. È un'interfaccia bellissima che gira nel browser.
- **Cosa fa:** Ti permette di chattare con i tuoi modelli, caricare documenti (RAG), e creare "Agenti" personalizzati.
- **Come si usa:** Una volta installata (via Docker), dal tuo PC fisso scriverai nel browser `http://192.168.1.50:3000`. Avrai la tua versione privata e potentissima di ChatGPT.
## 3. Collegare n8n alle tue IA
Se hai un altro server con **n8n**, puoi creare automazioni incredibili (es: "Leggi questa email, chiedi al server IA di riassumerla e mandami un messaggio su Telegram").
In n8n, userai il nodo **Ollama** (o il nodo HTTP Request):
- **Base URL:** Inserirai `http://192.168.1.50:11434`

- **Modello:** Scriverai il nome del modello caricato (es. `llama3:70b`)
- **Authentication:** Di default non serve, perché sei nella tua rete locale protetta.

## 4. Architettura Finale: Come comunicano tra loro
```
graph TD
    A[Tuo PC Fisso / Smartphone] -- Browser (Porta 3000) --> B[Open WebUI]
    C[Server n8n] -- Chiamate API (Porta 11434) --> D[Ollama / LocalAI]
    B -- Gestisce i modelli --> D
    D -- Distribuisce il calcolo --> E[GPU Tesla P40 #1]
    D -- Distribuisce il calcolo --> F[GPU Tesla P40 #2]
    D -- Distribuisce il calcolo --> G[GPU Tesla P40 #3]
```
### Perché questa struttura è perfetta?
1. **Potenza Centralizzata:** Le GPU scaldano e consumano nel server (magari in un'altra stanza), ma tu le usi comodamente dal tuo ufficio.
2. **API Standard:** Usando il protocollo di Ollama o quello compatibile con OpenAI, puoi collegare qualsiasi software esistente (n8n, Flowise, LangChain) senza cambiare configurazione.
3. **Privacy Totale:** Nessun dato esce mai dalla tua rete locale.
## Un consiglio sulla sicurezza
Dato che queste schede non hanno password di default sulle API, **non aprire mai la porta 11434 sul router verso internet**. Se vuoi usare le tue IA quando sei fuori casa, installa sul server **Tailscale** o una **VPN**: potrai accedere in sicurezza come se fossi seduto davanti al server.

## Link 
1) 