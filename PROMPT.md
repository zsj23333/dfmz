# Build prompt

Create a single-page, cinematic WebGL experience called **PEARL** — a five-chapter night crossing of the Huangpu, ending at the Oriental Pearl. The result should feel like an editorial art book moving through a live 3D city, not a conventional product landing page.

## Experience

- Use a fixed full-viewport Three.js canvas as the environmental layer.
- Build the Oriental Pearl tower, the river, the Pudong skyline, the Bund, light streaks, glow halos, drifting wisps, banks, and night atmosphere procedurally — no external images or video.
- Drive one continuous camera path from page scroll. Each section should feel like a new composed shot rather than a hard scene replacement.
- Add restrained bloom, film grain, vignette, depth haze, cold city light, warm reflection, and pink rose light on the Pearl.
- Keep the palette near-black, blue-charcoal, bone white, warm amber, and pearl rose.

## Scene

- The Oriental Pearl: a concrete needle, an antenna, three pink spheres of light (the largest lower sphere burning rose), three struts climbing to the lower sphere, and soft additive halos.
- The river: a large dark water plane in front of the tower, carrying vertical light streaks that pool the reflections of the Pearl and the towers.
- The skyline across the water: three parametric curtain-wall towers — Shanghai Tower as a twisting spiral, Jin Mao as a tiered glass pagoda, SWFC as a bottle-opener with its notch.
- The Bund: a low band of lit windows on the far bank and the Pudong silhouette on the other side, so the crossing reads left-to-right.
- A giant extruded wordmark in the 3D world (PEARL) that anchors the hero and drifts out of frame during later chapters.

## Layout

- Structure the page as a hero crossing, the Pearl chapter, the skyline chapter, the Bund atlas, an afterglow closing, and a manifesto footer.
- Use oversized left-aligned English headings, vertical Chinese display type on the right edge, small technical labels, chapter numbers, fine rules, and generous negative space.
- Show live WebGL windows inside editorial cards: each tower card is a real-time scissor-rendered view of the 3D tower, and the hero carries one floating preview window.
- Layer generated canvas cutouts of reeds and boughs at the bottom of the active viewport as foregrounds that arrive pinned while their section is active, then fade and blur away during the handoff.

## Motion

- Reveal headings word by word and supporting elements individually.
- Use slow, precise section transitions, subtle parallax, an eased Catmull-Rom camera between six keyframed positions, and a gentle sway on the tower and foregrounds.
- Let the navigation, chapter chips, right rail, cards, and foreground layers respond to the active section.
- Include reduced-motion behavior that preserves the complete reading experience.

## Interaction and quality

- Use a custom cursor only for fine pointer devices.
- Provide working anchor navigation, mobile navigation, responsive layouts, semantic landmarks, and accessible labels.
- Keep runtime assets local and use relative paths so the site works under a GitHub Pages repository subpath.
- Avoid frameworks, build tooling, analytics, trackers, remote fonts, placeholder imagery, generic glassmorphism, and decorative motion without narrative purpose.
- Include a preloader with a progress bar and a shot-mode debug helper (?view=0..5 to freeze each chapter camera, ?ex / ?bloom to tune the grade) so every chapter can be reviewed as a still.
- Verify at desktop and approximately 390 × 844, check all assets for 404s, parse every inline script, inspect the browser console, and test one complete scroll/navigation interaction before shipping.
