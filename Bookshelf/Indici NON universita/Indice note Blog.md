> Rappresentano le note dei mio blog personale basto sulla sicurezza Informatica

```dataview
TABLE file.name AS "Note", file.ctime AS "Created", 
  (filter(file.tags, (t) => t != "TO-DO")) AS "Tags"
FROM "Processed"
WHERE contains(file.tags, "Completed") AND contains(file.tags, "blog")
SORT file.ctime DESC
```