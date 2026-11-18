---
date: 2026-03-12T12:00
tags:
  - dashboard
  - overview
cssclasses:
  - page-wide
---
# Vault Overview Dashboard

## Notes nach Bereich

```dataview
TABLE length(rows) AS "Anzahl Notes"
FROM ""
WHERE file.name != "CLAUDE"
GROUP BY regexreplace(file.folder, "/.*", "") AS Bereich
SORT Bereich ASC
```

## Zuletzt bearbeitete Notes (letzte 7 Tage)

```dataview
TABLE file.mtime AS "Zuletzt bearbeitet", file.folder AS "Ordner"
WHERE file.mtime >= date(today) - dur(7 days) AND !contains(file.folder, "99 - Meta/Patterns") AND !contains(file.folder, ".obsidian")
SORT file.mtime DESC
LIMIT 25
```

## Verwaiste Notes (keine eingehenden Links)

```dataview
TABLE file.folder AS "Ordner", file.mtime AS "Zuletzt bearbeitet"
WHERE length(file.inlinks) = 0
  AND !contains(file.folder, "06 - Periodic")
  AND !contains(file.folder, "99 - Meta/Patterns")
  AND !contains(file.folder, "99 - Meta/Templates")
  AND !contains(file.folder, ".obsidian")
  AND !contains(file.folder, "Excalidraw")
  AND !contains(file.folder, "Fabric")
  AND !contains(file.folder, "copilot")
  AND file.name != "CLAUDE"
SORT file.folder ASC
```

## Notes mit den meisten Links (Hubs)

```dataview
TABLE length(file.outlinks) AS "Ausgehende Links", length(file.inlinks) AS "Eingehende Links", file.folder AS "Ordner"
WHERE length(file.outlinks) + length(file.inlinks) > 3
  AND !contains(file.folder, "99 - Meta/Patterns")
SORT length(file.outlinks) + length(file.inlinks) DESC
LIMIT 20
```

## Permanent Notes Wachstum

```dataview
TABLE file.cday AS "Erstellt", file.mtime AS "Zuletzt bearbeitet"
FROM "04 - Permanent"
SORT file.cday DESC
```

## Tags Uebersicht

```dataview
TABLE length(rows) AS "Anzahl"
FROM ""
WHERE file.tags
FLATTEN file.tags AS tag
GROUP BY tag
SORT length(rows) DESC
LIMIT 30
```
