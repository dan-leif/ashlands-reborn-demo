# CLAUDE.md — ashlands-reborn-demo

## Project Overview

Static showcase website for the **Ashlands Reborn** Valheim mod. The mod visually transforms the Ashlands biome into a Meadows-like aesthetic (green grass, normal trees, calm weather) without changing gameplay.

The site uses a before/after image slider so visitors can drag a vertical bar to compare vanilla Valheim vs. the mod. No framework, no build step — pure HTML/CSS/JS, hosted on GitHub Pages.

- **Live URL:** https://dan-leif.github.io/ashlands-reborn-demo/
- **Repo:** https://github.com/dan-leif/ashlands-reborn-demo
- **GitHub account:** dan-leif

## Structure

```
ashlands-reborn-demo/
  index.html        # entire site — HTML, CSS, and JS in one file
  photos/           # before/after screenshot pairs
    ruins_1_a.jpg       # vanilla
    ruins_1_b.jpg       # reborn
    valkyrie_1_a.jpg    # vanilla
    valkyrie_1_b.jpg    # reborn
    valkyrie_2_a.jpg    # vanilla
    valkyrie_2_b.jpg    # reborn
  .gitignore
  CLAUDE.md
```

## Photo Naming Convention

`{scene}_{index}_{variant}.jpg`
- `a` = vanilla (mod off)
- `b` = reborn (mod on)

To add a new scene, add a pair of photos following this convention and add an entry to the `scenes` array in `index.html`.

## Scenes (defined in index.html JS)

```js
const scenes = [
  { id: 'ruins_1',    caption: 'Ancient Ruins',              before: 'photos/ruins_1_a.jpg',    after: 'photos/ruins_1_b.jpg' },
  { id: 'valkyrie_1', caption: 'Fallen Valkyrie',            before: 'photos/valkyrie_1_a.jpg', after: 'photos/valkyrie_1_b.jpg' },
  { id: 'valkyrie_2', caption: 'Fallen Valkyrie (Close-up)', before: 'photos/valkyrie_2_a.jpg', after: 'photos/valkyrie_2_b.jpg' },
];
```

## Design

- **Aesthetic:** Dark fantasy — near-black background, ember/gold accents, green for "Reborn" label
- **Fonts:** Cinzel (headings/labels) + EB Garamond (body) via Google Fonts
- **Color tokens** (CSS vars in `:root`):
  - `--char` `#0e0c09` — page background
  - `--ember` `#c8843a` — gold accent (drag handle, active thumb border)
  - `--meadow` `#6daa4a` — green accent (Reborn label)
  - `--bone` `#d4c9a8` — primary text
- **Slider:** vanilla image sits behind, reborn image is clipped by `afterWrap` div whose width tracks drag position. Drag handle is absolutely positioned to match.
- **Navigation:** Prev/Next buttons + thumbnail strip. Thumbnails show the "reborn" (b) image.
- **Mobile:** touch events handled; responsive font sizes via `clamp()`; thumbnail/knob sizes shrink at ≤600px.

## Deployment

Push to `master` — GitHub Pages serves directly from the root of that branch. No CI, no build step needed.

```bash
git add .
git commit -m "your message"
git push
```

Changes are live within ~30 seconds after push (subsequent deploys are faster than the first).

## Mod Context (for writing copy or captions)

The **Ashlands Reborn** mod (BepInEx plugin for Valheim, Steam App 892970):
- Replaces Ashlands biome weather with clear skies
- Rewrites terrain vertex colors to look like Meadows
- Replaces Ashlands tree spawns with Beech/Oak trees
- Visually retextures/re-equips Charred Warrior creatures with custom armor (SouthsilArmor mod)
- Replaces Fallen Valkyrie with a standard Valkyrie mesh/animations
- All visual — no gameplay changes
- Plugin GUID: `com.ashlandsreborn.weather`
- Required companion mods: BepInExPack, ConfigurationManager, SouthsilArmor
