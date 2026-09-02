# PEARL — NIGHT OVER THE HUANGPU

> **在线体验：[https://zsj23333.github.io/dfmz/](https://zsj23333.github.io/dfmz/)**

A single-page, cinematic WebGL night crossing of the Huangpu toward the Oriental Pearl. A procedural Three.js scroll experience modeled on [kage](https://github.com/MengTo/kage): no external images or video — the tower, river, skyline, Bund, halos, and wordmark are all generated in code.

## Run

```bash
python -m http.server 8123 --bind 127.0.0.1
# then open http://127.0.0.1:8123/index.html
```

Opening `index.html` directly from the filesystem also works (all assets are local and relative), but a local server avoids any browser file-access quirks.

## Structure

```
index.html            single-file site (markup, CSS, scene code, post pipeline)
runtime/three.min.js  local three.js r1xx build
runtime/fonts.css     Onest family subfonts (base64, local)
PROMPT.md             the build prompt that generated this project
PROMPT.template.md    generic parameterized prompt derived from kage's PROMPT.md
```

## Chapters (camera path)

| # | Section | What you see |
|---|---------|--------------|
| 00 | The Crossing | hero over the water, the Pearl ahead |
| 01 | The Pearl | close to the water, looking up at the tower |
| 02 | The Skyline | pan to the three towers |
| 03 | The Bund | across the water, five-tower atlas |
| 04 | Afterglow | high above, descending |
| 05 | Footer | colophon over the night |

A single camera follows a Catmull-Rom path through six keyframed positions, so scrolling reads as one continuous dolly, not scene swaps.

## Scene (all procedural)

- **The Pearl** — a concrete needle, an antenna, three pink spheres (textured with a generated dot field), three struts, and additive halos.
- **The Huangpu** — a large dark water plane with vertical light streaks pooling the reflections of the Pearl and the towers.
- **The three towers** — Shanghai Tower (twisting spiral), Jin Mao (tiered pagoda), SWFC (bottle-opener with notch).
- **The Bund** — a low band of lit windows across the water.
- **The wordmark** — a giant extruded PEARL that anchors the hero.
- **Foregrounds** — canvas-generated reeds and boughs pinned to the bottom of the active section, fading and blurring on handoff.
- **Post** — 4-level Gaussian bloom, exposure, color temperature, vignette, grain, sRGB gamma.

## Controls & helpers

- Scroll to move through the chapters; nav / chapter chips / right rail jump to a section.
- The three tower cards are **live WebGL windows** (scissor-rendered sub-views), not images.
- Debug stills: `index.html?view=0` … `?view=5` freezes each chapter camera (no animation loop, handy for screenshots).
- Grade tuning: `?ex=1.3` exposure, `?bloom=1.1` bloom.

## Notes

- Palette: near-black, blue-charcoal, bone white, warm amber, pearl rose.
- Typography: Onest (local) for Latin, system CJK for the vertical Chinese accents.
- Reduced-motion and mobile (≈390×844) are supported; a custom cursor appears only on fine pointer devices.
