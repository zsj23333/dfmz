# Common Pitfalls

## 1. Chinese Encoding

**Problem**: PowerShell uses GBK encoding by default, which can corrupt UTF-8 files containing Chinese characters.

**Solution**: Always use Python for file operations involving Chinese text:

```python
# Correct
html = open('index.html', encoding='utf-8').read()
open('index.html', 'w', encoding='utf-8').write(html)

# Wrong (PowerShell)
# Get-Content -Path index.html  # May corrupt Chinese characters
```

## 2. matCompose Uniforms

**Problem**: The `matCompose` shader material requires `tB0`-`tB3` samplers for bloom. Missing these will cause rendering errors.

**Solution**: Ensure all uniforms are defined:

```javascript
POST.matCompose = mk(
  'uniform sampler2D tDiffuse,tB0,tB1,tB2,tB3; ...',
  { tB0: { value: null }, tB1: { value: null }, tB2: { value: null }, tB3: { value: null },
    w0: { value: 1 }, w1: { value: .72 }, w2: { value: .5 }, w3: { value: .34 },
    exposure: { value: qn('ex', 1.26) }, bloom: { value: qn('bloom', 1.0) }, time: { value: 0 } });
```

## 3. Footer ID

**Problem**: The footer must have `id="foot"` for scroll tracking to work correctly.

**Solution**: Ensure the footer element has the correct ID:

```html
<footer class="foot" id="foot" data-cam="5">
  ...
</footer>
```

## 4. targetScroll Update

**Problem**: The `targetScroll` variable must be updated in the scroll event listener. If it's only updated in shot mode, the camera won't move during normal scrolling.

**Solution**: Update `targetScroll` in the scroll event listener:

```javascript
window.addEventListener('scroll', () => {
  targetScroll = window.pageYOffset;
}, { passive: true });
```

## 5. Shot Mode Reveal

**Problem**: In shot mode (debug mode), all `[data-rv]` elements must be revealed immediately.

**Solution**: Force reveal all elements in shot mode:

```javascript
if (Q.has('shot') || Q.has('view')) {
  document.querySelectorAll('[data-rv]').forEach(el => el.classList.add('rv-in'));
}
```

## 6. Canvas Context Conflict

**Problem**: "Canvas has an existing context of a different type" error occurs when the canvas already has a different type of context.

**Solution**: Ensure no other code is creating a different context on the same canvas. If refreshing the page doesn't help, try closing all tabs and opening a new one.

## 7. Texture Generation

**Problem**: Procedural textures can be slow to generate, causing the preloader to take a long time.

**Solution**: Optimize texture generation:
- Use smaller texture sizes (512x512 instead of 2048x2048)
- Reduce the number of noise points
- Use `requestAnimationFrame` for async generation

## 8. Camera Path

**Problem**: The camera path may not look correct if the waypoints are not properly positioned.

**Solution**: Test the camera path with debug mode:
- Use `?view=0` to freeze the frame at waypoint 0
- Adjust waypoint positions until the path looks correct

## 9. Card Viewports

**Problem**: Card viewports may not render correctly if the camera positions are not properly set.

**Solution**: Ensure `CARD_CAM` has the correct number of cameras:

```javascript
const CARD_CAM = [
  { p: [x, y, z], f: [x, y, z], fov: 26 },
  { p: [x, y, z], f: [x, y, z], fov: 26 },
  { p: [x, y, z], f: [x, y, z], fov: 26 }
];
```

## 10. Responsive Design

**Problem**: The site may not look correct on different screen sizes.

**Solution**: Use responsive units:
- `clamp()` for font sizes and spacing
- `vw` and `vh` for viewport-relative units
- Media queries for different breakpoints

## 11. Performance

**Problem**: The site may run slowly on low-end devices.

**Solution**: Optimize performance:
- Reduce pixel ratio: `Math.min(devicePixelRatio || 1, 1.6)`
- Reduce bloom resolution
- Use simpler geometry
- Reduce the number of particles

## 12. Accessibility

**Problem**: The site may not be accessible to users with disabilities.

**Solution**: Ensure accessibility:
- Use `prefers-reduced-motion` media query
- Add ARIA labels to interactive elements
- Ensure color contrast meets WCAG AA standards
- Use semantic HTML elements
