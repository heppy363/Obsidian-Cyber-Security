---
aliases:
  - Completate
tags:
  - Completed
  - Docker
  - Immagini
---
--- 
## Nozioni
- **Usare immagini ufficiali o verificate**: garantiscono sicurezza e aggiornamenti continui.
- **Specificare sempre il tag di versione**: evitare `latest` per mantenere la riproducibilità.
- **Ridurre i layer**: combinare più comandi `RUN` o `COPY` nel Dockerfile per ridurre dimensione e complessità.
- **Rimuovere dipendenze temporanee**: durante la build, eliminare cache e file non necessari per mantenere l’immagine leggera.
- **Monitorare lo spazio disco**: usare periodicamente `docker system df` e `docker image prune` per evitare accumuli.
- **Usare tag semantici**: ad esempio `app:1.0`, `app:stable`, `app:test` per distinguere ambienti e versioni.

## Link 
1) 