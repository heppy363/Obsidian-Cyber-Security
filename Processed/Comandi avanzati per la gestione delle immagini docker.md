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
Oltre ai comandi di base, Docker offre numerose opzioni avanzate per ispezionare, esportare, e manipolare le immagini in modo professionale.

| Comando                                             | Descrizione                                                                                                            |
| --------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------- |
| docker image inspect <nome>                         | Mostra i **metadati dettagliati** di un’immagine (configurazioni, variabili d’ambiente, architettura, punti di mount). |
| docker tag <id> <nome>:<versione>                   | Assegna un **nuovo tag** o nome a un’immagine esistente. Utile per versionare o rinominare.                            |
| docker save -o <file.tar> <nome>                    | Esporta un’immagine in un file `.tar` (backup o trasferimento manuale).                                                |
| docker load -i <file.tar>                           | Importa un’immagine salvata precedentemente con `docker save`.                                                         |
| docker import <file.tar>                            | Crea una nuova immagine a partire da un archivio tar di un file system.                                                |
| docker export <id_container> -o <file.tar>          | Esporta il file system di un container in esecuzione come archivio tar.                                                |
| docker image rm $(docker images -q)                 | Rimuove **tutte** le immagini presenti nel sistema.                                                                    |
| docker image prune -a                               | Rimuove **tutte le immagini inutilizzate**, non solo quelle “dangling”.                                                |
| docker search --filter "is-official=true" <termine> | Filtra la ricerca mostrando solo le immagini ufficiali.                                                                |
| docker image build -t <nome>:<tag> .                | Costruisce una nuova immagine a partire da un `Dockerfile` nella directory corrente.                                   |
| docker image inspect --format '{{.Size}}' <nome>    | Restituisce solo la dimensione effettiva dell’immagine, utile per script di manutenzione.                              |


## Link 
1) 