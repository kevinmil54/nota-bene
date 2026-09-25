# Nota Bene

One project containing the full note-taking toolchain for reading academic
papers in Obsidian + Zotero:

```
plugins/zotero-integration/   Fork of mgmeyers' Zotero Integration plugin (GPL-3.0)
plugins/promote/              Second Reader: Promote Candidates plugin
Templates/                    Literature note (Zotero import) + permanent note templates
```

## What's new vs. the pieces it combines

**Highlights and annotations import as quotes, with page numbers.** The
literature-note template's "Quotes worth keeping" section now pulls every
highlight and annotation from the paper's PDF at import time:

- Highlighted text becomes `> "…" (p. N)`
- A comment attached to a highlight appears under its quote as *my note: …*
- Rectangle/area annotations import as embedded images, also with page numbers
- The block is wrapped in `{% persist "annotations" %}`, so re-importing the
  same item refreshes quotes without clobbering anything you wrote elsewhere

This works because the plugin already extracts PDF annotations (via
pdf-annots2json) and exposes them to Nunjucks templates as `annotations`
(fields: `annotatedText`, `page`, `comment`, `imageRelativePath`, `color`…).
So the feature lives in the template; the plugin fork exists so we can go
further when template-level changes aren't enough (e.g. page-label offsets,
color-based routing of highlights into different sections).

## The two plugins

- **Nota Bene: Zotero Import** (`plugins/zotero-integration/`) — forked from
  [obsidian-zotero-integration](https://github.com/mgmeyers/obsidian-zotero-integration)
  v3.2.1 under GPL-3.0 (license retained in `LICENSE.md`; this fork must stay
  GPL-3.0). Manifest id changed to `nota-bene-zotero` so it can be installed
  alongside — or distributed independently of — the upstream community plugin.
  Note: students switching from upstream will need to redo the plugin's
  settings (import format, bibliography style), since a new id means a fresh
  settings file. Build: `yarn && yarn build` (produces `main.js`).

- **Second Reader: Promote Candidates** (`plugins/promote/`) — copied
  unchanged, id kept as `second-reader-promote` so existing student installs
  keep updating. Checking a box under `## Permanent note candidates` creates a
  permanent note and links the line to it.

## Templates

`Templates/Literature Note Template - Zotero Import.md` is the import format
to configure in the Zotero plugin's settings (Import Formats → template file).
`Templates/Permanent Note Template.md` is used by the Promote plugin.

## Page-number behavior

For annotations made in **Zotero's built-in PDF reader** (the workflow we
teach), `{{a.page}}` carries Zotero's page *label* — the printed journal page
number, not the PDF sheet number — so quotes cite real pages. For highlights
made in external PDF apps and extracted straight from the file, only the
physical PDF page is available; applying a per-item offset there is the first
candidate for a real code change in the fork.
