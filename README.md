# City Miniature — an OpenCode skill

Build an interactive 3D miniature of a city **from scratch** as one self-contained HTML file:
city-specific geography, landmarks, traffic, day/night lighting and bilingual UI. Existing
miniatures are **mechanism references only** — never copy a scene and reskin it.

The skill ships a blank, city-agnostic starter and a design brief. The working San Francisco
diorama is included as a reference implementation; the public Bangkok miniature is the from-scratch
case study.

### Reference implementation

[San Francisco](https://somphol.github.io/san-francisco-miniature/) — the mechanism reference:
rotated grid, Market Street, eight SF landmarks, Golden Gate Park, bay piers.

### From-scratch example

[Bangkok](https://somphol.github.io/bangkok-miniature/) — the Chao Phraya, two banks, eight Bangkok
landmarks, tuk-tuks, long-tail boats and English/Thai copy. It started as a rejected reskin and was
rebuilt from scratch.

![San Francisco reference implementation](skills/city-miniature/docs/preview.png)

## Install

The skill lives at [`skills/city-miniature`](skills/city-miniature) — the directory name is the skill
ID. Copy it into OpenCode's skills directory:

```sh
git clone --depth 1 https://github.com/somphol/city-miniature.git /tmp/city-miniature
cp -R /tmp/city-miniature/skills/city-miniature ~/.config/opencode/skills/
rm -rf /tmp/city-miniature
```

Or point a config at the checkout:

```jsonc title="opencode.jsonc"
{
  "$schema": "https://opencode.ai/config.json",
  "skills": ["~/Projects/city-miniature/skills"]
}
```

It is also published as an HTTP catalog — add one URL and OpenCode fetches it:

```jsonc
{ "skills": ["https://somphol.github.io/opencode-skills/"] }
```

## Use

```sh
cd ~/.config/opencode/skills/city-miniature
node scripts/new-project.mjs --out ~/my-city
cd ~/my-city
npm install
npm run dev
```

Then:

1. Fill `CITY.md` — geography, districts, 6–8 landmarks, street pattern, architecture, transport,
   palette, copy and verification targets.
2. Read `references/city-brief.md`, `method.md`, `lessons.md`, `verification.md` and `hosting.md`.
3. Author the target city's geography, plan, buildings, landmarks, environment, traffic and copy
   from scratch.
4. Add the target's plan/geometry tests, browser checks and single-file build.
5. Review the day/night overview and every landmark image before publishing.

The blank starter has no scene code. That is deliberate: the city's geography and landmarks drive
the plan, not the other way around. Do not copy the San Francisco asset.

## Why from scratch

A copied scene inherits the old city's outline, grid, landmark spacing, street names, building
palette, copy and tests. It reads as the old city with new labels, and fixing it costs more than
starting clean. The Bangkok build is the evidence: the first attempt was a copied SF scaffold and
was rejected; the from-scratch rebuild produced a cleaner, more accurate river city. The full case
study is in
[`skills/city-miniature/references/build-log.md`](skills/city-miniature/references/build-log.md).

## What it produces

A city-specific single-file build, typically 0.5–1.5 MB, with no external scripts, fonts, images or
network calls. It runs from disk, from a static host or GitHub Pages, and embeds in a 345×345
iframe. The reference build is
[`skills/city-miniature/results/san-francisco-diorama/index.html`](skills/city-miniature/results/san-francisco-diorama/index.html).

## Repository layout

```text
skills/city-miniature/
├── SKILL.md                     the model-facing workflow and the from-scratch rule
├── ATTRIBUTION.md               origin, reused mechanism, licence status
├── references/
│   ├── city-brief.md            the design contract to fill before coding
│   ├── method.md                from-scratch order and invariants
│   ├── lessons.md               reskin failure and technical regressions
│   ├── verification.md          tests, capture API, headless checks
│   ├── hosting.md               single-file build, CSP, Pages, handshake
│   └── build-log.md             Bangkok from-scratch case study + SF reference
├── scripts/new-project.mjs      blank, city-agnostic starter (no scene code)
├── assets/san-francisco-diorama the reference implementation, not a template
├── results/…/index.html         the reference single-file build
└── docs/preview.png             reference screenshot
```

## Attribution

The San Francisco reference derives from the **Manhattan Miniature 0.2.0** sample by **SandBase
Lab** (<https://www.sandbase.ai>). What was reused, what is new, the licence status and the
from-scratch practice are documented in [ATTRIBUTION.md](ATTRIBUTION.md). The original archive
carried no licence for the sample itself, so attribution is given but redistribution terms should be
confirmed with the author. The original brand mark is not redistributed.

The blank starter and the new documentation are original to this skill.
