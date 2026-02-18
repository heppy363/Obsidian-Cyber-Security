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
## 1. Panoramica: Cos'è il RIP?
Il RIP è un protocollo di tipo **Interior Gateway Protocol (IGP)**, il che significa che è progettato per scambiare informazioni di routing all'interno di un singolo sistema autonomo (AS), come una rete aziendale di piccole dimensioni.
### Caratteristiche principali:
- **Algoritmo:** Utilizza l'[[Algoritmo Bellman-Ford]].
- **Metrica:** L'unica cosa che conta per il RIP è il **Hop Count** (numero di salti). Ogni router attraversato conta come 1 salto.
- **Limite di scalabilità:** Il numero massimo di hop consentiti è **15**. Un network a distanza 16 è considerato irraggiungibile (un "infinito" logico).
- **Aggiornamenti:** Invia l'intera tabella di routing ai vicini a intervalli regolari (solitamente ogni **30 secondi**).

## 2. Dettaglio Funzionamento
Per capire come "ragiona" il RIP, dobbiamo guardare come gestisce le informazioni.

### Il concetto di Distance Vector
Immagina che ogni router dica ai suoi vicini: _"Io so come arrivare alla rete X e mi costa Y salti"_. Il vicino riceve l'info, aggiunge 1 al costo e lo ridice ai suoi vicini. Non esiste una mappa globale della rete (a differenza dell'OSPF); ogni router vede il mondo solo attraverso gli occhi dei suoi vicini immediati.
### Versioni del Protocollo
Esistono tre varianti principali:

|Caratteristica|RIPv1|RIPv2|RIPng|
|---|---|---|---|
|**Tipo**|Classful (non invia subnet mask)|Classless (supporta CIDR/VLSM)|Classless (per IPv6)|
|**Metodo Invio**|Broadcast (`255.255.255.255`)|Multicast (`224.0.0.9`)|Multicast (`FF02::9`)|
|**Autenticazione**|No|Sì (Password/MD5)|Sì (tramite IPsec)|

## 3. Problemi e Soluzioni (Loop di Routing)
Poiché il RIP è "lento" a convergere (ovvero a capire se un link è caduto), rischia di creare loop in cui i pacchetti girano all'infinito. Per evitarlo, usa queste tecniche:
1. **Split Horizon:** Un router non pubblicizza mai una rotta sulla stessa interfaccia da cui l'ha appresa. (Se A dice a B che la rete X è da quella parte, B non deve ridire ad A che sa come arrivare a X).
2. **Route Poisoning:** Quando una rete cade, il router imposta la metrica a **16** (infinito) e la comunica subito, così tutti sanno che è morta.
3. **Hold-down Timers:** Quando una rotta diventa instabile, il router aspetta un certo periodo prima di accettare nuove informazioni su quella stessa rotta, evitando di credere a dati potenzialmente errati.

## 4. I Timer del RIP
Il comportamento del RIP è dettato da quattro orologi principali:
- **Update Timer (30s):** Frequenza degli annunci pubblicitari.
- **Invalid Timer (180s):** Se non ricevo aggiornamenti su una rotta per questo tempo, la considero "scaduta".
- **Hold-down Timer (180s):** Periodo di "silenzio" per evitare loop durante un cambio di topologia.
- **Flush Timer (240s):** Tempo dopo il quale la rotta viene fisicamente rimossa dalla tabella.

## Link 
1) 