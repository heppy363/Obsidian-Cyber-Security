---
aliases:
  - Completate
tags:
  - Completed
  - cercatoreLavoro
  - progettiPersonali
---
--- 
## Nozioni
`Metodologia della gestione degli errori questo e un progglema perche bannano gli indirizzi IP`
### 1. Errori di Rete e "Anti-Bot" (Il muro dei siti)
I siti web non vogliono essere scansionati. Quando il tuo bot accede, il server analizza la tua "impronta". Se capisce che sei un bot, ti blocca.
- **L'errore:** `403 Forbidden` o `429 Too Many Requests`.
- **La Soluzione (Proxy Rotation):** Non puoi usare il tuo IP di casa. Devi usare un provider (come Bright Data o ZenRows) che funge da "ponte". Il tuo script invia la richiesta al proxy, e il proxy la inoltra al sito usando ogni volta un IP diverso (residenziale).
- **Gestione Tecnica:** Se ricevi un `429`, il task non deve morire. Deve sollevare un'eccezione che dice all'orchestratore (Prefect): _"Ehi, mi hanno beccato. Mettimi in pausa per 5 minuti e riprova con un altro IP"_.
### 2. Errori di Parsing e Contenuto (Siti "Rotto" o Diversi)
Non tutti i siti sono uguali. Alcuni non hanno tag `<h1>`, altri sono interamente in Flash (vecchissimi), altri ancora bloccano il caricamento se non accetti i cookie.
- **L'errore:** `TimeoutError` (il sito non carica) o `AttributeError` (cerchi il titolo ma non esiste).
- **La Soluzione (Graceful Degradation):** Il bot deve essere "gentile" con i fallimenti. Se non riesce a trovare la data di creazione del sito, deve comunque salvare il resto delle informazioni (nome, categoria, telefono) marchiando il campo data come `NULL` o `Unknown`.
- **Analisi AI:** Se il parsing HTML fallisce, puoi passare lo screenshot della pagina (catturato con Playwright) a GPT-4o-vision: _"Non riesco a leggere il codice, dimmi tu guardando la foto di cosa si occupa questa azienda"_.
### 3. Errori di Stato e Persistenza (Il crash del sistema)
Cosa succede se la corrente salta mentre l'agente sta processando il lead n. 450 di 1000?
- **L'errore:** Perdita dei dati non salvati e duplicazione dei contatti (se riparti da zero, rischi di mandare due volte la stessa mail al cliente).
- **La Soluzione (Idempotenza):** Ogni lead deve avere uno stato nel database.
    - **Workflow:**
        1. Scrittura nel DB con stato `PENDING`.
        2. L'agente prende solo i lead `PENDING`.
        3. Inizia l'analisi -> Stato `PROCESSING`.
        4. Fine analisi -> Stato `COMPLETED`.
- Se il sistema crasha, al riavvio cercherà solo quelli rimasti in `PENDING` o `PROCESSING` da troppo tempo.

| **Tipo Errore**        | **Strumento**      | **Strategia**                            |
| ---------------------- | ------------------ | ---------------------------------------- |
| **IP Ban**             | Proxy Rotativi     | Cambia IP e aspetta (Backoff).           |
| **Sito Lento**         | Playwright Timeout | Chiudi la connessione dopo 30s.          |
| **Sito Moderno (SPA)** | Playwright Stealth | Aspetta il caricamento dei selettori JS. |
| **Crash Script**       | PostgreSQL Status  | Riprendi dal lead non ancora completato. |

## Link 
1) 