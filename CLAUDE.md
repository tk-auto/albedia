# Albedia

This repository is the **Albedia worldbuilding wiki** — a static MkDocs Material
site under `docs/` that records the world's locations, peoples, characters,
factions, events, stories, and myths.

## Default workflow: use the `albedia-wiki` skill

For any request that adds to or changes the world of Albedia — new or reworked
locations, peoples, characters, factions, events, history, stories, myths, or
lore of any kind — **use the [`albedia-wiki` skill](.claude/skills/albedia-wiki/SKILL.md)
by default.** It is the primary way to work in this repo: it interviews the user
for missing details, writes cross-linked wiki entries, verifies the strict
build, and commits to `main` once the user is satisfied.

Do not hand-edit `docs/` content ad hoc when a worldbuilding change is intended
— follow the skill so conventions, cross-linking, and the build stay intact.

The skill does not apply to purely technical work on the wiki's tooling itself
(the MkDocs config, CI workflow, or build setup); handle those directly.

## Quick facts

- Content lives in `docs/`; each category folder has an `index.md`.
- Build/preview: `pip install -r requirements.txt` then `mkdocs serve` (preview)
  or `mkdocs build --strict` (must pass — broken cross-links fail it).
- Pushes to `main` auto-deploy to GitHub Pages via `.github/workflows/deploy.yml`.
- The original Obsidian vault is archived read-only under `archive/obsidian/`.
