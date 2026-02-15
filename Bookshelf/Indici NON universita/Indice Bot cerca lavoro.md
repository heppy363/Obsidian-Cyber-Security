`Indice di tutte le note per la realizzazione di un agente indipendente per la ricerca del lavoro`

```dataview
TABLE file.name AS "Note", file.ctime AS "Created", 
  (filter(file.tags, (t) => t != "TO-DO")) AS "Tags"
FROM "Processed"
WHERE contains(file.tags, "Completed") AND contains(file.tags, "cercatoreLavoro")
SORT file.ctime DESC
```