---
date: 2026-03-12T12:00
tags:
  - dashboard
  - tasks
cssclasses:
  - page-wide
---
# Task Dashboard

## Alle offenen Tasks (vault-weit)

```dataviewjs
const exclude = ["99 - Meta/Templates", "99 - Meta/Patterns", "Fabric", "copilot-custom-prompts"];
const pages = dv.pages()
  .where(p => !exclude.some(e => p.file.folder.startsWith(e)))
  .where(p => p.file.tasks.some(t => !t.completed))
  .sort(p => p.file.mtime, 'desc');

for (const page of pages) {
  const open = page.file.tasks.where(t => !t.completed && t.text.trim() !== "");
  if (open.length === 0) continue;

  const container = this.container.createEl("details");
  const summary = container.createEl("summary");
  const link = summary.createEl("a", {
    text: page.file.name,
    cls: "internal-link",
    attr: { "data-href": page.file.name, href: page.file.name }
  });
  link.style.fontWeight = "bold";
  summary.appendText(` (${open.length} offen)`);

  const list = container.createEl("ul");
  for (const t of open) {
    const li = list.createEl("li");
    li.createEl("input", { attr: { type: "checkbox", disabled: true } });
    li.appendText(" " + t.text);
  }
}
```

## Offene Tasks nach Bereich

### Projekte (01)

```dataviewjs
const pages = dv.pages('"01 - Projects"')
  .where(p => p.file.tasks.some(t => !t.completed))
  .sort(p => p.file.mtime, 'desc');

for (const page of pages) {
  const open = page.file.tasks.where(t => !t.completed && t.text.trim() !== "");
  if (open.length === 0) continue;

  const container = this.container.createEl("details");
  const summary = container.createEl("summary");
  const link = summary.createEl("a", {
    text: page.file.name,
    cls: "internal-link",
    attr: { "data-href": page.file.name, href: page.file.name }
  });
  link.style.fontWeight = "bold";
  summary.appendText(` (${open.length})`);

  const list = container.createEl("ul");
  for (const t of open) {
    const li = list.createEl("li");
    li.createEl("input", { attr: { type: "checkbox", disabled: true } });
    li.appendText(" " + t.text);
  }
}
```

### Areas (02)

```dataviewjs
const pages = dv.pages('"02 - Areas"')
  .where(p => p.file.tasks.some(t => !t.completed))
  .sort(p => p.file.mtime, 'desc');

for (const page of pages) {
  const open = page.file.tasks.where(t => !t.completed && t.text.trim() !== "");
  if (open.length === 0) continue;

  const container = this.container.createEl("details");
  const summary = container.createEl("summary");
  const link = summary.createEl("a", {
    text: page.file.name,
    cls: "internal-link",
    attr: { "data-href": page.file.name, href: page.file.name }
  });
  link.style.fontWeight = "bold";
  summary.appendText(` (${open.length})`);

  const list = container.createEl("ul");
  for (const t of open) {
    const li = list.createEl("li");
    li.createEl("input", { attr: { type: "checkbox", disabled: true } });
    li.appendText(" " + t.text);
  }
}
```

### Permanent (04)

```dataviewjs
const pages = dv.pages('"04 - Permanent"')
  .where(p => p.file.tasks.some(t => !t.completed))
  .sort(p => p.file.mtime, 'desc');

for (const page of pages) {
  const open = page.file.tasks.where(t => !t.completed && t.text.trim() !== "");
  if (open.length === 0) continue;

  const container = this.container.createEl("details");
  const summary = container.createEl("summary");
  const link = summary.createEl("a", {
    text: page.file.name,
    cls: "internal-link",
    attr: { "data-href": page.file.name, href: page.file.name }
  });
  link.style.fontWeight = "bold";
  summary.appendText(` (${open.length})`);

  const list = container.createEl("ul");
  for (const t of open) {
    const li = list.createEl("li");
    li.createEl("input", { attr: { type: "checkbox", disabled: true } });
    li.appendText(" " + t.text);
  }
}
```

### Periodic Notes (letzte 7 Tage)

```dataviewjs
const cutoff = dv.date("today").minus(dv.duration("7 days"));
const pages = dv.pages('"06 - Periodic"')
  .where(p => p.file.mtime >= cutoff && p.file.tasks.some(t => !t.completed))
  .sort(p => p.file.mtime, 'desc');

for (const page of pages) {
  const open = page.file.tasks.where(t => !t.completed && t.text.trim() !== "");
  if (open.length === 0) continue;

  const container = this.container.createEl("details");
  const summary = container.createEl("summary");
  const link = summary.createEl("a", {
    text: page.file.name,
    cls: "internal-link",
    attr: { "data-href": page.file.name, href: page.file.name }
  });
  link.style.fontWeight = "bold";
  summary.appendText(` (${open.length})`);

  const list = container.createEl("ul");
  for (const t of open) {
    const li = list.createEl("li");
    li.createEl("input", { attr: { type: "checkbox", disabled: true } });
    li.appendText(" " + t.text);
  }
}
```

## Kuerzlich erledigte Tasks (letzte 14 Tage)

```dataviewjs
const exclude2 = ["99 - Meta/Templates", "99 - Meta/Patterns", "Fabric", "copilot-custom-prompts"];
const cutoff = dv.date("today").minus(dv.duration("14 days"));
const pages = dv.pages()
  .where(p => !exclude2.some(e => p.file.folder.startsWith(e)))
  .where(p => p.file.mtime >= cutoff && p.file.tasks.some(t => t.completed))
  .sort(p => p.file.mtime, 'desc');

for (const page of pages) {
  const done = page.file.tasks.where(t => t.completed && t.text.trim() !== "");
  if (done.length === 0) continue;

  const container = this.container.createEl("details");
  const summary = container.createEl("summary");
  const link = summary.createEl("a", {
    text: page.file.name,
    cls: "internal-link",
    attr: { "data-href": page.file.name, href: page.file.name }
  });
  link.style.fontWeight = "bold";
  summary.appendText(` (${done.length} erledigt)`);

  const list = container.createEl("ul");
  for (const t of done) {
    const li = list.createEl("li");
    li.createEl("input", { attr: { type: "checkbox", checked: true, disabled: true } });
    const s = li.createEl("s");
    s.appendText(" " + t.text);
  }
}
```

## Task-Statistik

```dataview
TABLE
  length(filter(file.tasks, (t) => !t.completed)) AS "Offen",
  length(filter(file.tasks, (t) => t.completed)) AS "Erledigt",
  length(file.tasks) AS "Gesamt"
WHERE length(file.tasks) > 0
  AND !contains(file.folder, "99 - Meta/Templates")
  AND !contains(file.folder, "99 - Meta/Patterns")
  AND !contains(file.folder, "Fabric")
  AND !contains(file.folder, "copilot-custom-prompts")
SORT length(filter(file.tasks, (t) => !t.completed)) DESC
LIMIT 20
```
