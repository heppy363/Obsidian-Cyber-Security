`Mostra tutte le lezioni che sono da elaborare quindi da ridurre a note atomiche`[[worckflow.canvas]]

## Mostra tutte le note che devono essere elaborate 
```dataview
TABLE file.name AS "Nota", file.ctime AS "Creata",
  filter(file.tags, (t) => t != "TO-DO" and t != "created") AS "Materia"
FROM "Lesson"
WHERE contains(file.tags, "#TO-DO")
SORT file.ctime DESC
```
