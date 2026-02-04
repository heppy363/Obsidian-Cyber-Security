`Tutte le note della mia rete domestica privata mini data center e Hom lab`

```dataview
TABLE file.name AS "Note", file.ctime AS "Created", 
  (filter(file.tags, (t) => t != "TO-DO")) AS "Tags"
FROM "Processed"
WHERE contains(file.tags, "Completed") AND contains(file.tags, "H-net")
SORT file.ctime DESC
```
 