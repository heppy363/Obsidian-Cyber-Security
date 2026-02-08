---
aliases:
  - Completate
tags:
  - Completed
  - H-net
  - VLAN
---
--- 
`Si tratta della configurazione delle mie VLAN a livello base con solo 5 macchine`
## Nozioni
| **VLAN ID** | **Nome**             | **Dispositivi**                  | **Logica di Accesso**                                                                         |
| ----------- | -------------------- | -------------------------------- | --------------------------------------------------------------------------------------------- |
| **10**      | **Admin (Kings)**    | PC Fisso, Portatile, VPN         | **I Re:** Possono accedere a tutto (VLAN 20, 30, 40).                                         |
| **20**      | **DMZ (Public)**     | Mini PC 1 (Sito Web, Blog)       | **Isolata:** Può solo rispondere a chi arriva da internet e chiedere dati specifici al NAS.   |
| **30**      | **Private Services** | Mini PC 2 (Gitea, Musica, Video) | **Interna:** Accessibile solo da te (VLAN 10) e legge dati dal NAS.                           |
| **40**      | **Storage (Vault)**  | NAS (S3 Bucket, DB, Media)       | **Protetta:** Non parla con nessuno di sua iniziativa; risponde solo a richieste autorizzate. |

### 2. Come cambia la gestione dei flussi (Firewall)
Il ruolo di pfSense diventa fondamentale per gestire queste nuove interazioni:
- **Il Mini PC 1 (Sito/Blog):** È il più pericoloso perché è esposto online. Se qualcuno lo "buca", grazie alla VLAN 20, rimarrà bloccato lì. Non potrà accedere al tuo PC fisso o al tuo server Gitea. Potrà solo leggere il database/bucket sul NAS tramite una porta specifica aperta su pfSense.
- **Il Mini PC 2 (Multimedia/Gitea):** Questo mini PC ha bisogno di molta banda verso il NAS per i video. Grazie alla **capacità di switching di 32 Gbps** del GS116E, lo streaming 4K o il caricamento di repository pesanti su Gitea non rallenteranno la navigazione del tuo PC fisso.
- **Storage S3/NAS:** Poiché userai un bucket S3 (probabilmente tramite MinIO o software simile sul NAS), dovrai configurare lo switch per supportare il traffico pesante. Il **design fanless** del tuo switch è perfetto qui, perché i trasferimenti massivi di dati verso il NAS non genereranno rumore di ventole nel tuo lab.
### 3. Configurazione Pratica sul Netgear GS116E
Nelle specifiche del tuo switch, abbiamo visto che puoi gestire tutto via Web. Ecco come assegneremo le porte fisiche:
- **Porte 1-2:** PC Fisso e Portatile (**VLAN 10**).
- **Porta 3:** Mini PC 1 - Web/Blog (**VLAN 20**).
- **Porta 4:** Mini PC 2 - Services (**VLAN 30**).
- **Porte 5-6:** NAS (**VLAN 40**). _Nota: se il NAS ha due porte, potresti usare il **Link Aggregation** per andare a 2 Gbps._
- **Porta 16:** Uplink verso pfSense (**Trunk - Tagged 10, 20, 30, 40**).

### 4. Il tocco "Pro": IGMP Snooping
Visto che hai un **server multimediale** (Mini PC 2), assicurati di attivare l'**IGMP Snooping** nelle impostazioni del Netgear. Questo eviterà che, mentre guardi un film in streaming su un dispositivo, il traffico video venga inviato inutilmente anche al Mini PC che gestisce il tuo blog, ottimizzando le risorse del "magazzino" (lo switch).


- [[Gestione porte VLAN 1.0]]
- [[Macchine pubbliche e private rete V1.0]]

## Link 
1) 