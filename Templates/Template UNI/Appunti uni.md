<%*
// 1. Recupera l'API di Dataview
const dv = app.plugins.plugins.dataview?.api;

if (!dv) {
    new Notice("Errore: Il plugin Dataview non è attivo.");
    return;
}

// 2. Cerca i corsi
const corsi = dv.pages().where(p => p.tipo == "corso");
const nomiCorsi = corsi.file.name.array();

if (nomiCorsi.length === 0) {
    new Notice("Nessun corso trovato!");
    return;
}

// 3. Selezione Corso e Titolo Nota
const corsoScelto = await tp.system.suggester(nomiCorsi, nomiCorsi);
if (!corsoScelto) return;

let titoloNota = await tp.system.prompt("Titolo della nota/lezione");
if (!titoloNota) titoloNota = "Senza Titolo";

// 4. RECUPERO TAG DAL CORSO
// Cerchiamo la pagina del corso scelto per leggerne i tag
const datiCorso = corsi.where(p => p.file.name === corsoScelto).first();
let tagEreditati = [];

if (datiCorso && datiCorso.file.tags) {
    // Filtriamo i tag per evitare di portarci dietro il tag "corso" 
    // e teniamo quelli specifici (come #programmazioneUNI)
    tagEreditati = datiCorso.file.tags.array().filter(t => t !== "#corso");
}

// Uniamo i tag ereditati con "appunti"
// Usiamo un Set per evitare duplicati
let setTags = new Set([...tagEreditati, "appunti", "Completed"]);
let tagsFinali = Array.from(setTags).map(t => t.replace("#", "")); // Rimuoviamo il cancelletto per il frontmatter

await tp.file.rename(titoloNota);
%>---
tipo: nota_lezione
corso: "<% corsoScelto %>"
tags: [<% tagsFinali.join(", ") %>]
creato: <% tp.date.now("YYYY-MM-DD HH:mm") %>
---

# 📝 Lezione: <% titoloNota %>
**Corso:** [[<% corsoScelto %>]]

---
## Contenuto


---
## Collegamenti
- Torna al corso: [[<% corsoScelto %>]]