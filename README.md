# Obsidian Vault Skeleton

An empty Obsidian vault with a PARA-style folder structure, the Vanilla AMOLED theme,
CSS snippets, plugins, templates and dashboards. Contains no notes.

## Use as a new vault

1. Clone or download this repo.
2. In Obsidian: *Open folder as vault* and select the folder.
3. Confirm *Trust author and enable plugins*.

## Add the CSS to an existing vault

Close Obsidian first, or reload it afterwards (`Cmd/Ctrl+P` → *Reload app without saving*).

### 1. Copy the files

Copy these folders from this repo into the `.obsidian` folder of your vault.
`.obsidian` is hidden: on macOS press `Cmd+Shift+.` in Finder to show it.

| From this repo                      | To your vault                       |
|-------------------------------------|-------------------------------------|
| `.obsidian/snippets/*.css`          | `<your vault>/.obsidian/snippets/`  |
| `.obsidian/themes/Vanilla AMOLED/`  | `<your vault>/.obsidian/themes/`    |

Create `snippets` or `themes` if it does not exist yet.
Do **not** copy `appearance.json`; it would overwrite your own appearance settings.

### 2. Enable them

- *Settings → Appearance → Themes*: select **Vanilla AMOLED**.
- *Settings → Appearance → CSS snippets*: click the reload icon, then switch on the snippets you want.

### 3. What each snippet does and how to use it

| Snippet                   | Effect | How to trigger it |
|---------------------------|--------|-------------------|
| **Colored Sidebar Items** | Colors folders in the file explorer | Automatic for folders whose names start with `00`–`07`, `99`, `Excali` or `Fabric`. For other folder names, edit the `data-path^="..."` selectors in the file. |
| **Daily Note Themes**     | One color scheme per weekday | Frontmatter `cssclasses: [daily, monday]` (or `tuesday` … `sunday`) |
| **Weekly_Note_Themes**    | Color scheme for weekly notes | Frontmatter `cssclasses: [weekly]` |
| **Notebook Backgrounds**  | Paper backgrounds and pen colors | `cssclasses: [page-white]`, `page-manila` or `page-blueprint`, optionally combined with `pen-blue`, `pen-red`, … |

Example frontmatter:

```yaml
---
cssclasses: [daily, friday]
---
```

The templates in `99 - Meta/Templates` already set these classes automatically:
`Daily (Vanilla)` adds `daily` plus the weekday (via `{{date:dddd}}`), `Weekly` adds `weekly`.
Copy them into your vault's template folder to get the themed notes without manual work.

### 4. Fonts (optional)

The snippets and appearance settings expect **MesloLGL Nerd Font**, **JetBrainsMono Nerd Font**
and **Bai Jamjuree**. Without them Obsidian falls back to default fonts; everything still works.
Install them from [nerdfonts.com](https://www.nerdfonts.com/font-downloads) and
[Google Fonts](https://fonts.google.com/specimen/Bai+Jamjuree), then set them under
*Settings → Appearance → Font*.

## Hotkeys

| Shortcut          | Action | Requires |
|-------------------|--------|----------|
| `Alt+Shift+N`     | New unique note (`YYYYMMDDHHmm` prefix) in `05 - Fleeting`, using template `Unique` | Core plugin *Unique note creator* |
| `Alt+Shift+T`     | Insert a Templater template into the current note | Community plugin *Templater* |
| `Alt+Shift+D`     | Insert template `Daily (Vanilla)` | *Templater*, plus the template registered as a hotkey (see below) |

On macOS `Alt` is the `Option` key.

### Add the hotkeys to an existing vault

**Option A: set them by hand** (safe, keeps your own hotkeys)

1. *Settings → Hotkeys*, search for the command, click the `+` and press the shortcut:
   - *Unique note creator: Create new unique note* → `Alt+Shift+N`
   - *Templater: Open insert template modal* → `Alt+Shift+T`
2. For `Alt+Shift+D`: *Settings → Templater → Template hotkeys → Add new hotkey for template*,
   choose `Daily (Vanilla)`. Then assign `Alt+Shift+D` to the new command
   *Templater: Insert Daily (Vanilla)* under *Settings → Hotkeys*.

**Option B: copy the file**

Copy `.obsidian/hotkeys.json` into `<your vault>/.obsidian/`. This **replaces** all your
existing custom hotkeys. If you already have some, merge the entries into your file instead.

Either way, the folder and template paths must exist in your vault. Adjust them under
*Settings → Unique note creator* and *Settings → Templater* (template folder), or copy
`99 - Meta/Templates` and `05 - Fleeting` from this repo.

## Credits

Snippets *Colored Sidebar Items*, *Daily Note Themes* and *Notebook Backgrounds* by CyanVoxel.
