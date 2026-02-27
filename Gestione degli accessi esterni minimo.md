---
tipo: nota_lezione
corso: "Dashboard H-NET"
tags: [progetto, hNet, Completed]
creato: 2026-02-27 21:46
---

# 📝 Lezione: Gestione degli accessi esterni minimo
**Corso:** [[Dashboard H-NET]]

---
## Contenuto

### 1. Il percorso del traffico
Il traffico che arriva dall'esterno deve attraversare due "dogane":
1. **Router ISP:** Riceve la richiesta (es. sulla porta 80 o 443).
2. **pfSense (Lenovo M720q):** Riceve la richiesta dal router ISP.
3. **Reverse Proxy:** Riceve la richiesta da pfSense e la smista al servizio corretto nel tuo Homelab.

### 2. Configurazione dei Port Forwarding (Il "ponte")
Per far arrivare il traffico dall'esterno al tuo Homelab, devi creare due regole di inoltro:
- **Sul Router ISP:** Devi aprire le porte **80** (HTTP) e **443** (HTTPS) e indirizzarle verso l'indirizzo IP della **WAN del tuo Lenovo** (quell'indirizzo tipo `192.168.1.50` di cui parlavamo prima).
- **Su pfSense:** Devi creare una regola di NAT (Firewall -> NAT -> Port Forward) che prenda il traffico in arrivo sulla WAN (sempre porte 80 e 443) e lo invii all'IP interno del tuo **Reverse Proxy** (es. `10.0.0.5`).

### 3. Dove far girare il Reverse Proxy?
Hai tre opzioni principali nel tuo Homelab:
1. **Pacchetto pfSense (HAProxy):** Puoi installare HAProxy direttamente sul tuo Lenovo M720q. È molto potente ma la configurazione è un po' tecnica.
2. **Container Docker (Nginx Proxy Manager):** Questa è la scelta che ti consiglio. È semplicissimo da usare, ha un'interfaccia grafica fantastica e gestisce i certificati SSL (Let's Encrypt) con un click.
3. **Traefik:** Ottimo se prevedi di usare molti container Docker, ma ha una curva di apprendimento più alta.

### 4. Il problema dell'IP Pubblico (Dynamic DNS)
Molti router ISP non hanno un IP pubblico statico (cambia ogni volta che riavvii il modem).
- **Soluzione:** Usa un servizio di **DDNS** (come DuckDNS, No-IP o Cloudflare). Puoi configurare pfSense stesso affinché aggiorni automaticamente il tuo indirizzo IP ogni volta che cambia. In questo modo potrai accedere ai tuoi servizi usando un nome (es. `miohomelab.duckdns.org`) invece di un numero.

### 5. Perché è meglio del semplice Port Forwarding?
Usando un Reverse Proxy nel tuo Lab:
- **Un solo punto di ingresso:** Apri solo la porta 443 invece di aprirne una per ogni servizio.
- **Sicurezza SSL:** Il proxy gestisce i certificati, così tutti i tuoi servizi saranno in `HTTPS` (con il lucchetto verde).
- **Nomi mnemonici:** Potrai raggiungere i servizi con nomi chiari (es. `obsidian.lab.local`, `pfsense.lab.local`, `server1.lab.local`).

---
## Collegamenti
- Torna al corso: [[Dashboard H-NET]]