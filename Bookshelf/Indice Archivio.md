

## Mostra tutte le note che sono considerate archiviate
```dataview
TABLE file.name AS "Nota", file.ctime AS "Creata",
  filter(file.tags, (t) => t != "TO-DO" and t != "created") AS "Materia"
FROM "Archive"
WHERE contains(file.tags, "#ArchiviO")
SORT file.ctime DESC
```
