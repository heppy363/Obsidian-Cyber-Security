---
aliases:
  - Completate
tags:
  - Completed
  - Morrolinux
  - videoYT
---
--- 
## Nozioni
### 1. **Obiettivo del progetto**
Winboat è un **applicativo open source** progettato per consentire l’esecuzione di **applicazioni Windows su sistemi Linux** in modo semplice, isolato e riproducibile.  
L’idea di base è combinare la **virtualizzazione** (Windows in una VM) con la **containerizzazione** (Docker) per ottenere un ambiente flessibile e facilmente distribuibile.
### 2. **Architettura generale**
Winboat si basa su **tre livelli principali**:
1. **Host Linux**
    - Sistema operativo principale dell’utente.
    - Esegue Docker e gestisce le risorse di calcolo.
    - Mostra il flusso video delle app Windows tramite RDP (Remote Desktop Protocol).
2. **Container Docker**
    - Contiene tutto il necessario per avviare e gestire la macchina virtuale Windows.
    - Isola completamente l’ambiente di esecuzione, evitando conflitti con librerie o dipendenze del sistema host.
    - Può essere facilmente distribuito o replicato su altri sistemi Linux.
3. **Macchina Virtuale Windows**
    - Viene eseguita all’interno del container.
    - Ospita le applicazioni Windows desiderate.
    - Comunica con l’host tramite **RDP** o un protocollo simile, permettendo la visualizzazione e l’interazione diretta con le app dall’ambiente Linux.
### 3. **Flusso operativo**
1. L’utente avvia **Winboat** sul sistema Linux.
2. Winboat esegue un **container Docker** preconfigurato che contiene:
    - Un hypervisor o un gestore di macchine virtuali (es. QEMU/KVM, VirtualBox headless, ecc.).
    - Un’istanza di **Windows** installata e configurata per l’uso remoto.
3. All’interno del container viene avviata la **macchina virtuale Windows**.
4. L’ambiente host si connette via **RDP** alla VM, integrando:
    - **Flusso video** dell’applicazione Windows.
    - **Input** da tastiera e mouse.
    - Eventualmente **condivisione file** o clipboard.
5. Il risultato: le app Windows appaiono come se fossero eseguite nativamente sul desktop Linux.

## Link 
1) 