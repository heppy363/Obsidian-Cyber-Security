---
tipo: nota_lezione
corso: "Dashboard progetti personali"
tags: [progetto, progettiPersonali, Completed]
creato: 2026-03-25 22:52
---

# 📝 Lezione: D-bus
**Corso:** [[Dashboard progetti personali]]

---
## Contenuto

## D-Bus (Desktop Bus)
D-Bus è un sistema di **Inter-Process Communication (IPC)** che permette a più applicazioni di comunicare tra loro, scambiarsi messaggi e invocare funzioni in modo standardizzato.
## 1. I due Bus principali
D-Bus opera solitamente su due livelli (istanze) separati:
- **System Bus:** Un'unica istanza per tutto il sistema. Viene avviata al boot (`dbus-daemon`). Gestisce eventi critici come l'aggiunta di nuovo hardware, lo stato della rete o lo spegnimento del sistema.
- **Session Bus:** Un'istanza per ogni utente che effettua il login. Gestisce la comunicazione tra le applicazioni desktop dell'utente (es. l'integrazione tra il player musicale e la barra delle notifiche).

## 2. Evoluzione: Da HAL a udev
Qui è dove dobbiamo fare una precisione importante per l'architettura attuale:
- **HAL (Hardware Abstraction Layer):** È effettivamente **deprecato** da anni. Un tempo serviva a fornire un database centralizzato dell'hardware, ma era pesante e ridondante.
- **udev:** È il moderno gestore dei dispositivi di Linux. Quando colleghi una periferica (es. una chiavetta USB), il **Kernel** invia un segnale a **udev**.
- **Il flusso attuale:** Il Kernel rileva l'hardware → **udev** crea il file in `/dev` e gestisce i permessi → **udev** (o un demone come `upower` o `NetworkManager`) invia un messaggio su **D-Bus** → Il Desktop Environment (GNOME/KDE) riceve la notifica e mostra l'icona sul desktop.

## 3. Concetti Chiave per l'esame LPI
- **Oggetti e Percorsi:** Ogni servizio su D-Bus ha un percorso (es. `/org/freedesktop/NetworkManager`).
- **Metodi e Segnali:** Le app possono chiamare un **Metodo** (es. "Connettiti al Wi-Fi") o restare in ascolto di un **Segnale** (es. "Batteria scarica").
- **Indipendenza dall'Hardware:** D-Bus astrae i dettagli tecnici. L'applicazione non deve sapere _come_ il kernel parla con il modulo Wi-Fi, deve solo sapere che il servizio `NetworkManager` è disponibile sul Bus.

## Strumenti Utili (Command Line)
Per l'esame e per il troubleshooting, tieni a mente questi comandi:
1. `dbus-send`: Per inviare messaggi manualmente al bus.
2. `dbus-monitor`: Per vedere in tempo reale i messaggi che transitano sul bus (molto utile per capire cosa succede "sotto il cofano").
3. `busctl`: Lo strumento moderno (parte di systemd) per interagire con D-Bus.

## Tabella Riassuntiva

|Componente|Ruolo|
|---|---|
|**Kernel**|Rileva l'hardware a basso livello.|
|**udev**|Gestisce i nodi in `/dev` e le regole dei dispositivi.|
|**D-Bus**|Il "postino" che trasporta la notizia dell'evento alle app.|
|**HAL**|Obsoleto/Deprecato (sostituito dalle funzionalità di udev e systemd).|


Si tratta di un messag bus sistem 
![[Pasted image 20260325225307.png]]

### Stato aggiornato del architettura 
![[Pasted image 20260325225651.png]]




---
## Collegamenti
- Torna al corso: [[Dashboard progetti personali]]