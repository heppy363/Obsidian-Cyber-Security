---
aliases:
  - Lesson
tags:
  - TO-DO
Docente:
Modulo: "1"
---
--- 
## Nozioni





## Riferimenti link
- [[Indice note]]


<%*
const counterPath = tp.file.find_tfile("counter.md");
let counter = await app.vault.read(counterPath);
counter = parseInt(counter.trim()) + 1;
await app.vault.modify(counterPath, counter.toString());

const date = tp.date.now("DD-MM-YYYY");
const newName = `${date}-${counter}`;
await tp.file.rename(newName);
%>
