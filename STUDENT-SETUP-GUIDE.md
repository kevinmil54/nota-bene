# Setting Up Your Nota Bene Note System

This gets your computer ready to take literature notes the Nota Bene way:
highlight and annotate a paper in Zotero, import it into a structured note —
your highlights arrive automatically as quotes with page numbers — take your
own notes, and promote your best ideas into standalone permanent notes with
one click. It's a one-time setup (30–45 minutes) — after that, each new paper
takes seconds to turn into a note.

Works on **Mac or Windows**. Steps are marked where they differ.

---

## 1. Get a good markdown editor

Your notes are plain text files in a format called **Markdown** (`# heading`,
`**bold**`, `[[links]]`). Obsidian (step 2) *is* a markdown editor and will
be where you do almost all your writing — but it's worth having a
lightweight general-purpose one too, for quickly opening a `.md` file
without launching Obsidian.

**Recommended: [Zettlr](https://www.zettlr.com/)** — free, open-source, and
identical on Mac and Windows. Unlike a general code editor, it's built
specifically for academic Markdown writing (citations, footnotes, live
preview), which fits this note-taking system well.

- **Mac:** Download the `.dmg` → open it → drag **Zettlr** to Applications.
- **Windows:** Download the installer → run it → accept the defaults.

**If you work with R or Quarto:** use **[Positron](https://positron.posit.co/)**
instead (or alongside Zettlr) — Posit's IDE built for R, Python, and Quarto
(`.qmd`) documents. Same install pattern on both platforms: download →
run the installer → open.

**Avoid TextEdit (Mac) and WordPad (Windows) for this** unless you switch
them to plain-text mode — both default to rich text and will quietly corrupt
a `.md` file with hidden formatting. Plain Notepad on Windows is fine in a
pinch; on Mac, use TextEdit's **Format → Make Plain Text** first.

---

## 2. Install Obsidian

1. Go to **[obsidian.md](https://obsidian.md/)** and click **Download** — it
   detects your OS automatically.
2. **Mac:** open the downloaded `.dmg`, drag **Obsidian** into Applications,
   launch it.
   **Windows:** run the downloaded installer, launch Obsidian when it
   finishes.
3. On first launch: **Create a new vault** (a vault is just a folder of
   notes). If your instructor gave you a starter vault instead, choose
   **Open folder as vault** and pick that folder.

---

## 3. Install Zotero

Zotero is where your papers live. It feeds Obsidian the metadata (title,
authors, citation key) for each note — and, in this system, it's also **where
you do your highlighting**: anything you highlight or comment on in Zotero's
PDF reader lands in your note as a quote with its page number.

1. Go to **[zotero.org/download](https://www.zotero.org/download/)** and
   download **Zotero 7** for your OS.
2. **Mac:** open the `.dmg`, drag Zotero to Applications.
   **Windows:** run the installer.
3. Launch Zotero. Create a free account at zotero.org when prompted, and
   sign in (Zotero → Settings → Sync) — this backs up your library and lets
   you use Zotero on more than one device. Not required, but you'll want it.
4. **Turn on the setting that lets Obsidian talk to Zotero:** Zotero →
   Settings → **Advanced** → check **"Allow other applications to
   communicate with Zotero."** Zotero must be running (in the background is
   fine) whenever you import a note in Obsidian.
5. **Install the Better BibTeX plugin.** This is what generates the stable
   citation key (like `smith2023learning`) and the formatted APA reference
   the templates use — without it, those fields come out blank.
   - Download the latest `.xpi` from
     **[the Better BibTeX releases page](https://github.com/retorquere/zotero-better-bibtex/releases/latest)**
     (the file named `zotero-better-bibtex-X.X.X.xpi`).
   - In Zotero: **Tools → Plugins** → gear icon (top right) → **"Install
     Plugin From File..."** → select the downloaded `.xpi`.
   - Restart Zotero.

### 3a. Install the Zotero Connector (browser extension)

This is what saves an article into Zotero straight from your browser.

1. Go to **[zotero.org/download](https://www.zotero.org/download/)** and
   scroll to **"Zotero Connector."** It detects your browser (Chrome,
   Firefox, Edge, Safari) and gives you the right install button.
2. Click it, then confirm the install in your browser's extension store.
3. **To use it:** open an article's webpage (or its PDF), click the Zotero
   icon that appears in your browser's toolbar. It saves the citation info —
   and the PDF, when available — into whichever collection is currently
   selected in the Zotero app. Zotero must be open for this to work.

---

## 4. Set up Obsidian for the Nota Bene note system

### a. Turn on community plugins
Settings (gear icon) → **Community plugins** → **Turn on community
plugins** (you'll see a one-time warning about third-party code — this is
expected).

### b. Install "BRAT"
Settings → Community plugins → **Browse** → search **"BRAT"** (Beta
Reviewers Auto-update Tool) → **Install** → **Enable**. BRAT is what lets
you install the two custom Nota Bene plugins below, which aren't in
Obsidian's official plugin list.

### c. Install "Nota Bene: Zotero Import"
This is Nota Bene's own version of the Zotero Integration plugin.

1. Command Palette (`Cmd/Ctrl+P`) → **"BRAT: Add a beta plugin for
   testing."**
2. Paste: `kevinmil54/nota-bene`
3. Settings → Community plugins → enable **"Nota Bene: Zotero Import."**

(If you already have the community "Zotero Integration" plugin installed
from another class, disable it — running both at once will give you two
copies of every import command.)

### d. Install "Second Reader: Promote Candidates"
1. Command Palette → **"BRAT: Add a beta plugin for testing."**
2. Paste: `kevinmil54/second-reader-obsidian-promote`
3. Settings → Community plugins → enable **"Second Reader: Promote
   Candidates."**

### e. Get the two templates into your vault
Your instructor will give you two files — **`Literature Note Template -
Zotero Import.md`** and **`Permanent Note Template.md`** — or you can get
them from
**[the Nota Bene repo's Templates folder](https://github.com/kevinmil54/nota-bene/tree/main/Templates)**
(open each file there and use the download button). Use the versions that
come with Nota Bene: the literature template is what makes your Zotero
highlights import as quotes.

Create a `Templates` folder inside your vault (in Obsidian's file explorer,
right-click → **New folder**) and put both files in it.

### f. Point the plugin at the permanent-note template
Settings → **Second Reader: Promote Candidates** → **Template path** →
enter `Templates/Permanent Note Template.md` (match the path to wherever
you put it in step e).

### g. Configure the import format
Settings → **Nota Bene: Zotero Import** → **Import Formats** → add a new
format:
- **Name:** `Nota Bene Literature Note`
- **Template:** the path to `Templates/Literature Note Template - Zotero
  Import.md`
- **Output path template:** `Literature_notes/{{citekey}}.md` (creates a
  `Literature_notes` folder automatically)
- **Bibliography Style:** search **"APA"** → choose **American Psychological
  Association 7th edition**

### h. (Optional, recommended) Auto-open imported notes
Same Settings page → toggle **"Open the created or updated note(s) after
import"** on, so each new literature note opens automatically.

---

## Generating a note for a particular article

Once setup is done, this is the whole routine per paper:

1. **Get the article into Zotero.** On the article's webpage, click the
   Zotero Connector button in your browser (best — pulls in full metadata).
   Or drag the PDF straight into the Zotero app window.
2. **Check it saved correctly** — title, authors, and year look right in
   Zotero. If you dragged in a bare PDF and the fields are empty, right-click
   the item → **"Retrieve Metadata for PDF."**
3. **Read the paper in Zotero's PDF reader** (double-click the PDF in
   Zotero). As you read, **highlight passages worth keeping** and add sticky
   comments where you have a reaction. Use Zotero's own reader for this, not
   Preview or Adobe — Zotero's reader is what records the real (printed) page
   number for each highlight.
4. **In Obsidian:** Command Palette → **"Nota Bene: Zotero Import: Nota Bene
   Literature Note"** (the command is named after the import format from step
   4g — *not* the generic "Import notes," which skips your template).
5. Search for the article by title or author, select it (you can multi-select
   several at once).
6. Obsidian creates the literature note, pre-filled with title, authors,
   year, the Zotero link, the full APA reference — and, under **"Quotes worth
   keeping,"** every highlight you made, as a quote with its page number.
   Comments you attached to highlights appear under their quotes; area
   snapshots come in as images.
7. **Take your own notes** directly in that file — fill in "Why I'm reading
   this," "Summary (in my own words)," "Key ideas," and so on. You can edit
   the imported quotes freely (trim them, add reactions).
8. **Keep reading later?** Highlight more in Zotero, then run the same import
   command on the same article: only your *new* highlights are appended —
   nothing you've written or edited is touched.
9. When an idea is worth its own standalone note, write it (or accept a
   suggested one) under **"Permanent note candidates"** and **check its
   box** — a new permanent note is created automatically, built from the
   Permanent Note Template, and that line becomes a link to it.

---

## Troubleshooting

| Symptom | Fix |
|---|---|
| The import command for your format doesn't appear in the Command Palette | Plugin isn't enabled, or Obsidian needs a full restart (not just a reload) after enabling it. |
| Import fails / "could not connect to Zotero" | Zotero desktop must be running. Check Zotero → Settings → Advanced → "Allow other applications to communicate with Zotero" is checked. |
| Citation key or reference comes out blank, or shows `{{citekey}}` literally | Better BibTeX isn't installed, or Zotero wasn't restarted after installing it. |
| The "Import notes" command creates a blank note with just a citekey, no content | That's the generic command — it doesn't use your template. Use the command named after your import format instead ("Nota Bene: Zotero Import: Nota Bene Literature Note"), set up in step 4g. |
| No quotes appear under "Quotes worth keeping" after import | You haven't highlighted anything yet, or the highlights were made in another PDF app (Preview, Adobe) — make them in **Zotero's** PDF reader, then re-run the import on the same article. |
| Quotes show the wrong page numbers | Highlights made outside Zotero's reader only carry the PDF's sheet number. For printed page numbers, highlight in Zotero's reader (it can also fix the numbering under the reader's page-number field). |
| A highlight you deleted in Zotero is still in the note | Imports only *add* new quotes; they never remove. Delete the quote line in Obsidian by hand. |
| Checking a candidate box just crosses out the text — no new note appears | The "Second Reader: Promote Candidates" plugin isn't enabled, the note's frontmatter is missing `tags: [literature-note]`, or the heading isn't exactly `## Permanent note candidates`. |
| BRAT can't find a plugin | Double-check the repo name: `kevinmil54/nota-bene` for the Zotero import plugin, `kevinmil54/second-reader-obsidian-promote` for Promote Candidates. |
| Every import command appears twice in the Command Palette | Both "Nota Bene: Zotero Import" and the community "Zotero Integration" plugin are enabled — disable the community one. |
| Reference style isn't APA | You likely set the "Citation Style" (used for inline citations) instead of the **Import Format's own "Bibliography Style"** field — these are two separate settings in the plugin. |

---

## Updating

- **Nota Bene: Zotero Import** and **Second Reader: Promote Candidates**
  update automatically through BRAT (BRAT checks for new versions when
  Obsidian starts). To check manually: Command Palette → **"BRAT: Check for
  updates to all beta plugins and UPDATE."**
- **BRAT** itself updates like any community plugin: Settings → Community
  plugins → **Check for updates**.
- **Templates** don't update themselves — if your instructor announces a new
  template version, download it and replace the file in your vault's
  `Templates` folder. Existing notes keep whatever template they were created
  with; only new imports use the new template.
