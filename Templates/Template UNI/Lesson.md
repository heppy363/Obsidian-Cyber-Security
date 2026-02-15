<%*
// 1. GESTIONE CONTATORE E NOME FILE
const counterPath = tp.file.find_tfile("counter.md");
if (!counterPath) {
    new Notice("Errore: file counter.md non trovato!");
    return;
}
let counter = await app.vault.read(counterPath);
counter = parseInt(counter.trim()) + 1;
await app.vault.modify(counterPath, counter.toString());

const date = tp.date.now("DD-MM-YYYY");
const newName = `${date}-${counter}`;
await tp.file.rename(newName);

// 2. RECUPERO API DATAVIEW E SCELTA CORSO
const dv = app.plugins.plugins.dataview?.api;
if (!dv) {
    new Notice("Errore: Dataview non attivo.");
    return;
}

const corsi = dv.pages().where(p => p.tipo == "corso");
const nomiCorsi = corsi.file.name.array();

if (nomiCorsi.length === 0) {
    new Notice("Nessun corso trovato!");
    return;
}

const corsoScelto = await tp.system.suggester(nomiCorsi, nomiCorsi);
if (!corsoScelto) return;

// 3. TAG PREDEFINITI
// Aggiungiamo TO-DO, uni e il nome del corso (senza spazi)
const tagCorso = corsoScelto.replace(/\s+/g, '');
const tagsFinali = ["TO-DO", "uni", tagCorso];

%>---
tipo: nota_lezione
corso: "<% corsoScelto %>"
tags: [<% tagsFinali.join(", ") %>]
id_lezione: <% counter %>
creato: <% tp.date.now("YYYY-MM-DD HH:mm") %>
---

# 📖 Lezione: <% newName %>
**Corso principale:** [[<% corsoScelto %>]]

---
## 📝 Note di studio


---
## 🔗 Collegamenti
- [[<% corsoScelto %>|Torna all'indice del corso]]