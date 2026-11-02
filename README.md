# City Miniature — an OpenCode skill

Build an interactive 3D miniature of a city as **one self-contained HTML file**: a street grid,
dedicated landmark models, traffic and boats, day/night lighting, and a landmark bar with camera
flights. Ships with a working San Francisco diorama as the template.

![San Francisco diorama](skills/city-miniature/docs/preview.png)

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
node scripts/new-project.mjs --out ~/my-miniature
cd ~/my-miniature
npm ci
npm run dev            # live editing
npm run build:single   # -> dist-single/index.html
node tests/run.mjs     # geometry, traffic, diversity, planning
node scripts/verify.mjs # driven interactions, frame-rate independent
```

`npm run shoot` is the deeper visual harness; it needs GPU-backed headless Chrome.

## What it produces

`dist-single/index.html` — roughly 1 MB, no external scripts, fonts, images or network calls. It runs
from disk, from a static host, or on GitHub Pages, and embeds in a 345×345 iframe.

The template's city, San Francisco, has eight landmarks (Golden Gate Bridge, Transamerica Pyramid,
Salesforce Tower, Ferry Building, Coit Tower, Painted Ladies, City Hall, Alcatraz), a rotated
downtown grid with Market Street cutting across it, Golden Gate Park, the Presidio, bay piers and
~200 street parcels.

## Repository layout

```text
skills/city-miniature/
├── SKILL.md                     workflow, module map, adaptation recipes
├── ATTRIBUTION.md               origin, reused components, licence status
├── assets/san-francisco-diorama the working template (source, 45 files)
├── results/…/index.html         the published single-file build
├── references/                  method, lessons, verification, hosting, build log
├── scripts/new-project.mjs      scaffold a project from the template
└── docs/preview.png             screenshot of this build
```

## Adapting it to another city

Change the outline, the street frame, the landmark anchors and their models, the camera views and
the copy **together** — a new city with old coordinates reads as a reskin. `references/method.md`
lists the invariants; `references/build-log.md` records the dead ends so you do not repeat them.

## Attribution

The template derives from the **Manhattan Miniature 0.2.0** sample by **SandBase Lab**
(<https://www.sandbase.ai>). What was reused, what is new, and the licence status are documented in
[ATTRIBUTION.md](ATTRIBUTION.md). The original archive carried no licence for the sample itself, so
attribution is given but redistribution terms should be confirmed with the author. The original
brand mark is not redistributed: the fork uses a neutral identity.
