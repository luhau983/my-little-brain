# LittleBrain 🧠

A self-maintaining knowledge base with **two trees**. **Beerus** writes the wiki; you curate and ask.

## Two domains
- **`doltech/`** — engineering knowledge from work (doltech projects). Shareable with the team later.
- **`personal/`** — personal projects + external knowledge you study. Private.

Each is a self-contained mini-wiki: `raw/` (sources), `wiki/` (Beerus pages), `index.md` (catalog),
`outputs/` (slides/charts). They share one `CLAUDE.md` (the rules) and one root `log.md` (timeline).
Root `index.md` is the front door.

## The three things you do
**1. Ingest** — add knowledge.
- Drop a file into `doltech/raw/...` or `personal/raw/...` and say: `ingest <path>`.
- Beerus picks the domain, reads it, discusses takeaways, writes the source page + updates
  entities/concepts, fixes cross-refs, flags contradictions, updates that domain's index + the log, commits.

**2. Query** — ask anything.
- `What do we know about MongoDB transactions in our Micronaut setup?`
- Beerus reads the front door → the right domain index → pages, answers with citations, offers to file it back.

**3. Lint** — keep it healthy.
- `lint doltech` / `lint personal` → contradictions, stale claims, orphans, missing pages, data gaps.

## Recommended setup
- Open this folder as an **Obsidian vault**; Beerus on one side, Obsidian on the other.
- Settings → Files & links → attachment folder per domain `raw/assets/`; bind a "Download attachments" hotkey.
- Use **graph view** to see hubs vs orphans (two clusters, one per domain). Enable **Dataview**.

## Tips
- Ingest one source at a time and stay involved — quality compounds.
- Keep the boundary: never let personal notes drift into `doltech/`.
- It's a git repo: `git log` is your changelog.
