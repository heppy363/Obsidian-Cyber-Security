---
aliases:
  - Completate
tags:
  - Completed
  - risorsePersonali
---
--- 
## Nozioni
`Si tratta di un sistema per il trasferimento di file da un PC al altra con diverso sistema operativo sulla stessa rete basato su SyncTrayzor`

> Scenario: mi interessa spostare o avere delle cartelle sempre sincronizzate tra due o piu PC sulla stessa rete in maniera indipendente dal sistema operativo 

### 1. Installazione sui due sistemi
#### **Su Windows 11**
1. Scarica l'installer di **SyncTrayzor** da [questo link](https://www.google.com/search?q=https://github.com/canton7/SyncTrayzor/releases/latest) (scarica il file `.exe` chiamato `SyncTrayzorSetup-x64.exe`).
2. Installalo come un normale programma.
3. Avvialo. Windows Firewall ti chiederà i permessi: **accetta entrambi** (Reti private e Reti pubbliche) per evitare blocchi nella rete locale.
#### **Su EndeavourOS (Arch based)**
1. Apri il terminale e digita:
```
sudo pacman -S syncthing
```
2. Ora installa anche un'interfaccia grafica per renderlo semplice come su Windows. Ti consiglio **Syncthing-GTK** (molto intuitivo):
```
sudo pacman -S syncthing-gtk
```
3. Avvia **Syncthing-GTK** dal tuo menu delle applicazioni. Al primo avvio ti chiederà di configurare il demone (il servizio), clicca su "Sì/Avvia".

### 2. Accoppiamento dei PC (Il "Matrimonio")
Ora dobbiamo far sì che il PC Windows e il PC Linux si conoscano.
1. **Su EndeavourOS (Syncthing-GTK):** Clicca sull'icona a forma di ingranaggio o "ID Dispositivo". Vedrai un codice lungo e un QR Code.
2. **Su Windows (SyncTrayzor):**
    - In basso a destra, clicca su **"+ Aggiungi Dispositivo Remoto"**.
    - Se sei fortunato e i PC sono già ben visibili in rete, vedrai l'ID del PC Linux apparire in blu sotto il campo di testo. Cliccaci sopra.
    - Altrimenti, copia l'ID da Linux e incollalo qui.
    - Dagli un nome, ad esempio "Mio-PC-Linux".
    - Clicca su **Salva**.
3. **Su EndeavourOS:** In pochi secondi apparirà una notifica o un banner in alto che dice: _"Il dispositivo Windows-PC vuole connettersi"_. Clicca su **Aggiungi**.

### 3. Sincronizzazione di una cartella
Facciamo una prova creando una cartella "Scambio" che esiste su entrambi.
1. **Su Windows:**
    - Nel pannello di sinistra, clicca su **"+ Aggiungi Cartella"**.
    - **Etichetta:** Scriviamo `Documenti_Condivisi`.
    - **Percorso:** Scegli la cartella che vuoi (es: `C:\Utenti\Tuonome\Scambio`).
    - Vai nella scheda **Condivisione** e metti la spunta su "Mio-PC-Linux".
    - Clicca su **Salva**.
2. **Su EndeavourOS:**
    - Apparirà un pop-up: _"Il PC Windows vuole condividere la cartella Documenti_Condivisi"_. Clicca su **Aggiungi**.
    - Ti chiederà dove salvarla sul tuo sistema Linux (es: `/home/tuonome/Scambio`).
    - Clicca su **Salva**.

### 4. Ultimo tocco: Avvio automatico
Per far sì che i file si sincronizzino senza che tu debba aprire i programmi ogni volta:
- **Su Windows:** SyncTrayzor di solito si imposta da solo per avviarsi con Windows (controlla nelle impostazioni del programma).
- **Su EndeavourOS:**
    - Se usi **Syncthing-GTK**, vai nelle sue impostazioni e spunta "Avvia all'accesso".
    - In alternativa, da terminale abilita il servizio di sistema così lavora in background:
```
systemctl --user enable syncthing.service
systemctl --user start syncthing.service
```

### Come capire se funziona?
- Se metti un file nella cartella su Windows, vedrai un'icona blu su Linux che indica il download.
- Quando la barra diventa verde con scritto **"Sincronizzato"**, i file sono identici su entrambi i PC.
**Nota per EndeavourOS:** Se hai il firewall attivo (ufw), ricordati di aprire le porte necessarie con `sudo ufw allow 22000/tcp` e `sudo ufw allow 21027/udp`, ma solitamente in una configurazione standard casalinga non serve.

## Link 
1) 