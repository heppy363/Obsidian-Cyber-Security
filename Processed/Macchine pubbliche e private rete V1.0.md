---
aliases:
  - Completate
tags:
  - Completed
  - H-net
---
--- 
## Nozioni
### 1. La Logica di Accesso "Solo VPN"
Per garantire che il tuo ambiente di sviluppo (VLAN 30) sia invisibile all'esterno, useremo una combinazione di pfSense e il Reverse Proxy:
- **Traffico Pubblico (Sito/Blog):** Internet → pfSense → Reverse Proxy (VLAN 20) → Mini PC 1. (Sempre aperto).
- **Traffico Privato (Gitea/Sviluppo):** Internet → **Bloccato di base**.
- **Traffico via VPN:** Utente VPN → pfSense (Tunnel sicuro) → Accesso diretto a VLAN 30 (Mini PC 2) o tramite il Reverse Proxy ma con restrizione IP.
### 2. Il Reverse Proxy come "Filtro d'Ingresso"
Puoi usare il Reverse Proxy sul Mini PC 1 anche per i servizi privati, ma con una marcia in più:
1. **Sottodomini separati:** Crei `blog.tuodominio.it` (Pubblico) e `git.tuodominio.it` (Privato).
2. **Access Control List (ACL):** Sul Reverse Proxy configuri una regola che dice: _"Se la richiesta arriva per `git.tuodominio.it`, falla passare SOLO se l'indirizzo IP di chi chiama appartiene alla tua rete interna o alla VPN"_.
3. **Vantaggio:** Continui ad avere certificati SSL validi (HTTPS) e nomi facili da ricordare, senza però esporre il codice di Gitea a tutto il mondo.
### 3. Configurazione sullo Switch Netgear GS116E
Grazie alle caratteristiche del tuo switch, possiamo isolare fisicamente queste comunicazioni:
- **Isolamento delle Porte:** Configureremo le porte del Mini PC 2 (VLAN 30) in modo che non possano mai rispondere a pacchetti provenienti direttamente dalla porta del router dedicata a Internet, ma solo a quelli provenienti dalla porta del router dedicata alla VPN o dalla tua porta Admin (VLAN 10).
- **Affidabilità:** Poiché Gitea e i servizi di sviluppo sono critici per il tuo lavoro, l'MTBF di oltre **2 milioni di ore** del GS116E ti assicura che il "ponte" tra il tuo PC e il server di sviluppo non crolli mai per problemi hardware.
- **Gestione:** Se per errore di configurazione ti "chiudi fuori" dalla VLAN di sviluppo, potrai usare la **ProSAFE Plus Utility** per resettare la configurazione della porta specifica senza perdere l'accesso a tutto il resto.

### 4. Schema delle Regole di pfSense per la "Rete di Sviluppo"

Per far sì che i "Re" (tu) possano lavorare e le macchine "Sviluppo" siano protette:

|Sorgente|Destinazione|Porta|Azione|Motivo|
|---|---|---|---|---|
|**VLAN 10 (PC/VPN)**|**VLAN 30 (Gitea)**|Qualsiasi|**PERMIT**|Sei il "Re", gestisci lo sviluppo.|
|**Internet (Any)**|**VLAN 30 (Gitea)**|Qualsiasi|**DENY**|Protezione totale dall'esterno.|
|**VLAN 30 (Gitea)**|**VLAN 40 (NAS)**|Porta DB/S3|**PERMIT**|Permette a Gitea di salvare i dati.|
|**VLAN 30 (Gitea)**|**VLAN 10 (PC)**|Qualsiasi|**DENY**|Se Gitea viene compromesso, non può attaccare il tuo PC.|
La VLAN 30 è la mia **Secure Dev Zone**. L'accesso è blindato: solo io (VLAN 10) e chi è autenticato in VPN può 'vedere' Gitea e gli altri servizi privati. Il Reverse Proxy nella DMZ (VLAN 20) funge da portineria, ma pfSense e lo switch Netgear assicurano che nessuno possa scavalcare il muro senza le giuste credenziali."

## Link 
1) 