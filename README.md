# LittleBrain 🧠

A self-maintaining technical knowledge base. **Beerus** writes the wiki; you curate and ask.

## Layout
- `raw/` — drop your sources here (never edited). Source of truth.
- `wiki/` — Beerus-generated, interlinked pages. Browse in Obsidian.
- `outputs/` — generated slides/charts.
- `CLAUDE.md` — the rules Beerus follows. `index.md` — catalog. `log.md` — history.

## The three things you do

**1. Ingest** — add knowledge.
- Drop a file into `raw/articles|papers|transcripts|books/` (Obsidian Web Clipper is great for web).
- Tell Beerus: `ingest raw/articles/<file>.md`
- Beerus reads it, discusses takeaways, then writes the source page + updates entities/concepts,
  fixes cross-refs, flags contradictions, updates the index & log, and commits.

**2. Query** — ask anything.
- `What do we know about MongoDB transactions vs our Micronaut setup?`
- Beerus reads the index, finds pages, answers with citations, and offers to file the answer back.

**3. Lint** — keep it healthy.
- `lint the wiki` → contradictions, stale claims, orphans, missing pages, data gaps + suggested sources.

## Recommended setup
- Open this folder as an **Obsidian vault**; keep Beerus on one side, Obsidian on the other.
- Obsidian → Settings → Files & links → set attachment folder to `raw/assets/`, bind a "Download
  attachments" hotkey so clipped images land locally.
- Use the **graph view** to see hubs vs orphans. Enable **Dataview** for dynamic tables from frontmatter.

## Tips
- Ingest one source at a time and stay involved — quality compounds.
- Good answers shouldn't die in chat — let Beerus file them as synthesis pages.
- It's a git repo: `git log` is your wiki's changelog.
