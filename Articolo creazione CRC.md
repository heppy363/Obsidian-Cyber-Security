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
## 1. Traduzione in Italiano

"Il controllo di ridondanza ciclico (CRC) è una tecnica di rilevamento degli errori utilizzata per trovare errori nei dati. È comunemente usato per determinare se i dati durante una trasmissione, o i dati presenti nelle memorie dati e programmi, siano stati corrotti o meno. Un CRC prende un flusso di dati o un blocco di dati come input e genera un output a 16 o 32 bit che può essere aggiunto ai dati e utilizzato come checksum.

Quando i dati vengono ricevuti, il dispositivo o l'applicazione ripete il calcolo: se il nuovo risultato del CRC non corrisponde a quello calcolato in precedenza, il blocco contiene un errore nei dati. L'applicazione rileverà l'errore e potrà intraprendere un'azione correttiva, come richiedere che i dati vengano inviati di nuovo o semplicemente non utilizzare i dati errati.

Il motore CRC nel DMAC (Direct Memory Access Controller) supporta due polinomi CRC comunemente usati: CRC-16 (CRC-CCITT) e CRC-32 (IEEE 802.3). Tipicamente, applicare il CRC-n (CRC-16 o CRC-32) a un blocco di dati di lunghezza arbitraria rileverà qualsiasi singola alterazione che sia ≤n bit di lunghezza, e rileverà la frazione 1−2−n di tutti i "burst" (scariche) di errore più lunghi.

- **CRC-16:** Polinomio: x16+x12+x5+1 (Valore esadecimale: `0x1021`)
    
- **CRC-32:** Polinomio: x32+x26+x23+x22+x16+x12+x11+x10+x8+x7+x5+x4+x2+x+1 (Valore esadecimale: `0x04C11DB7`)
    

La sorgente dei dati per il motore CRC può essere uno dei canali DMA o l'interfaccia bus APB, e deve essere selezionata scrivendo nei bit 'CRC Input Source' nel registro di controllo CRC (CRCCTRL.CRCSRC). Il motore CRC preleva quindi l'input dalla sorgente selezionata e genera un checksum basato su questi dati. Il checksum è disponibile nel registro 'CRC Checksum' (CRCCHKSUM). Quando si usa il polinomio CRC-32, il checksum finale letto viene invertito nei bit e complementato.

Il polinomio CRC viene selezionato scrivendo nel bit 'CRC Polynomial Type' nel registro di controllo CRC (CRCCTRL.CRCPOLY); il valore predefinito è CRC-16. Il motore CRC opera solo su byte. Quando il DMA è usato come sorgente dati, verrà utilizzata l'impostazione della dimensione del battito (beat size) del canale DMA. Quando usato con l'interfaccia bus APB, l'applicazione deve selezionare il campo bit 'CRC Beat Size'. Sono supportati tipi di accesso al bus a 8, 16 o 32 bit. Il numero corrispondente di byte verrà scritto nel registro CRCDATAIN e il motore CRC opererà sui dati in ingresso byte dopo byte."



## Link 
1) [qui](https://onlinedocs.microchip.com/oxy/GUID-24121E3C-B8D3-4957-90D7-3EE3914A3F39-en-US-4/GUID-8D03F7AB-3A13-49FA-99ED-366B618AD6CB.html)