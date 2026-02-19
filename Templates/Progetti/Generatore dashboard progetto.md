<%*
// 1. Chiede il nome del corso
let nomeProgetto = await tp.system.prompt("Nome del progetto");
// 2. Chiede i tag
let tagsProgetto = await tp.system.prompt("Inserisci tag extra (separati da virgola)");
// 3. Rinomina il file col nome del corso
await tp.file.rename(nomeProgetto);
%>---
tipo: progetto
corso: <% nomeProgetto %>
tags: [progetto, <% tagsProgetto %>]
stato: in_corso
---

# 📚 Corso: <% nomeProgetto %>

## 🗺️ Roadmap di Avanzamento
> [!info] Progresso
> `$= const p = dv.current().file.tasks.filter(t => t.fullyCompleted).length; const t = dv.current().file.tasks.length; const ratio = t > 0 ? Math.round((p/t)*100) : 0; "<progress value='" + ratio + "' max='100'></progress> " + ratio + "%"`

- [ ] **Fase 1**: 
- [ ] **Fase 2**: 
- [ ] **Fase 3**: 

## Argomenti 
> Mettere tutti gli argomenti del progetto  

---

## 📝 Note del Corso (dalla cartella Processed)
```dataview
LIST
FROM "Processed"
WHERE corso = "<% nomeProgetto %>" AND tipo != "progetto"
SORT file.ctime DESC
```
