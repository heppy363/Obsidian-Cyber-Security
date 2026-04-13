---
tipo: nota_lezione
corso: "Dashboard Python"
tags: [progetto, linguaggiProg, python, uni, programmazione, Completed]
creato: 2026-03-26 21:19
---

# 📝 Lezione: Micro python
**Corso:** [[Dashboard Python]]

---
## Contenuto

```
micro_python/
├── src/
│   └── micro_std/             # Il pacchetto principale
│       ├── __init__.py        # Espone le funzioni principali
│       ├── core.py            # Funzioni built-in (map, filter, enumerate)
│       ├── types.py           # Implementazioni di List, Dict, etc.
│       ├── math.py            # Funzioni matematiche base
│       └── itertools.py       # Iteratori personalizzati
├── tests/                     # Cartella dedicata ai test
│   ├── test_core.py
│   ├── test_math.py
│   └── test_types.py
├── examples/                  # Script per mostrare come si usa
│   └── demo.py
└── README.md                  # Documentazione del progetto
```

## Architettura del Sistema
Il progetto adotta una struttura **`src/` layout**, standard de facto per la distribuzione di pacchetti Python, per garantire una netta separazione tra codice sorgente e test.

## Componenti Principali:

|Modulo|Descrizione|Corrispettivo Reale|
|---|---|---|
|`micro_std.core`|Funzioni universali (built-ins)|`builtins`|
|`micro_std.itertools`|Strumenti per iterazione efficiente|`itertools`|
|`micro_std.math`|Funzioni matematiche e costanti|`math`|
|`micro_std.types`|Implementazione di tipi di dato complessi|`collections` / `types`|

## Standard di Sviluppo

## Implementazione "Pure Python"
- **Nessuna dipendenza esterna**: È vietato l'uso di librerie fuori dalla std-lib originale (e idealmente, si cerca di non usare nemmeno quella).
- **Protocolli**: Ogni funzione deve rispettare i protocolli di Python (es. `__iter__`, `__next__`, `__call__`).
- **Documentazione interna**: Ogni funzione deve avere una _Docstring_ che ne spieghi il comportamento e la complessità computazionale O(n).
## Testing & Qualità
Il progetto segue un approccio **Test-Driven** (o quasi). Ogni funzione in `micro_std` deve essere validata contro il comportamento della funzione originale di Python.
- **Tool**: `unittest` o `pytest`.
- **Requisito**: Il test passa solo se l'output di `micro_std.func()` è identico a `builtins.func()`.

## 4. Guida all'Installazione (Sviluppo)
Per lavorare al progetto mantenendo i path corretti:
1. Clona la repository.
2. Crea un ambiente virtuale: `python -m venv venv`.
3. Installa in modalità editabile:

```
pip install -e .
```

_(Nota: richiede un file `pyproject.toml` o `setup.py` nella root)._
## 5. Roadmap Iniziale
- [ ] Setup della struttura cartelle e configurazione `pytest`.
- [ ] Implementazione funzioni base in `core.py` (`enumerate`, `zip`, `range`).
- [ ] Implementazione dei primi iteratori in `itertools.py` (`chain`, `cycle`).
- [ ] Creazione di una suite di test automatizzata.



---
## Collegamenti
- Torna al corso: [[Dashboard Python]]