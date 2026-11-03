# Agent notes — city-miniature

An OpenCode skill that builds a single-file 3D city diorama **from scratch** from a city brief and a
blank starter. The San Francisco asset is a mechanism reference, not a template to copy. Read
`skills/city-miniature/SKILL.md` first; this file is the handoff for whoever works on the skill.

## Commands

```sh
# scaffold a blank starter (no scene code is copied)
cd skills/city-miniature
node scripts/new-project.mjs --out /tmp/try-city
cd /tmp/try-city && npm install && npm run build

# validate the skill before publishing
node ~/.config/opencode/skills/skill-publish/scripts/check-skill.mjs \
  /Users/somphol/Projects/city-miniature/skills/city-miniature

# sync the published source into the installed copy
rsync -a --delete --exclude docs skills/city-miniature/ \
  ~/.config/opencode/skills/city-miniature/
```

The reference asset still has its own commands (`npm ci`, `npm run build:single`, `node tests/run.mjs`,
`node scripts/verify.mjs`) if you need to inspect the mechanism. Those are not the starter's
commands.

## Architecture

The skill is a workflow plus a reference implementation. Nothing executes at skill load time.

- `skills/city-miniature/SKILL.md` — the model-facing instructions: the from-scratch rule, the
  workflow, the target module map and the definition of done.
- `skills/city-miniature/references/city-brief.md` — the design contract to fill as `CITY.md`.
- `skills/city-miniature/references/method.md` — from-scratch order, invariants, reference pattern.
- `skills/city-miniature/references/lessons.md` — reskin failure and technical regressions.
- `skills/city-miniature/references/build-log.md` — Bangkok from-scratch case study + SF log.
- `skills/city-miniature/references/verification.md` — tests, capture API, headless checks.
- `skills/city-miniature/references/hosting.md` — single-file build, CSP, Pages, handshake.
- `skills/city-miniature/scripts/new-project.mjs` — the only skill-level executable; it writes a
  blank starter and copies no scene content.
- `skills/city-miniature/assets/san-francisco-diorama/` — the reference implementation. Read it for
  the mechanism; do not copy its source, geography, landmarks, copy or tests.
- `skills/city-miniature/results/` — the reference build, for inspecting the intended output.
- `ATTRIBUTION.md` — origin and licence status of the derived reference. Keep it accurate.

## Constraints

- **Do not copy an existing miniature and adjust a few coordinates.** A reskin inherits the old
  city's geography, street logic, landmarks, palette, transport, copy and tests. The Bangkok build
  started that way and was rejected; the from-scratch rebuild is the model.
- The starter must remain blank: no San Francisco scene code, coordinates, street names, landmark
  ids, strings or test targets.
- The target's geography, plan, landmarks, buildings, transport, palette, copy and verification
  targets are authored together.
- The published artifact must stay a **single self-contained HTML file** under a strict CSP: no
  fetch, no fonts, no image URLs, no storage. Anything that adds a network request breaks the premise.
- `SKILL.md` is read by a model, not a parser: keep it short, concrete and free of hedging.
- The skill must stay at `skills/<id>/SKILL.md`; the directory name is the ID OpenCode loads.
- The installed copy at `~/.config/opencode/skills/city-miniature` must be re-synced after edits
  here, or the skill will describe a newer workflow than it ships.
- `ATTRIBUTION.md` must stay in sync with the code: if reused components change, update it.
- Do not restore the original author's brand mark or wordmark; the fork uses a neutral identity.

## Known issues

- The San Francisco reference has two cosmetic gaps: the bridge's city end has no approach viaduct,
  and blocks whose streets failed to route stay empty.
- `npm run shoot` cannot pass without GPU-backed headless Chrome; use the virtual-time verify check.
- The blank starter deliberately has no test, verify or single-file scripts. The agent adds them for
  the target city; the references show the patterns.
- The reference asset is derived work (see `README.md` provenance); third-party notices ship in its
  build.

## Continuity

- Published skill repo: <https://github.com/somphol/city-miniature> (public).
- Catalog: <https://somphol.github.io/opencode-skills/> (source repo
  <https://github.com/somphol/opencode-skills>).
- Catalog source path: `~/Projects/city-miniature/skills/city-miniature`.
- Installed copy: `~/.config/opencode/skills/city-miniature`.
- From-scratch example: <https://github.com/somphol/bangkok-miniature> and
  <https://somphol.github.io/bangkok-miniature/>.
- Session transcripts from the work that produced it are archived **locally only** in
  `~/opencode-transcripts`; they are deliberately not published.
