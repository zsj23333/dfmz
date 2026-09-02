# Build prompt — {{PROJECT_NAME}}

Create a single-page, cinematic WebGL experience called **{{PROJECT_NAME}}**: a {{CHAPTER_COUNT}}-chapter {{JOURNEY_DESCRIPTION}} through {{SETTING}}. The result should feel like an editorial art book moving through a live 3D world, not a conventional product landing page.

> How to use this template: replace every `{{PLACEHOLDER}}` below, then delete this block and the placeholder comments. Keep the structure and the quality bars — they are the reusable parts. A worked example lives in `PROMPT.md` (the Oriental Pearl project).

## Experience

- Use a fixed full-viewport Three.js canvas as the environmental layer.
- Build {{SCENE_ELEMENTS}} procedurally — no external images or video unless the prompt explicitly allows them.
- Drive one continuous camera path from page scroll. Each section should feel like a new composed shot rather than a hard scene replacement.
- Add restrained bloom, film grain, vignette, depth haze, {{PRIMARY_LIGHT}}, and {{ACCENT_LIGHT}}.
- Keep the palette {{PALETTE}}.

## Scene

- {{HERO_SUBJECT}}: the central landmark or world piece that anchors the hero and repeats across chapters.
- {{ENVIRONMENT}}: the ground / water / sky system and the atmospheric layer that fills the space between camera and subject.
- {{SUPPORTING_SET}}: secondary objects or a built environment that give the world scale and depth.
- {{AMBIENT_EFFECTS}}: particles, light streaks, halos, fog, or drifting elements that make the scene feel alive.
- A giant extruded wordmark ({{WORDMARK_TEXT}}) in the 3D world that anchors the hero and drifts out of frame during later chapters.

## Layout

- Structure the page as a hero, {{CHAPTER_NAMES}}, a closing, and a manifesto footer.
- Use oversized left-aligned English headings, large vertical {{VERTICAL_TYPE_LANGUAGE}} display type, small technical labels, chapter numbers, fine rules, and generous negative space.
- Layer {{FOREGROUND_CUTOUTS}} at the bottom of the active viewport as foregrounds that arrive pinned while their section is active, then fade and blur away during the handoff.
- Optionally show live WebGL windows inside editorial cards: each card is a real-time scissor-rendered view of a scene subject, and the hero carries one floating preview window.
- Center any play icon within the image frame itself, excluding the caption area.

## Motion

- Reveal headings word by word and supporting elements individually.
- Use slow, precise section transitions, subtle parallax, an eased {{CAMERA_CURVE}} camera between {{KEYFRAME_COUNT}} keyframed positions, and a gentle sway on the subject and foregrounds.
- Let the navigation, chapter {{CHAPTER_NAV_STYLE}}, right rail, cards, and foreground layers respond to the active section.
- Include reduced-motion behavior that preserves the complete reading experience.

## Interaction and quality

- Use a custom cursor only for fine pointer devices.
- Provide working anchor navigation, mobile navigation, responsive layouts, semantic landmarks, and accessible labels.
- Keep runtime assets local and use relative paths so the site works under a GitHub Pages repository subpath.
- Avoid frameworks, build tooling, analytics, trackers, remote fonts, placeholder imagery, generic glassmorphism, and decorative motion without narrative purpose.
- Include a preloader with a progress bar and a shot-mode debug helper (e.g. `?view=0..N` to freeze each chapter camera, `?ex` / `?bloom` to tune the grade) so every chapter can be reviewed as a still.
- Verify at desktop and approximately 390 × 844, check all assets for 404s, parse every inline script, inspect the browser console, and test one complete scroll/navigation interaction before shipping.

---

## Placeholder cheat sheet

| Placeholder | Example (Oriental Pearl) |
|---|---|
| `{{PROJECT_NAME}}` | PEARL |
| `{{CHAPTER_COUNT}}` / `{{JOURNEY_DESCRIPTION}}` / `{{SETTING}}` | five-chapter / night crossing / the Huangpu toward the Oriental Pearl |
| `{{SCENE_ELEMENTS}}` | the tower, the river, the skyline, the Bund, light streaks, halos, wisps, banks, atmosphere |
| `{{PRIMARY_LIGHT}}` / `{{ACCENT_LIGHT}}` | cold city light, warm amber reflection / pink rose light on the Pearl |
| `{{PALETTE}}` | near-black, blue-charcoal, bone white, warm amber, pearl rose |
| `{{HERO_SUBJECT}}` | the Oriental Pearl: a concrete needle, three pink spheres, struts, additive halos |
| `{{ENVIRONMENT}}` | the Huangpu: a dark water plane with vertical light streaks |
| `{{SUPPORTING_SET}}` | three parametric towers — spiral, pagoda, bottle-opener — plus a lit Bund |
| `{{AMBIENT_EFFECTS}}` | glow halos, drifting wisps, night atmosphere |
| `{{WORDMARK_TEXT}}` | PEARL |
| `{{CHAPTER_NAMES}}` | the Pearl / the Skyline / the Bund / Afterglow |
| `{{VERTICAL_TYPE_LANGUAGE}}` | Chinese (东方明珠) |
| `{{FOREGROUND_CUTOUTS}}` | canvas-generated reeds and boughs |
| `{{CAMERA_CURVE}}` / `{{KEYFRAME_COUNT}}` | Catmull-Rom / 6 |
| `{{CHAPTER_NAV_STYLE}}` | chips |
