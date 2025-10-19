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
Docker e altre aziende del settore hanno aderito alla **Open Container Initiative (OCI)**, un’organizzazione che definisce **specifiche comuni** per la creazione, la distribuzione e l’esecuzione delle immagini container.
Lo standard **OCI Image Specification** stabilisce come devono essere strutturati i metadati, i layer e le configurazioni di un’immagine, in modo che **ogni container engine (Docker, Podman, containerd, ecc.) sia in grado di interpretarla e utilizzarla correttamente**.
Questo significa che un’immagine creata con Docker può essere eseguita anche con altri strumenti compatibili con lo standard OCI, senza necessità di conversione o adattamento.  
In altre parole, lo standard OCI **svincola il formato dell’immagine dall’implementazione specifica del container engine**, favorendo la portabilità e la collaborazione tra ecosistemi diversi.

## Link 
1) 