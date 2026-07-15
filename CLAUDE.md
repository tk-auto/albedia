# Albedia

This repository is the **Albedia worldbuilding wiki** — a static MkDocs Material
site under `docs/` that records the world's locations, peoples, characters,
factions, events, stories, and myths.

**Worldbuilding is the main activity here.** For any request that adds to or
changes the world of Albedia — new or reworked locations, peoples, characters,
factions, events, history, stories, myths, or lore of any kind — you are the
collaborative editor of the world: draw the lore out of the user, write
cross-linked wiki entries, keep the record consistent, verify the strict build,
and commit once the user is satisfied. Follow the guidance below by default so
conventions, cross-linking, and the build stay intact — don't hand-edit `docs/`
content ad hoc.

This guidance does not apply to purely technical work on the wiki's tooling
itself (the MkDocs config, CI workflow, or build setup); handle those directly.

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
| Places: regions, cities, landmarks | `docs/locations/` | `.claude/templates/location.md` |
| Populations, ancestries, species | `docs/peoples/` | `.claude/templates/people.md` |
| Named individuals | `docs/characters/` | `.claude/templates/character.md` |
| Organizations, orders, powers | `docs/factions/` | `.claude/templates/faction.md` |
| History, the timeline | `docs/events/` | `.claude/templates/event.md` |
| Tales set in the world | `docs/stories/` | `.claude/templates/story.md` |
| Legends, faith, cosmology | `docs/myths/` | `.claude/templates/myth.md` |

Templates live in `.claude/templates/`. Read the matching one and adapt it — the
headings are a scaffold, not a straitjacket. Drop sections that don't apply; add
sections the subject calls for.

If a subject doesn't fit any category, propose a new one to the user (a new
`docs/<category>/` folder with its own `index.md`, added to the world overview)
rather than forcing a bad fit.

### 3. Write or edit the entry
Follow the conventions below. Read existing entries you're linking to so names,
spellings, and facts line up. When editing, preserve what's there and integrate
the new material rather than overwriting wholesale.

### 4. Wire up cross-links — both directions
This is the part that's easy to half-do. For every relationship the new content
implies:
- Add a forward link from the new/edited entry to each related entry.
- **Add the reciprocal link back** — mention the new entry (or add a *See also*
  line) on each entry it references.
- Update the category `index.md` to list the new entry.
- Add or update a concise [glossary](#the-glossary) entry for any world-specific
  term the change introduces.
- If the entry is significant to the world at large, consider a mention on the
  home page (`docs/index.md`).

### 5. Verify
Run `mkdocs build --strict` (set up the venv from `requirements.txt` if needed).
A clean build means no broken links. Fix anything it flags. Offer `mkdocs serve`
if the user wants to preview.

### 6. Confirm, then commit
Summarize what changed and **ask the user if they're satisfied.** Only once they
confirm, stage and commit to `main` with a clear message describing the lore
change (e.g. `Add the Ashen Concord faction and link it to Panacea`), not the
mechanics. Then push. Never commit before the user has approved the content.

## Writing conventions

- **Filenames**: lowercase kebab-case slugs matching the title —
  `mistness.md`, `the-skyhangers.md`, `ashen-concord.md`. Articles like
  "the" are kept in the slug when they're part of the name — except for
  locations, which never take one (see next rule).
- **Locations take no leading "The" in titles and main links**: location
  entries are named without a leading article — *Mistness*, *Barren Peaks*,
  *Scythed Lands*, never "The Mistness" — in front-matter titles, slugs,
  headings, and the link text of listings (category indexes, tables, *See
  also* lines, "See …" references). In **running prose**, keep a lowercase
  "the" where the name is a noun and grammar calls for it — "rising in the
  Barren Peaks", "a city of the Mistness", "the Taje Plateaus" — writing the
  article outside the link text: `the [Mistness](…)`. This rule is specific to
  locations; entries in other categories (peoples, myths, …) keep their
  article when it's part of the name (e.g. *The SkyHangers*).
- **Front matter**: every page opens with YAML front matter carrying at least
  `title` and `tags`. Reuse existing tags (`locations`, `city`, `region`,
  `peoples`, `characters`, `factions`, `events`, `stories`, `myths`, `glossary`)
  and add specific ones where useful. Tags feed `docs/tags.md`.
- **Cross-links**: standard relative Markdown links to the target `.md` file,
  e.g. `[Mistness](../locations/mistness.md)` or, within a folder,
  `[Panacea](panacea.md)`. Not `[[wikilinks]]` — this is a static build. Linking
  to a heading anchor within a page (e.g. `the-skyhangers.md#terminology`) is
  fine, since headings get anchors; do not link to definition-list terms, which
  don't get one.
- **First line of real content** should define the subject and link the world
  (`[Albedia](../index.md)`) and its parent (region, people, …).
- **Stubs**: a page that exists mainly to be linked to opens with a blockquote:
  `> **Stub.** …` inviting expansion. Prefer a real stub page over a dangling
  link — but flesh it out as soon as there's material.
- **Tone**: encyclopedic and in-world. State the world's facts plainly, as a
  wiki would. Keep authorial/meta notes to clearly-marked italic asides.
- **Consistency**: when you notice a contradiction or spelling drift with
  existing canon, flag it to the user and resolve it rather than adding a third
  variant.

## The glossary

`docs/glossary.md` is the world's **global glossary** — the single place that
collects Albedia's particular vocabulary (common-noun terms such as *Roc*,
*Anchor*, *Courser*, *Glider*), as distinct from the proper names of places or
peoples, which live in their own entries.

- Each glossary entry is a **short** definition (a definition-list `Term` /
  `:   definition` pair) that **links out to the fuller account** in the relevant
  location or people article. The detailed treatment stays in that article; the
  glossary is the index across the whole world.
- When a change coins or leans on a world-specific term, add or update its
  glossary entry, and link the term's home article back to the glossary
  (reciprocal, like any cross-link).
- Tag glossary content with the `glossary` tag; the page is surfaced on the home
  page grid.

## The world so far

Albedia's canon includes: **Mistness** (clouded northern pole) with its
floating **Rocs** and the **SkyHangers** who live suspended beneath them in the
cities of **Panacea** and **Calduca**; the broad southern region of
**Hereterra** and its many locations (the Diamond River, Val Verde, the Barren
Peaks, the Scythed Lands, the Esper Counties, and more); and the stub region
**Calyps Islands**. The original Obsidian vault is preserved read-only under
`archive/obsidian/` — consult it when in doubt about migrated content, but treat
`docs/` as the living canon.

## Quick facts

- Content lives in `docs/`; each category folder has an `index.md`.
- Build/preview: `pip install -r requirements.txt` then `mkdocs serve` (preview)
  or `mkdocs build --strict` (must pass — broken cross-links fail it).
- Nav is generated automatically from the `docs/` tree; no `mkdocs.yml` edits are
  needed when adding a page.
- Pushes to `main` auto-deploy to GitHub Pages via `.github/workflows/deploy.yml`.

## Committing

Always commit directly to `main` — no feature branches, no pull requests, no
fuss. Make the change, ensure `mkdocs build --strict` passes, commit, and push
to `main`.

## After the change lands on `main`

Once the change is on `main` (the push, or a merge), the GitHub Pages deploy runs
automatically via [`.github/workflows/deploy.yml`](.github/workflows/deploy.yml).
Don't stop there:

1. **Wait for the deploy Action to finish** — watch the workflow run triggered by
   the commit until it completes (a green success, not merely "queued" or
   "in progress").
2. **Present the published URL to the user** — once the run succeeds, give them
   the live GitHub Pages link, <https://tk-auto.github.io/albedia/>, so they can
   see the change on the site.

If the Action fails, report the failure and what broke rather than sending the
URL as though it succeeded.
