# Design Guide

## Color Palette

The default color palette is a dark night theme with accent colors:

```css
:root {
  --ink: #04070d;          /* background */
  --ink-2: #070d16;        /* raised background */
  --bone: #dce5ea;         /* primary text */
  --bone-dim: #a3b0bb;     /* secondary text */
  --muted: #71808d;        /* muted text */
  --line: rgba(220,229,234,.13);  /* borders */
  --line-soft: rgba(220,229,234,.07);
  --rose: #ff3d7f;         /* primary accent */
  --ember: #ff9a4d;        /* secondary accent */
  --cyan: #67c6dd;         /* tertiary accent */
  --gold: #e8b45c;         /* highlight */
}
```

### Customizing Colors

1. **Primary accent**: Change `--rose` to match the theme
2. **Secondary accent**: Change `--ember` for warm tones
3. **Tertiary accent**: Change `--cyan` for cool tones
4. **Background**: Adjust `--ink` and `--ink-2` for mood

## Typography

The site uses two font families:
- **Onest**: Primary font for UI text
- **Wordmark**: Display font for large headings

Both are loaded from `runtime/fonts.css`.

### Font Sizes

- **Hero title**: `clamp(38px, 7.4vw, 124px)`
- **Section title**: `clamp(28px, 4.8vw, 72px)`
- **Body text**: `clamp(15px, 1.16vw, 19px)`
- **Small text**: `11px`

## Layout

### Grid System

The site uses a responsive grid:
- **Desktop**: 12-column grid
- **Tablet**: 8-column grid
- **Mobile**: 4-column grid

### Spacing

- **Padding**: `clamp(20px, 3.4vw, 56px)`
- **Gap**: `clamp(14px, 2.4vw, 40px)`
- **Section padding**: `clamp(88px, 15vh, 190px)`

## Animation

### Scroll Animation

The scroll animation uses:
- **Damping**: `damp(scroll, targetScroll, 5.0, dt)`
- **Easing**: `easeIO(sat(progress * 1.02 - 0.005))`
- **Camera**: Catmull-Rom spline interpolation

### UI Animation

- **Reveal**: `IntersectionObserver` with `data-rv` attribute
- **Hover**: CSS transitions with `cubic-bezier(.22,.61,.36,1)`
- **Preloader**: Linear progress bar

## Accessibility

- **Reduced motion**: `prefers-reduced-motion` media query
- **Keyboard navigation**: Tab order follows visual order
- **Screen reader**: Semantic HTML and ARIA labels
- **Color contrast**: Meets WCAG AA standards

## Performance

- **Texture generation**: All textures are generated procedurally
- **Geometry**: Optimized geometry with reasonable polygon counts
- **Post-processing**: 4-level bloom with adjustable resolution
- **Pixel ratio**: `Math.min(devicePixelRatio || 1, 2)`
