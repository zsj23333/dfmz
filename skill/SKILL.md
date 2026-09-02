---
name: immersive-threejs-site
description: "Generate cinematic, immersive Three.js scroll-driven websites with a single HTML file. Use when the user asks to create an immersive 3D website, a scroll-driven experience, a cinematic landing page, or a Three.js showcase for a landmark, city, or theme. Produces a complete, self-contained HTML file with procedural 3D scenes, post-processing effects, and smooth scroll animations."
---

# Immersive Three.js Site Generator

## Overview

Generate a complete, cinematic, scroll-driven Three.js website in a single HTML file. The site features:
- Procedural 3D scenes (no external images/videos)
- Smooth scroll-driven camera animations
- Post-processing effects (bloom, exposure, color grading, vignette, noise)
- Interactive UI elements (preloader, navigation, cards, progress rail)
- Fully responsive and accessible

## Workflow

### 1. Understand the Theme

Ask the user for:
- **Theme**: What landmark, city, or concept should the site be about?
- **Mood**: What atmosphere? (e.g., night, dawn, cyberpunk, romantic)
- **Color palette**: Any preferred colors? (default: dark night with accent colors)
- **Chapters**: How many chapters? (default: 5 chapters + hero + footer)

### 2. Generate the Site

Use the template in `assets/template/` as a starting point:

```bash
# Copy the template
cp -r assets/template/ my-site/
cd my-site
```

Then customize:
1. **HTML content**: Update title, meta, navigation, hero, chapters, cards, footer
2. **CSS variables**: Update color palette in `:root`
3. **Scene functions**: Rewrite `buildScene()` to match the theme
4. **Camera waypoints**: Update `WPS` and `WPT` for the new scene
5. **Card cameras**: Update `CARD_CAM` for card viewports

### 3. Test and Verify

1. Start a local server: `python -m http.server 8000`
2. Open `http://localhost:8000` in a browser
3. Check:
   - Preloader completes
   - Scene renders correctly
   - Scroll animations work
   - Cards update correctly
   - No console errors

### 4. Deploy

1. Push to GitHub
2. Enable GitHub Pages
3. Access via `https://<username>.github.io/<repo>/`

## Key Concepts

### Scene Structure

The scene is built procedurally using Three.js:
- **Sky**: A large sphere with a procedural sky texture
- **Ground**: A large plane with a procedural texture
- **Main subject**: The landmark or theme (e.g., tower, stadium, mountain)
- **Surroundings**: Secondary objects (e.g., water, buildings, trees)
- **Atmosphere**: Haze, particles, and lighting effects

### Camera Animation

The camera follows a Catmull-Rom spline path:
- **Waypoints**: Defined in `WPS` array (position, lookAt, FOV)
- **Timing**: Defined in `WPT` array (progress values)
- **Smoothing**: Uses `easeIO` for smooth transitions
- **Scroll**: Progress is driven by scroll position

### Post-Processing

The post-processing pipeline includes:
- **Bright pass**: Extract bright areas for bloom
- **Gaussian blur**: 4 levels of blur for bloom
- **Compose**: Combine scene with bloom, apply exposure, color grading, vignette, noise

### UI Elements

- **Preloader**: Shows loading progress
- **Navigation**: Fixed header with chapter links
- **Hero**: Full-screen intro with title and subtitle
- **Chapters**: Scrollable sections with content
- **Cards**: Interactive cards with live 3D previews
- **Progress rail**: Fixed right-side navigation

## Resources

### assets/template/

The complete template directory:
- `index.html`: The main HTML file (copy and customize)
- `runtime/three.min.js`: Three.js library
- `runtime/fonts.css`: Font definitions

### references/

Detailed reference documentation:
- `design-guide.md`: Design principles and best practices
- `scene-patterns.md`: Common scene patterns and techniques
- `common-pitfalls.md`: Common issues and solutions

## Common Pitfalls

See `references/common-pitfalls.md` for detailed solutions. Key issues:
1. **Chinese encoding**: Use Python for file operations, not PowerShell
2. **matCompose uniforms**: Must include `tB0`-`tB3` samplers
3. **Footer id**: Must have `id="foot"` for scroll tracking
4. **targetScroll**: Must be updated in scroll event listener
5. **Shot mode**: Must force reveal all `[data-rv]` elements
