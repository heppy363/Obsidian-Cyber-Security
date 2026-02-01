---
aliases:
  - Completate
tags:
  - Completed
  - progettiPersonali
  - blog
  - CI/CD
---
--- 
## Nozioni
Nel caso laciando questo comando `sudo docker logs gitea-runner` da sottolineare che il nome del conteiner potrebbe camiare si veda la seguente scritta `unknown: runner registration token not found` vuoldire che il token non e piu valido queto puo accadere per molti motivi il primo il tempo scaduto 

## Risoluzione 
1) Generre un nuovo tocken e metterlo nel file `docker-compose-runner.yml` 
	1) fermare il container docker `sudo docker compose -f docker-compose-runner.yml down`
	2) Pulire i dati di registrazione `sudo rm -rf ./runner_data/* sudo docker compose -f docker-compose-runner.yml up -d`
	3) Ri far partire il servizio 
2) Per controllare che tutto funzioni si deve procedere a rifare il comando 
	1) `sudo docker logs -f gitea-runner` 
	2) Controllare se non vi sono piu degli errori legati al token 



## Link 
1) 