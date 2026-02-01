---
aliases:
  - Completate
tags:
  - Completed
  - blog
  - progettiPersonali
  - CI/CD
---
--- 
## Nozioni
`Si tratta di un esempio di configurazione su una macchina virtuale di Gitea tramite docker` 

1) Configurazione del area 
	1) Creazione della cartella necessaria `mkdri cicd-setup` 
	2) creazione del file `docker-compose.yml` 
```
services:
  # Il server GIT (stile GitHub)
  gitea:
    image: gitea/gitea:1.21
    container_name: gitea
    environment:
      - USER_UID=1000
      - USER_GID=1000
      - GITEA__actions__ENABLED=true # Abilita le Actions già all'avvio
    restart: always
    networks:
      - cicd_net
    ports:
      - "3000:3000"
      - "2222:22"
    volumes:
      - ./gitea_data:/data
      - /etc/timezone:/etc/timezone:ro
      - /etc/localtime:/etc/localtime:ro

  # Il magazzino per le tue immagini Docker
  registry:
    image: registry:2
    container_name: docker-registry
    restart: always
    networks:
      - cicd_net
    ports:
      - "5000:5000"
    volumes:
      - ./registry_data:/var/lib/registry

networks:
  cicd_net:
    driver: bridge
```
2) Una volta configurato il file si puo lanciare il servizio con il seguente comando `docker compose up -d`
3) Dopo aver lanciato il comando di build, controllare lo stato dei container, con il seguente comando `docker ps
	1) in questo caso devono essere attivi _gitea_ e _docker-registry_ 
4) Accedere al interfaccia web di gitea lo si fa connetendosi al host sulla specifica porta in questo caso `http://192.168.178.200:3000/` si noti che l'indirizzo IP e quello impostato nel file di configurazione della rete macchina virtuale controllare qui [[Configurazione di una macchina virtuale in modalita Bridge]]
	1) da notare che e meglio al momento non procedere con HTTPS dato che i certificati ssl non sono stati configurati correttamente e questo puo dare il seguente errore _SSL_ERROR_RX_RECORD_TOO_LONG_ (su firefox) 
5) Configurare l'installazione di ghitea in questo caso essendo una prova lascio tutto standard da controllare 
	1) la porta SSH
	2) L'url di base indirizzo e porta del server 
	3) Creazione di un account admin 
		1) heppy
		2) 1234


## Link 
1) 