---
date: 2026-03-12T12:00
tags:
  - dashboard
  - linking
cssclasses:
  - page-wide
---
# Linking Dashboard

## Am besten vernetzte Notes

```dataview
TABLE length(file.inlinks) AS "Eingehend", length(file.outlinks) AS "Ausgehend", (length(file.inlinks) + length(file.outlinks)) AS "Gesamt"
WHERE !contains(file.folder, "99 - Meta/Patterns") AND !contains(file.folder, "Fabric") AND !contains(file.folder, ".obsidian")
SORT (length(file.inlinks) + length(file.outlinks)) DESC
LIMIT 20
```

## Verwaiste Notes in Projekten & Areas (Linking-Kandidaten)

```dataview
TABLE file.folder AS "Ordner", file.mtime AS "Zuletzt bearbeitet"
WHERE length(file.inlinks) = 0 AND length(file.outlinks) = 0
  AND (contains(file.folder, "01 - Projects") OR contains(file.folder, "02 - Areas") OR contains(file.folder, "03 - Resources") OR contains(file.folder, "04 - Permanent"))
SORT file.folder ASC
```

## Notes mit vielen ausgehenden Links aber wenig eingehenden

```dataview
TABLE length(file.outlinks) AS "Ausgehend", length(file.inlinks) AS "Eingehend"
WHERE length(file.outlinks) > 3 AND length(file.inlinks) = 0
  AND !contains(file.folder, "99 - Meta/Patterns")
SORT length(file.outlinks) DESC
LIMIT 15
```

## Backlinks pro Bereich

```dataview
TABLE length(rows) AS "Notes", sum(map(rows, (r) => length(r.file.inlinks))) AS "Eingehende Links gesamt"
FROM "01 - Projects" OR "02 - Areas" OR "03 - Resources" OR "04 - Permanent"
GROUP BY file.folder AS Ordner
SORT sum(map(rows, (r) => length(r.file.inlinks))) DESC
LIMIT 20
```
