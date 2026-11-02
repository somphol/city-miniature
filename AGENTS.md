# Agent notes — city-miniature

An OpenCode skill that builds a single-file 3D city diorama from a working San Francisco template.
Read `SKILL.md` first; this file is the handoff for whoever works on the skill itself.

## Commands

```sh
# scaffold and build a project from the template
node scripts/new-project.mjs --out /tmp/try-city
cd /tmp/try-city && npm ci && npm run build:single && node tests/run.mjs

# reinstall the working copy after editing this repo
rsync -a --delete --exclude .git --exclude docs ~/Projects/city-miniature/ \
  ~/.config/opencode/skills/city-miniature/
```

`new-project.mjs` copies `assets/san-francisco-diorama`, skipping `node_modules`, `dist`,
`dist-single`, `shots` and `film`, and rewrites the package name. There is no build step for the
skill itself; the assets are the source.

## Architecture

The skill is a template plus documentation. Nothing here executes at skill load time.

- `SKILL.md` — the model-facing instructions: when to use, workflow, module map, recipes.
- `assets/san-francisco-diorama/` — the actual project. Its own `src/`, `tests/` and `scripts/` are
  what a scaffolded user gets.
- `references/` — the deep detail the model reads on demand.
- `scripts/new-project.mjs` — the only skill-level executable.
- `results/` — a built reference output, for eyeballing what "done" looks like.

The template's construction order is documented in `references/method.md`; do not reorder it without
reading that file.

## Constraints

- The published artifact must stay a **single self-contained HTML file** under a strict CSP: no
  fetch, no fonts, no image URLs, no storage. Anything that adds a network request breaks the premise.
- `SKILL.md` is read by a model, not a parser: keep it short, concrete and free of hedging.
- `assets/…/src/i18n/strings.json` carries both English and Simplified Chinese. Keep the keys in sync.
- Do not vendor `node_modules` or build output into the repo; `.gitignore` covers them.
- The installed copy at `~/.config/opencode/skills/city-miniature` must be re-synced after edits here
  (command above), or the skill will describe a newer template than it ships.

## Known issues

- The template's `npm run shoot` cannot pass without GPU-backed headless Chrome; use
  `node scripts/verify.mjs` instead and say so in reports.
- The San Francisco template has two cosmetic gaps: the bridge's city end has no approach viaduct,
  and blocks whose streets failed to route stay empty.
- The template is derived work (see `README.md` provenance); third-party notices ship in the build.

## Continuity

- Published copy of this skill: <https://github.com/somphol/city-miniature> (public).
- Installed copy: `~/.config/opencode/skills/city-miniature` (globally available as `@city-miniature`).
- Session transcripts from the work that produced it are archived **locally only** in
  `~/opencode-transcripts`; they are deliberately not published.
