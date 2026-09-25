# Nota Bene

One project containing the full note-taking toolchain for reading academic
papers in Obsidian + Zotero:

```
plugins/zotero-integration/   Fork of mgmeyers' Zotero Integration plugin (GPL-3.0)
plugins/promote/              Second Reader: Promote Candidates plugin
Templates/                    Literature note (Zotero import) + permanent note templates
```

## The workflow it supports

Students read in Zotero's PDF reader with their Obsidian literature note open
alongside, **typing notes and highlighting at the same time**. Whenever they
like, they click the highlighter icon in Obsidian's left ribbon (or run
**"Sync highlights into current note"**) and every highlight or comment made
since the last sync lands under "Quotes worth keeping" — with the printed page
number — without disturbing a single character they've typed.

## What the fork adds over upstream Zotero Integration

- **Sync highlights into current note** (command + ribbon icon). Works on the
  open note via its `citekey` frontmatter, wherever the note lives or however
  it's been renamed. Applied through the live editor, so it's safe mid-typing:
  cursor, undo history, and unsaved keystrokes are preserved. If the student
  edits a quote while Zotero is being queried, their edit wins and the new
  highlights are appended on top of it.
- **Re-importing never overwrites a note.** Upstream regenerates the whole
  file on re-import, keeping only `persist` blocks — which would erase notes a
  student typed. In Nota Bene, importing an existing note merges new
  highlights into its persist blocks and changes nothing else.
- **Deduplication by Zotero annotation ID**, not by import date. Each quote
  carries a block ID (`^nb-<zotero key>`), and a highlight is only added if
  its ID isn't already anywhere in the note. This survives students editing
  quotes, moving them to other sections, typing below the end-of-file date
  marker, and highlights synced late from another device. Block IDs also let
  students link to an individual quote from a permanent note
  (`[[smith2023#^nb-ABCD1234]]`).
- **Accidentally deleted quote block is restored**, re-inserted under the
  "Quotes worth keeping" heading rather than silently dropped.
- **Upstream bug fix:** highlights on the first PDF page had no page number
  (`pageIndex` 0 was treated as missing).
- New template variables: `newAnnotations` (not yet in the note) and
  `a.nbId` (the block-ID-safe annotation ID).

Tests for all of the above: `src/bbt/tests/sync.test.ts` and
`template.sync.test.ts` (the latter renders the real literature-note template
through the plugin's Nunjucks environment). `npm test` has one pre-existing
upstream failure in `template.env.test.ts` ("sanely handles new lines"),
unrelated to these changes.

## The two plugins

- **Nota Bene: Zotero Import** (`plugins/zotero-integration/`) — forked from
  [obsidian-zotero-integration](https://github.com/mgmeyers/obsidian-zotero-integration)
  v3.2.1 under GPL-3.0 (license retained in `LICENSE.md`; this fork must stay
  GPL-3.0). Manifest id `nota-bene-zotero`, so it's independent of the
  upstream community plugin (and students switching from upstream redo the
  plugin's settings once). Build: `npm install && npm run build`; release by
  bumping `manifest.json`/`package.json`/`versions.json` and attaching
  `main.js`, `manifest.json`, `styles.css` to a GitHub release tagged with the
  version — BRAT installs from `kevinmil54/nota-bene`.

- **Second Reader: Promote Candidates** (`plugins/promote/`) — copied
  unchanged, id kept as `second-reader-promote` so existing student installs
  keep updating from their original repo. Checking a box under
  `## Permanent note candidates` creates a permanent note and links the line
  to it.

## Templates

`Templates/Literature Note Template - Zotero Import.md` is the import format
to configure in the plugin's settings (Import Formats → template file); sync
uses the import format whose template path contains "Literature Note" (else
the first one). `Templates/Permanent Note Template.md` is used by the Promote
plugin.

## Page numbers

Quotes use `a.pageLabel` — Zotero's page *label*, i.e. the printed journal
page — falling back to `a.page`, the physical PDF page. Highlights made in
Zotero's reader get the printed page; highlights made in an external PDF app
and extracted from the file may only have the physical page. If a PDF's labels
are wrong, students can fix them in Zotero's reader (right-click a page in
the thumbnails sidebar → Rename Page…), which corrects all future syncs.

## Known limitations

- Sync assumes the item is in the student's personal library (library 1);
  items in Zotero group libraries aren't matched yet.
- Deleting a quote from the note doesn't stop it coming back on the next sync
  while the highlight still exists in Zotero — delete the highlight in Zotero
  too (or keep the line and trim it).
