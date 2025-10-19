---
aliases:
  - Completate
tags:
  - Completed
  - Docker
---
--- 
## Nozioni
Un **registro Docker** è un servizio che **memorizza e gestisce un insieme di [[Le repository in docker]]**. 
In altre parole, si può immaginare il registro come un **database centralizzato** o una **piattaforma di distribuzione** che funge da archivio per tutte le immagini containerizzate.  
Attraverso il registro, gli sviluppatori possono **pubblicare (push)** le proprie immagini e **scaricarle (pull)** su altri sistemi in modo semplice e standardizzato.
Il registro rappresenta dunque **il punto di incontro tra sviluppo e distribuzione**:  
gli sviluppatori creano immagini localmente, le inviano al registro, e successivamente altri sistemi (come server di produzione o orchestratori come Kubernetes) possono scaricarle per eseguirle.
Il registro più noto e utilizzato è **Docker Hub**, il servizio ufficiale offerto da Docker Inc., che ospita sia immagini pubbliche che private.  
Tuttavia, esistono anche registri alternativi, pubblici o privati, come **GitHub Container Registry**, **Google Container Registry (GCR)**, **Amazon Elastic Container Registry (ECR)** o **Harbor** per ambienti aziendali on-premise.
In contesti professionali, l’utilizzo di registri privati consente di mantenere **un controllo maggiore sulla sicurezza e sulla gestione delle versioni** delle immagini, evitando di esporre pubblicamente componenti software sensibili.
## Link 
1) 