---
aliases:
  - Completate
tags:
  - Completed
  - CompTIAnetwork
  - Certificati
---
--- 
## Nozioni
A livello universitario, è fondamentale distinguere i dispositivi che operano puramente al **Livello 1** (Physical Layer) da quelli che iniziano a guardare i dati (Livello 2 o 3).
I dispositivi del Livello 1 non comprendono indirizzi MAC, non leggono pacchetti e non prendono decisioni logiche: il loro compito è solo **gestire, rigenerare o instradare segnali elettrici, ottici o radio**.
 apparati del Livello Fisico:
### Tabella degli Apparati di Livello 1 (Physical Layer)

|Apparato|Funzione Principale|Caratteristiche Tecniche|Perché usarlo|
|---|---|---|---|
|**Ripetitore (Repeater)**|Rigenerazione del segnale|Riceve un segnale degradato (attenuato), lo ripulisce dal rumore e lo ritrasmette con la potenza originale.|Per superare i limiti fisici di distanza (es. oltre i 100m del rame).|
|**Hub (Ethernet)**|Concentratore di segnale|Funge da ripetitore multi-porta. Invia ogni segnale ricevuto in ingresso su **tutte** le altre porte (_Broadcasting fisico_).|Quasi obsoleto (sostituito dallo Switch). Crea un unico **dominio di collisione**.|
|**Ricetrasmettitore (Transceiver / SFP)**|Conversione di mezzo|Converte segnali elettrici in ottici e viceversa. Esempi comuni sono i moduli SFP/SFP+ inseriti negli switch.|Per collegare un apparato con uscita in rame a una dorsale in fibra ottica.|
|**Modem (Modulatore/Demodulatore)**|Modulazione del segnale|Converte dati digitali in segnali analogici (modulazione) e viceversa (demodulazione) per viaggiare su mezzi non digitali.|Per trasmettere dati su linee telefoniche (DSL) o cavi coassiali (DOCSIS).|
|**Access Point (Solo parte radio)**|Bridge fisico/radio|Converte i segnali elettrici del cavo Ethernet in onde elettromagnetiche (RF).|Per permettere la connettività Wi-Fi a dispositivi mobili.|
|**Cavi e Connettori**|Mezzo trasmissivo|Sono considerati parte integrante del Livello 1 (passivi).|Rappresentano l'infrastruttura fisica vera e propria.|

### Analisi Specifica per lo Studente Universitario
#### 1. La differenza tra Hub e Switch (Punto critico d'esame)
Questa è la domanda classica.
- L'**Hub** lavora al **Livello 1**: non "legge" il frame Ethernet, vede solo bit. Se il computer A invia un dato al computer B, l'Hub lo manda a tutti (B, C, D). Questo genera collisioni e spreco di banda.
- Lo **Switch** lavora al **Livello 2**: legge l'indirizzo MAC di destinazione e invia il dato solo sulla porta corretta. Lo Switch "interrompe" i domini di collisione, l'Hub no.

#### 2. Il concetto di "Dominio di Collisione"
Al Livello 1, se due dispositivi trasmettono contemporaneamente sullo stesso segmento fisico (o tramite un Hub), i segnali si sovrappongono e si distruggono. Questa area fisica è chiamata **Dominio di Collisione**. Gli apparati di Livello 1 (come i ripetitori e gli hub) **estendono** il dominio di collisione, non lo dividono.

#### 3. I Transceiver (SFP/QSFP)
Nelle reti moderne, lo "standard" fisico è modulare. Gli switch hanno degli slot vuoti dove inserisci il Transceiver. Questo è l'esempio perfetto di Livello 1: il modulo non sa cosa sta passando (TCP, UDP, HTTP), si occupa solo di trasformare i bit elettrici che arrivano dalla scheda madre in impulsi laser per la fibra.

#### 4. Amplificatori vs Ripetitori
- Un **amplificatore** (analogico) aumenta tutto, incluso il rumore di fondo.
- Un **ripetitore** (digitale) interpreta i bit, ricostruisce il segnale "pulito" e lo emette come nuovo. Il Livello 1 moderno usa quasi esclusivamente la rigenerazione digitale.

## Link 
1) 