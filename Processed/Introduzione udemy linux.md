---
tipo: nota_lezione
corso: "Dashboard Udemy morroLinux Linux"
tags: [progetto, Linux, Udemy, morroLinux, certificazioni, Completed]
creato: 2026-03-18 22:35
---

# 📝 Lezione: Introduzione
**Corso:** [[Dashboard Udemy morroLinux Linux]]

---
## Contenuto
## 1. Il Panorama delle Distribuzioni Linux
Le distribuzioni (o "distro") non sono entità isolate, ma si evolvono seguendo alberi genealogici precisi. Sebbene esistano migliaia di varianti, la maggior parte deriva da tre "famiglie" storiche, a cui si aggiunge il ramo mobile di Google.
## Le 4 Famiglie Principali
- **Debian Family:** Focalizzata sulla stabilità e sul software libero.
- **Red Hat Family (RHEL):** Orientata al mercato enterprise e ai server aziendali.
- **Arch Family:** Basata sul principio "KISS" (_Keep It Simple, Stupid_) e sul modello Rolling Release.
- **Android:** Basata sul kernel Linux ma con un'architettura e una gestione dei pacchetti (APK) completamente diversa dalle distro desktop/server.

## 2. Gestione dei Pacchetti (Package Management)
Ogni famiglia utilizza strumenti specifici per installare, aggiornare e rimuovere il software. Per l'esame LPI è fondamentale distinguere tra il formato del pacchetto e il comando utilizzato.

|Famiglia|Formato Pacchetto|Package Manager (CLI)|Note|
|---|---|---|---|
|**Debian**|`.deb`|`apt`, `apt-get`|Gestione avanzata delle dipendenze.|
|**Red Hat**|`.rpm`|`dnf` (moderno), `yum`|Red Hat usa RPM come base.|
|**Arch**|`pkg.tar.zst`|`pacman`|Estremamente veloce e leggero.|

## 3. Analisi delle Distribuzioni Common-Use
La frammentazione di Linux è dovuta a diverse **filosofie di utilizzo** (stabilità vs. novità) e licenze software.
## A. Ramo Debian
- **Debian:** Il "sistema operativo universale". Molto conservativo; la versione _Stable_ include solo pacchetti testati per anni. La filosofia è strettamente legata al software libero (Free Software).
- **Ubuntu:** Sviluppata da Canonical, nasce da Debian con l'obiettivo di essere "Linux per esseri umani". Punta sull'usabilità **Out-of-the-Box** (driver pronti, codec multimediali preinstallati).
- **Linux Mint:** Derivata di Ubuntu, è pensata per facilitare la transizione degli utenti da Windows, offrendo un'interfaccia molto familiare e intuitiva.
## B. Ramo Red Hat
- **Fedora:** È il "laboratorio" di Red Hat. Qui vengono testate le nuove tecnologie (come Wayland o Systemd) prima che approdino su RHEL (Red Hat Enterprise Linux).
- **CentOS / Rocky Linux / AlmaLinux:** Versioni "community" o cloni di RHEL, usatissime in ambito server per la loro affidabilità industriale.
## C. Ramo Arch
- **Arch Linux:** Una distribuzione "minimalista" dove l'utente deve configurare tutto manualmente. È una **Rolling Release**: non esistono versioni 11, 12, 13, ma il sistema si aggiorna continuamente all'ultima versione disponibile.
---

> **Nota per lo studio:** Per la certificazione LPI 010-160 o 101-500, ricorda che Debian usa `dpkg` come tool di basso livello e `apt` come tool di alto livello. Analogamente, Red Hat usa `rpm` (basso livello) e `dnf` (alto livello).


---
## Collegamenti
- Torna al corso: [[Dashboard Udemy morroLinux Linux]]
- [[Macchina virtuale VirtualBox]]
- [[VirtualBox Guest Additions]]