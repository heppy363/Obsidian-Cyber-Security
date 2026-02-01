---
aliases:
  - Completate
tags:
  - Completed
  - IA
  - ClaudIA
  - whindows
---
--- 
## Nozioni
# Ralph on Windows: Autonomous AI Coding Loop
Questa guida spiega come configurare e far girare **Ralph**, l'agente autonomo basato su **Claude Code (Anthropic)**, in un ambiente **Windows**. Ralph permette di automatizzare lo sviluppo di intere User Stories leggendo un file di requisiti (`prd.json`) e lavorando in un loop continuo finché l'obiettivo non è raggiunto.
## Perché questa versione?
Claude Code è nativamente pensato per ambienti Unix-like. Su Windows, gli sviluppatori incontrano tre ostacoli principali che questa configurazione risolve:
1. **Percorsi dei file**: Differenza tra `C:\Users` e `/c/Users`.
2. **Fine riga (Line Endings)**: Conflitto tra CRLF (Windows) e LF (Linux).
3. **Spazi nei percorsi**: Cartelle come `Progetti AI` rompono gli script Bash se non protette.
## Prerequisiti
1. **Abbonamento Claude Pro**: Necessario per accedere ai limiti di messaggi della CLI.
2. **Claude Code CLI**: Installato nativamente.
    - Comando: `powershell -c "irm https://claude.ai/install.ps1 | iex"`
3. **Git for Windows**: Per avere **Git Bash** (fondamentale per eseguire lo script `.sh`).
4. **UV (Astral)**: Consigliato per la gestione ultra-rapida di Python.
    - Comando: `powershell -c "irm https://astral.sh/uv/install.ps1 | iex"`

## Struttura del Progetto
```
📂 Il_Tuo_Progetto/
├── 📄 ralph.sh          # Il cuore dell'automazione (Bash)
├── 📄 prd.json           # La "mente": contiene le User Stories e gli obiettivi
├── 📄 progress.txt       # Log di tutto ciò che Claude scrive e fa
├── 📁 tasks/             # (Opzionale) Task granulari generati dall'IA
└── 📁 src/               # Il codice generato apparirà qui
```

## Configurazione dei File
#### 1. Il file `ralph.sh` (Versione Windows)
Questo script gestisce il loop. **Importante:** In VS Code, assicurati che la codifica del file sia impostata su **LF** (non CRLF).
```
#!/bin/bash
set -e

# CONFIGURAZIONE PERCORSO WINDOWS
CLAUDE_BIN="C:/Users/$(whoami)/.local/bin/claude.exe"
SCRIPT_DIR="$(cd "$(dirname "${BASH_SOURCE[0]}")" && pwd)"
PRD_FILE="$SCRIPT_DIR/prd.json"
PROGRESS_FILE="$SCRIPT_DIR/progress.txt"

# Inizializzazione
echo "# Ralph Progress Log - $(date)" > "$PROGRESS_FILE"

for i in $(seq 1 50); do
  echo ">>> Iterazione $i"
  
  # Prompt di innesco basato sul PRD
  PROMPT="Analizza prd.json. Implementa la prima User Story con 'passes': false. Usa 'uv' per dipendenze e test. Aggiorna prd.json quando finisci una US. Termina con <promise>COMPLETE</promise>."

  # Esecuzione Claude Code
  OUTPUT=$(echo "$PROMPT" | "$CLAUDE_BIN" --dangerously-skip-permissions --print 2>&1 | tee -a "$PROGRESS_FILE") || true

  # Verifica completamento
  if echo "$OUTPUT" | grep -q "<promise>COMPLETE</promise>"; then
    echo "Task completato!"
    exit 0
  fi
  sleep 2
done
```
#### 2. Il file `prd.json`
È il documento che guida l'agente. Ecco uno schema base:
```
{
  "project": "NomeProgetto",
  "objective": "Descrizione macro dell'app",
  "userStories": [
    {
      "id": "US-001",
      "title": "Scaffolding",
      "acceptanceCriteria": ["pyproject.toml creato", "cartella src creata"],
      "passes": false
    }
  ]
}
```
## Come avviare Ralph
1. Apri la cartella in **VS Code**.
2. Apri il terminale e seleziona **Git Bash** dal menu a tendina.
3. Rendi lo script eseguibile (solo la prima volta):
```
chmod +x ralph.sh
```
4. Lancia il loop:
```
./ralph.sh --tool claude 20
```
## Risoluzione Problemi comuni su Windows
- **Error: No such file or directory**: Controlla che non ci siano spazi nei nomi delle cartelle superiori. Se ci sono, rinominale (es. da `Miei Progetti` a `Miei_Progetti`).
- **Caratteri strani nel log ()**: Accade quando PowerShell e Bash si scambiano dati. Assicurati che tutti i file siano salvati in **UTF-8 senza BOM**.
- **Claude non scrive file**: Verifica di aver aggiunto il flag `--dangerously-skip-permissions` nello script, altrimenti Claude si bloccherà aspettando un "Sì" manuale che non può dare nel loop.


## Link 
1) 