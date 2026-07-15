# Albedia

The worldbuilding wiki for **Albedia** — a static, wiki-like encyclopedia of the
world's lands, peoples, factions, history, stories, and myths. Built with
[MkDocs Material](https://squidfunk.github.io/mkdocs-material/).

This repository was migrated from an Obsidian vault. The original vault
(`.canvas` graphs, notes, and Obsidian config) is preserved under
[`archive/obsidian/`](archive/obsidian/) for reference.

## Structure

```
docs/
  index.md          # World overview — the front door of the wiki
  locations/        # Places: regions, cities, landmarks, geography
  peoples/          # Peoples, populations, ancestries, species
  characters/       # Individuals — named people and beings
  factions/         # Organizations, orders, powers, alliances
  events/           # History and the timeline
  stories/          # Tales and narratives set in the world
  myths/            # Legends, religion, cosmology
  glossary.md       # Global glossary of world-specific terms
  tags.md           # Auto-generated tag index
archive/obsidian/   # Original Obsidian vault (read-only reference)
.claude/templates/  # Entry scaffolds for each category
CLAUDE.md           # How Claude edits the world (conventions + workflow)
```

Each category folder has an `index.md` that lists and introduces its entries.

## Editing with Claude

Worldbuilding is the main activity in this repo, so Claude works this way by
default — the full workflow and conventions live in
[`CLAUDE.md`](CLAUDE.md), with entry scaffolds in
[`.claude/templates/`](.claude/templates/). Just tell Claude what you want to add
or change ("add a faction that rules Panacea", "flesh out the SkyHangers", "what
myths do the SkyHangers tell?") and it will interview you for the missing
details, write the entry using the conventions below, wire up cross-links, verify
the build, and commit.

## Conventions

- **Filenames** are lowercase kebab-case slugs (`the-mistness.md`,
  `the-skyhangers.md`).
- **Every page** starts with YAML front matter containing `title` and `tags`.
- **Cross-links** are standard relative Markdown links to the target `.md`
  file, e.g. `[The Mistness](../locations/the-mistness.md)`. When you link A → B,
  add a reciprocal mention (or a **See also** entry) B → A so the web stays
  connected in both directions.
- **Stubs** (pages that exist mainly to be linked to) carry a
  `> **Stub.** …` note inviting expansion.

## Build & preview

Requires Python 3.9+.

```bash
python -m venv .venv && source .venv/bin/activate
pip install -r requirements.txt

mkdocs serve            # live preview at http://127.0.0.1:8000
mkdocs build --strict   # production build into site/ ; fails on broken links
```

`--strict` turns broken internal links into build errors, so cross-links can't
silently rot.

## Deployment

Every push to `main` builds the site and publishes it to **GitHub Pages** via
[`.github/workflows/deploy.yml`](.github/workflows/deploy.yml). The workflow runs
`mkdocs build --strict`, so a broken cross-link fails the deploy instead of
shipping a broken wiki.

One-time setup: in the repository's **Settings → Pages**, set **Source** to
**GitHub Actions**. The site then publishes to
<https://tk-auto.github.io/albedia/>.
