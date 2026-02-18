<%*
// 1. Chiede il nome del corso
let nomeCorso = await tp.system.prompt("Nome del Corso");
// 2. Chiede i tag
let tagsCorso = await tp.system.prompt("Inserisci tag extra (separati da virgola)");
// 3. Rinomina il file col nome del corso
await tp.file.rename(nomeCorso);
%>---
tipo: corso
corso: <% nomeCorso %>
tags: [corso, <% tagsCorso %>]
stato: in_corso
---

# 📚 Corso: <% nomeCorso %>

## 🗺️ Roadmap di Avanzamento
> [!info] Progresso
> `$= const p = dv.current().file.tasks.filter(t => t.fullyCompleted).length; const t = dv.current().file.tasks.length; const ratio = t > 0 ? Math.round((p/t)*100) : 0; "<progress value='" + ratio + "' max='100'></progress> " + ratio + "%"`

- [ ] **Fase 1**: Introduzione
- [ ] **Fase 2**: Concetti Base
- [ ] **Fase 3**: Pratica

## Argomenti 
> Mettere tutti gli argomenti del corso 

---

## 📝 Note del Corso (dalla cartella Processed)
```dataview
LIST
FROM "Processed"
WHERE corso = "<% nomeCorso %>" AND tipo != "corso"
SORT file.ctime DESC
```
