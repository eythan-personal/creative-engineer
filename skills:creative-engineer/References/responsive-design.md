# Responsive Design

## Strategy

**Mobile-first is the default.** Start with the smallest viewport and layer on complexity. This forces you to prioritize content and prevents desktop-first designs from becoming cramped afterthoughts on mobile.

Exception: if the project is desktop-only (dashboards, internal tools, WebGL experiences), start at the primary viewport and scale down only where needed.

## Breakpoints

Don't pick arbitrary pixel values. Design to where the layout breaks, not to specific devices. That said, these ranges cover the vast majority of real-world viewports:

```css
/* Mobile-first base styles — no media query needed */

/* Tablet landscape / small desktop */
@media (min-width: 768px) { }

/* Desktop */
@media (min-width: 1024px) { }

/* Wide desktop */
@media (min-width: 1440px) { }

/* Ultra-wide — cap content width here */
@media (min-width: 1920px) { }
```

Use `min-width` for mobile-first (adding complexity up). Use `max-width` only when overriding a desktop default down — avoid mixing the two directions in the same project.

## Fluid Typography

`clamp()` eliminates most typographic breakpoints. The font scales smoothly between a minimum and maximum based on viewport width:

```css
h1 { font-size: clamp(2.5rem, 5vw + 1rem, 6rem); }
h2 { font-size: clamp(1.75rem, 3vw + 0.5rem, 3.5rem); }
h3 { font-size: clamp(1.25rem, 2vw + 0.5rem, 2rem); }
body { font-size: clamp(1rem, 0.5vw + 0.875rem, 1.25rem); }
```

The middle value (`5vw + 1rem`) controls the rate of scaling. Adding a `rem` value ensures the font never collapses to zero on very small viewports.

## Fluid Spacing

Apply the same `clamp()` principle to padding and gaps:

```css
:root {
  --space-xs: clamp(0.5rem, 1vw, 0.75rem);
  --space-sm: clamp(0.75rem, 2vw, 1.5rem);
  --space-md: clamp(1.5rem, 4vw, 3rem);
  --space-lg: clamp(3rem, 8vw, 6rem);
  --space-xl: clamp(5rem, 12vw, 10rem);
}

.hero { padding-block: var(--space-xl); }
.section { padding-block: var(--space-lg); }
.card { padding: var(--space-md); }
```

This replaces the need for spacing overrides at every breakpoint.

## Layout Adaptation

### Grid collapse pattern
The most common responsive pattern — a multi-column grid that stacks on mobile:

```css
.grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(min(100%, 320px), 1fr));
  gap: var(--space-md);
}
```

`auto-fit` + `minmax` handles the breakpoint automatically. No media query needed.

### Sidebar layout
A sidebar that collapses below the main content on small screens:

```css
.layout {
  display: grid;
  grid-template-columns: 1fr;
  gap: var(--space-md);
}

@media (min-width: 768px) {
  .layout {
    grid-template-columns: 280px 1fr;
  }
}
```

### Container queries
When a component's layout should respond to its container, not the viewport:

```css
.card-container {
  container-type: inline-size;
}

@container (min-width: 400px) {
  .card {
    flex-direction: row;
  }
}
```

Use container queries for reusable components that live in different contexts. Use media queries for page-level layout decisions.

## Content Width

Never let content run edge-to-edge on wide screens. Cap readable content:

```css
.content {
  width: min(100% - 2rem, 1200px);
  margin-inline: auto;
}

/* Full-bleed sections that still constrain inner content */
.full-bleed {
  width: 100%;
}
.full-bleed > .inner {
  width: min(100% - 2rem, 1200px);
  margin-inline: auto;
}
```

Body text specifically should never exceed `65ch` for readability:

```css
.prose {
  max-width: 65ch;
}
```

## Responsive Images

```html
<picture>
  <source srcset="hero-wide.avif" media="(min-width: 1024px)" type="image/avif">
  <source srcset="hero-wide.webp" media="(min-width: 1024px)" type="image/webp">
  <source srcset="hero-mobile.avif" type="image/avif">
  <source srcset="hero-mobile.webp" type="image/webp">
  <img src="hero-mobile.jpg" alt="..." loading="lazy" decoding="async">
</picture>
```

For inline images where art direction isn't needed, `srcset` with width descriptors is simpler:

```html
<img
  srcset="photo-400.webp 400w, photo-800.webp 800w, photo-1200.webp 1200w"
  sizes="(min-width: 1024px) 50vw, 100vw"
  src="photo-800.webp"
  alt="..."
  loading="lazy"
  decoding="async"
>
```

Use `object-fit: cover` with a defined aspect ratio to prevent layout shift:

```css
.image-container {
  aspect-ratio: 16 / 9;
  overflow: hidden;
}
.image-container img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}
```

## Mobile-Specific Concerns

- **Touch targets:** Minimum 44x44px. Generous padding on links and buttons — the tap area should be larger than the visual element.
- **Hover states don't exist on touch.** Never hide content or functionality behind hover. Use hover as progressive enhancement, not a requirement.
- **Viewport meta tag:** Always include `<meta name="viewport" content="width=device-width, initial-scale=1">`. Without it, mobile browsers render at desktop width and zoom out.
- **Scroll hijacking caution:** Smooth scroll libraries and scroll-driven animations that feel cinematic on desktop can feel sluggish or broken on mobile. Test on real devices and consider disabling heavy scroll effects below tablet breakpoints.
- **Fixed/sticky elements:** Large fixed headers or persistent CTAs eat into limited mobile viewport space. Keep them minimal or auto-hide on scroll.
- **Form inputs:** Use appropriate `type` attributes (`email`, `tel`, `url`) to trigger the right mobile keyboard. Avoid custom dropdowns that fight native mobile select behavior.

## Testing

- Chrome DevTools device mode is a starting point, not a substitute for real devices.
- Test on a mid-range Android phone (not just iPhone). If it works on a three-year-old Android, it works everywhere.
- Check landscape orientation on phones — layouts that assume portrait can break badly.
- Test with dynamic viewport units (`dvh`) if using viewport-height layouts, as mobile browser chrome (address bar, toolbar) changes the available height.
