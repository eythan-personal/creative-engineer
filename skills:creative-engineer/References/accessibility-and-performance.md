# Accessibility & Performance

## Accessibility as Craft

The best creative developers treat accessibility as a design constraint that improves the work, not a checkbox.

- `prefers-reduced-motion` — Simplify or disable animations. GSAP's `matchMedia` handles this cleanly. Active Theory swaps hover video reels for stills when reduced motion is preferred.
- `prefers-color-scheme` — Support dark/light modes when appropriate.
- Semantic HTML — `<nav>`, `<main>`, `<section>`, `<article>`, `<aside>`, `<header>`, `<footer>`. Screen readers rely on these.
- Focus management — Visible, styled `:focus-visible` rings. Logical tab order. Motion's `whileFocus` follows `:focus-visible` semantics.
- Color contrast — WCAG AA minimum (4.5:1 for body text, 3:1 for large text). Creative palettes can still meet these thresholds.
- ARIA labels on interactive elements that lack visible text.
- Alt text on images. Decorative images get `alt=""` and `aria-hidden="true"`.
- Native scrollbar preserved. Lenis and Locomotive Scroll v5 both keep the real browser scrollbar. Never hide it without providing equivalent functionality.
- Keyboard navigation must work for all interactive elements. Every drag interaction should have a keyboard alternative.
- Touch targets minimum 44x44px on mobile.

## Performance Budgets

Creative sites CAN be fast. Active Theory achieves ~1.3s LCP on desktop with full WebGL. The tricks:

- **Code split** — Load 3D/heavy assets only when needed. Dynamic `import()`.
- **Compress everything** — Draco for 3D meshes, AVIF/WebP for images, gzip/brotli for text.
- **Lazy load below-fold** — Use Intersection Observer to load assets as they approach the viewport.
- **requestIdleCallback** for non-critical initialization.
- **Font loading strategy** — `font-display: swap` or `optional`. Preload critical fonts with `<link rel="preload">`.
- **Minimize main-thread work** — Offload heavy computation to Web Workers. Use `OffscreenCanvas` for WebGL when possible.
- **Profile relentlessly** — Chrome DevTools Performance tab. Target 60fps. Watch for layout thrash.
- **Limit scroll animations to major sections** — Animating every small element can slow down older devices and feel chaotic.
- **Test on mid-range phones** — If animations cause jank on a three-year-old Android, they're hurting more than helping.
