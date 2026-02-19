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


[[Piano di studi <% nomeCorso %>]]
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
