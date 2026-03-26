---
tipo: nota_lezione
corso: "Dashboard Udemy morroLinux Linux"
tags: [progetto, Linux, Udemy, morroLinux, certificazioni, Completed]
creato: 2026-03-25 23:30
---

# 📝 Lezione: approfondimento runlevel
**Corso:** [[Dashboard Udemy morroLinux Linux]]

---
## Contenuto
I **runlevel** possono essere confusi perché oggi, con i sistemi moderni (come Ubuntu, Fedora o Debian recenti), sono stati quasi del tutto sostituiti dai "Target" di **systemd**. Tuttavia, per l'esame LPI, è fondamentale capire la logica "classica" (SysVinit).
Immagina il runlevel come una **"modalità di funzionamento"** del computer. A seconda del numero (da 0 a 6), il sistema decide quali servizi attivare.


## 1. La gerarchia dei Runlevel (Lo standard LPI)

|Livello|Cosa succede?|Esempio pratico|
|---|---|---|
|**0**|**Arresto (Halt)**|Il sistema chiude tutto e si spegne.|
|**1 (o S)**|**Single User Mode**|Solo root può accedere. Niente rete, niente grafica. Serve per riparare il disco o resettare password.|
|**2**|**Multi-user (No rete)**|Più utenti possono loggarsi, ma la rete non è attiva (usato raramente).|
|**3**|**Multi-user + Rete**|**Il classico dei Server.** Hai la rete, hai molti utenti, ma solo riga di comando (niente mouse/finestre).|
|**4**|**Non definito**|Spazio libero per personalizzazioni (quasi mai usato).|
|**5**|**Grafico (X11)**|**Il classico dei Desktop.** È identico al 3, ma avvia anche il login grafico (GNOME, KDE, ecc.).|
|**6**|**Riavvio (Reboot)**|Il sistema chiude tutto e si riavvia.|

## 2. Come fa il sistema a sapere cosa avviare?
In passato (SysVinit), tutto girava intorno alla cartella `/etc/inittab` e alle cartelle `/etc/rcX.d/` (dove X è il numero del runlevel).
- Se entravi nel **Runlevel 3**, il sistema guardava dentro `/etc/rc3.d/`.
- Lì trovava dei file che iniziavano con **S** (Start) per avviare i servizi (es. `S01ssh`) o con **K** (Kill) per fermarli.

## 3. Il passaggio a Systemd (I "Target")
Oggi non usiamo più i numeri, ma i **Target**. Per l'esame devi conoscere le corrispondenze:
- **Runlevel 1** → `rescue.target`
- **Runlevel 3** → `multi-user.target`
- **Runlevel 5** → `graphical.target`

## 4. Comandi da ricordare (Fondamentali per l'esame)
Per vedere in che livello sei e cosa è successo prima:


```
runlevel
```

_(Ti risponde con due caratteri, es: `N 5`. Significa che prima non c'era un livello precedente (N) e ora sei nel 5)._
Per cambiare livello al volo (es. passare dal grafico alla riga di comando):

```
init 3
```
Per spegnere o riavviare (usando la logica dei runlevel):

```
init 0  # Spegne
init 6  # Riavvia
```

**Esercizio veloce per te:** Se sei su un server che non ha monitor e deve solo rispondere a richieste web, quale runlevel sceglieresti come predefinito? (La risposta corretta è il **3**, perché il 5 sprecherebbe risorse per una grafica che non vedrebbe nessuno).

---
## Collegamenti
- Torna al corso: [[Dashboard Udemy morroLinux Linux]]