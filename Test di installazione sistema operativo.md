---
tipo: nota_lezione
corso: "Dashboard H-NET"
tags: [progetto, hNet, Completed]
creato: 2026-02-22 12:38
---

# 📝 Lezione: Test di installazione sistema operativo
**Corso:** [[Dashboard H-NET]]

---
## Contenuto

#### **1. Preparazione Supporto d'Installazione**
- **Software utilizzato:** Rufus.
- **Problema riscontrato:** Errore `grub_is_cli_need_auth not found` durante il caricamento di GRUB.
- **Causa:** Conflitto tra la modalità di scrittura "ISO" e il firmware UEFI della Supermicro X9, che non riconosceva correttamente i moduli di sicurezza del bootloader.
- **Soluzione:** * Ricreazione della chiavetta USB con **Schema partizione GPT** e **Target UEFI**.
    - Utilizzo della modalità di scrittura **"DD Mode"** (copia bit a bit), che ha garantito la massima compatibilità con il BIOS server.

#### **2. Configurazione BIOS per il Boot**
- **Boot Mode Select:** Impostato su **UEFI** per supportare correttamente le partizioni moderne e l'SSD SanDisk.
- **Secure Boot:** Disabilitato (Disabled) per evitare blocchi durante il caricamento del kernel Linux su hardware datato.
- **Video Option ROM:** Impostata su **Legacy/EFI** per permettere alla GTX 1050 di visualizzare il segnale durante il caricamento del sistema operativo.
#### **3. Installazione e Post-Installazione (Ubuntu)**
- **Target:** SSD SanDisk da 480GB.
- **Stato:** Installazione completata con successo e accesso al desktop di Ubuntu raggiunto.
- **Verifica Hardware da OS:**
    - CPU: Rilevato correttamente lo Xeon E5-2690 V2 (20 thread logici).
    - RAM: Verificati **112 GB** tramite il comando `free -m`.
    - GPU: Rilevata la NVIDIA GTX 1050 tramite bus PCIe.

#### **4. Diagnostica e Stress Test (Software Suite)**
Abbiamo predisposto una serie di strumenti per validare la stabilità del sistema operativo sotto carico:
- **`stress-ng`**: Installato per testare la stabilità del kernel nella gestione della memoria massiccia (112 GB) e del multithreading della CPU.
- **`s-tui`**: Configurato per il monitoraggio grafico delle frequenze di clock e delle temperature (fondamentale per evitare il _thermal throttling_).
- **`lm-sensors`**: Configurato e calibrato tramite `sensors-detect` per leggere correttamente i sensori della scheda madre Supermicro.
	- stabili e non superano mai i 60 gradi al massimo delle prestazioni 
#### **5. Ottimizzazioni di Sistema Applicate**
- **GRUB Tuning:** Aggiunta del parametro `pcie_aspm=off` per prevenire il blocco (state DOWN) delle schede di rete Intel integrate dovuto al risparmio energetico aggressivo di Linux su bus PCIe server.
- **Sostituzione Driver Rete:** Identificata l'interfaccia `eno1` come controller primario e forzato lo stato su **UP** via software.

## Collegamenti
- Torna al corso: [[Dashboard H-NET]]