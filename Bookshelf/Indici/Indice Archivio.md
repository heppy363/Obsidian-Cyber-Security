`Si tratta di tutte le note delle lezzioni unniversitarie e non che devono essere rielaborate in note atomiche come da`[[worckflow.canvas]]

## Mostra tutte le note che sono considerate archiviate
```dataview
TABLE file.name AS "Nota", file.ctime AS "Creata",
  filter(file.tags, (t) => t != "TO-DO" and t != "created") AS "Materia"
FROM "Archive"
WHERE contains(file.tags, "#ArchiviO")
SORT file.ctime DESC
```
