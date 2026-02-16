>indica tutto quello che categorizzo, come IA progetti idee studi 

```dataview
TABLE file.name AS "Note", file.ctime AS "Created", 
  (filter(file.tags, (t) => t != "TO-DO")) AS "Tags"
FROM "Processed"
WHERE contains(file.tags, "Completed") AND contains(file.tags, "IA")
SORT file.ctime DESC
```