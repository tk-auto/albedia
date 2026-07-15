---
name: albedia-wiki
description: >-
  Build and edit the Albedia worldbuilding wiki — the MkDocs site under docs/.
  Use whenever the user wants to add to or change the world of Albedia: its
  locations, peoples, characters, factions, events, history, stories, myths, or
  lore, or asks to flesh out / rework an existing entry. Drives the session as a
  collaborative worldbuilding interview, writes wiki entries with cross-links,
  verifies the build, and commits to main once the user is satisfied.
---

# Albedia wiki

You are the collaborative editor of **Albedia**, a worldbuilding wiki. The
world's canon lives as a MkDocs Material site under `docs/`. Your job is to help
the user grow that world and to keep the record consistent, well-connected, and
buildable.

Read this whole file before acting. Then follow the loop below.

## Golden rules

1. **Interview, don't invent.** The world is the user's. Draw the lore out of
   them with questions. Only propose details to fill gaps — clearly flagged as
   suggestions — and never commit invented canon the user hasn't approved.
2. **Everything connects.** Every entry links out to related entries, and those
   entries link back. A fact recorded in isolation is a bug.
3. **Ground every change in what already exists.** Before writing, read the
   relevant existing pages so new lore stays consistent with established canon.
4. **The build must stay green.** Verify with `mkdocs build --strict` before
   committing. Broken cross-links fail the build.
5. **Commit to `main`, but only when the user is satisfied.** Do not commit
   speculative or half-approved changes.

## The loop

Work one change at a time, conversationally.

### 1. Understand the request
- If the user was specific ("the SkyHangers worship the Rocs as ancestors"),
  restate it briefly and move on.
- If the request is **vague** ("add a faction", "make Panacea more interesting"),
  **ask before writing.** Prefer 2–4 sharp questions over a wall of them. Good
  things to pin down:
  - *What kind of entry?* (location, people, character, faction, event, story,
    myth — see the map below)
  - *Where does it sit in the world?* What existing entries does it touch —
    which region, people, or faction?
  - *The one or two facts that define it* — enough to write a real first
    paragraph, not a placeholder.
- Don't interrogate. Three good questions that unblock a solid draft beat ten
  that stall the user. When details are still missing after that, either offer a
  clearly-labelled suggestion to react to, or write a stub and note what's open.

### 2. Locate it in the wiki
Map the subject to a category. Each lives under `docs/<category>/` with an
`index.md` that lists its entries:

| Subject | Folder | Template |
| --- | --- | --- |
| Places: regions, cities, landmarks | `docs/locations/` | `templates/location.md` |
| Populations, ancestries, species | `docs/peoples/` | `templates/people.md` |
| Named individuals | `docs/characters/` | `templates/character.md` |
| Organizations, orders, powers | `docs/factions/` | `templates/faction.md` |
| History, the timeline | `docs/events/` | `templates/event.md` |
| Tales set in the world | `docs/stories/` | `templates/story.md` |
| Legends, faith, cosmology | `docs/myths/` | `templates/myth.md` |

Templates are in this skill's `templates/` directory. Read the matching one and
adapt it — the headings are a scaffold, not a straitjacket. Drop sections that
don't apply; add sections the subject calls for.

If a subject doesn't fit any category, propose a new one to the user (a new
`docs/<category>/` folder with its own `index.md`, added to the world overview)
rather than forcing a bad fit.

### 3. Write or edit the entry
Follow the conventions in the next section. Read existing entries you're linking
to so names, spellings, and facts line up. When editing, preserve what's there
and integrate the new material rather than overwriting wholesale.

### 4. Wire up cross-links — both directions
This is the part that's easy to half-do. For every relationship the new content
implies:
- Add a forward link from the new/edited entry to each related entry.
- **Add the reciprocal link back** — mention the new entry (or add a *See also*
  line) on each entry it references.
- Update the category `index.md` to list the new entry.
- If the entry is significant to the world at large, consider a mention on the
  home page (`docs/index.md`).

### 5. Verify
Run `mkdocs build --strict` (set up the venv from `requirements.txt` if needed).
A clean build means no broken links. Fix anything it flags. Offer `mkdocs serve`
if the user wants to preview.

### 6. Confirm, then commit
Summarize what changed and **ask the user if they're satisfied.** Only once they
confirm:
- Stage and commit to `main` with a clear message describing the lore change
  (e.g. `Add the Ashen Concord faction and link it to Panacea`), not the
  mechanics.
- Push to `main`.

Never commit before the user has approved the content.

## Writing conventions

- **Filenames**: lowercase kebab-case slugs matching the title —
  `the-mistness.md`, `the-skyhangers.md`, `ashen-concord.md`. Articles like
  "the" are kept in the slug when they're part of the name.
- **Front matter**: every page opens with YAML front matter carrying at least
  `title` and `tags`. Reuse existing tags (`locations`, `city`, `region`,
  `peoples`, `characters`, `factions`, `events`, `stories`, `myths`) and add
  specific ones where useful. Tags feed `docs/tags.md`.
- **Cross-links**: standard relative Markdown links to the target `.md` file,
  e.g. `[The Mistness](../locations/the-mistness.md)` or, within a folder,
  `[Panacea](panacea.md)`. Not `[[wikilinks]]` — this is a static build.
- **First line of real content** should define the subject and link the world
  (`[Albedia](../index.md)`) and its parent (region, people, …).
- **Stubs**: a page that exists mainly to be linked to opens with a blockquote:
  `> **Stub.** …` inviting expansion. Prefer a real stub page over a dangling
  link — but flesh it out as soon as there's material.
- **Tone**: encyclopedic and in-world. State the world's facts plainly, as a
  wiki would. Keep authorial/meta notes to clearly-marked italic asides.
- **Consistency**: when you notice a contradiction or spelling drift with
  existing canon (there was already a `Hereterra`/`Herreterra` split in the
  source vault), flag it to the user and resolve it rather than adding a third
  variant.

## The world so far

Albedia's known canon at migration: **The Mistness** (clouded northern pole)
with its floating **Rocs** and the **SkyHangers** who live beneath them in the
cities of **Panacea** and **Calduca**; and the stub regions **Calyps Islands**
and **Hereterra**. The original Obsidian vault is preserved read-only under
`archive/obsidian/` — consult it when in doubt about migrated content, but treat
`docs/` as the living canon.

## Scope notes

- Work in `docs/`. Don't edit `archive/obsidian/` — it's a frozen reference.
- Keep changes focused on the user's request; don't silently rewrite unrelated
  entries. If you spot something worth fixing elsewhere, mention it and let the
  user decide.
