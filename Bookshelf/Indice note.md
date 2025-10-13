## Note precedenti

```dataview
TABLE file.name AS "Note", file.ctime AS "Created", 
  filter(file.tags, (t) => t != "TO-DO" and t != "created") AS "Materia"
FROM "Lesson"
WHERE file.ctime >= date(today) - dur(1 day) AND file.ctime < date(today)
SORT file.ctime DESC
```

## Note da elaborare
 
```dataview
TABLE file.name AS "Note", file.ctime AS "Created", 
  filter(file.tags, (t) => t != "TO-DO") AS "Tags"
FROM "Lesson"
WHERE contains(file.tags, "TO-DO")
SORT file.ctime DESC
```

