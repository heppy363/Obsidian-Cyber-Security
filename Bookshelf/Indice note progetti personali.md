> Rappresenta tutte le note dei miei progetti personali
```dataview
TABLE file.name AS "Note", file.ctime AS "Created", 
  (filter(file.tags, (t) => t != "TO-DO")) AS "Tags"
FROM "Processed"
WHERE contains(file.tags, "Completed") AND contains(file.tags, "progettiPersonali")
SORT file.ctime DESC
```