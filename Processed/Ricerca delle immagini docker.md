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
Per trovare immagini già pronte all’uso, pubblicate sul **registro ufficiale Docker Hub**, si utilizza il comando:
```
docker search <nome>
```
```
docker search ubuntu
```
Questo comando interroga Docker Hub e restituisce una lista di immagini che contengono nel nome o nella descrizione la parola “ubuntu”.  
L’obiettivo è individuare **immagini di base** (come sistemi operativi o servizi) da cui partire per costruire il proprio ambiente containerizzato.
L’output mostra:
- **NAME** → il nome dell’immagine o del repository
- **DESCRIPTION** → una breve descrizione del suo contenuto o utilizzo
- **STARS** → numero di valutazioni positive ricevute (indicatore di affidabilità)
- **OFFICIAL** → se l’immagine è mantenuta ufficialmente dal progetto
- **AUTOMATED** → se è generata automaticamente da un sistema di build continuo

> 💡 _Esempio_:  
> `ubuntu` è l’immagine ufficiale del sistema operativo Ubuntu, mantenuta dal team Canonical. Da essa derivano immagini come `ubuntu/apache2` o `ubuntu/postgres`, che contengono servizi preconfigurati.

## Link 
1) 