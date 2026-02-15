> Rappresenta tutte le note per studiare e capire docker come tecnologia e come teoria

```dataview
TABLE file.name AS "Note", file.ctime AS "Created", 
  (filter(file.tags, (t) => t != "TO-DO")) AS "Tags"
FROM "Processed"
WHERE contains(file.tags, "Completed") AND contains(file.tags, "Docker")
SORT file.ctime DESC
```