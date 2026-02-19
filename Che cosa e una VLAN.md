---
tipo: nota_lezione
corso: "Dashboard H-NET"
tags: [progetto, hNet, Completed]
creato: 2026-02-19 22:31
---

# 📝 Lezione: Che cosa e una VLAN
**Corso:** [[Dashboard H-NET]]

---
## Contenuto
Una  Vlan sa si puo intendere come una rete dentro la rete, di fatto noi abbimamo un switch che funge da grande magaziono qui i paccheti tramite il riconoscimento del indirizzo MAC della maccina destinataria vengono instradati tutto questo avviene al livello 2 livello Data Link se lo switch lo permette in questo caso si possono creare delle reti virtuali separate, che non comunicano tra di loro anche se fisicamente gli apparati sono gli stessi, questo e importante dato che a volte e necessario che le macchine siano isolate, da considerare che lo switch lo deve permettere dato che di base questo lo fa ma non vale per tutti spece gli economici.
Da qui la grande differenza tra switch e hab questo ultimo parla in maneira brodcast gli arriva in messagio e chiede a tutte le macchine della rete il pacchetto e destinato a loro o meno uno switch questo non lo fa dato che lavora al livelo 2 del modello ISO OSI controlla il Fraim MAC e tramite la sua tabella interna MAC o CAM  cerca la macchina indirizzata e poi glielo manda.
**Le sotto reti** virtuali saranno composte da un GW virtuale ovvero un dirizzo che vera configurato su PFsens ad esempio rete 1 GW virtuale 10.0.0.1 da li a casta si nomineranno tutti gli altri, cosi via per tutte le altre reti e quindi con PFsens che conosce tutte le reti puo instradare il traffico alle specifiche con tutto quello che riguarda il concetto di sicurezza quandi quale rete puo fare quale cosa. La magia avviene con il cavo detto **Trunk** ovverro quello che fisicamente arriva dal mio router PFsens fino al mio switch da li avviene il tagging ovvero l'identificazione e categorizzazione delle varie VLAN con il relativo instradamento. 
Ad esempio, potrai dire a pfSense: _"La rete 10.0.0.x (Guest) può andare su internet ma non può assolutamente toccare il Gateway della rete 10.0.1.x (Database)"_.

---
## Collegamenti
- Torna al corso: [[Dashboard H-NET]]