# Micro-Interactions & Polish Details

The details that compound into a great interface. Users don't consciously notice these — they just feel that the interface is better. As one design engineer at a top product studio put it: "Every single interface has infinite opportunity for polish and delight."

## Interaction Patterns

- **Custom cursor** — Replace the default cursor with a dot, crosshair, or branded element. Scale it on hover over interactive elements. `mix-blend-mode: difference` or `exclusion` creates auto-contrast against any background.
- **Cursor trail** — A series of fading dots or shapes that follow the cursor with decreasing opacity. Use requestAnimationFrame and an array of positions.
- **Cursor-reactive distortion** — WebGL shader effects that distort content based on cursor position. The cursor becomes a tool for exploration, revealing hidden depth effects.
- **Magnetic buttons** — Buttons that subtly pull toward the cursor as it approaches. Calculate distance on `mousemove`, apply transform with lerp (linear interpolation) for smooth following.
- **Hover image reveals** — Images that appear on hover over text links, following the cursor. A signature Awwwards pattern. Use absolute positioning + pointer events none on the image.
- **Contextual icon animation** — When swapping icons (copy → check), animate with `opacity`, `scale`, and `blur` rather than instant swap. Use exactly: `scale: 0.25 → 1`, `opacity: 0 → 1`, `blur: 4px → 0px`, with `bounce: 0`.
- **Smooth state transitions** — Never let anything appear or disappear instantly. Everything enters and exits with intention.
- **Loading states** — Skeleton screens, progress bars, or creative loading animations instead of spinners.
- **Scroll progress indicators** — A thin bar at the top of the viewport or a subtle page progress element.

### Icon Animation Code

**Motion (Framer Motion):**
```tsx
<AnimatePresence mode="popLayout" initial={false}>
  <motion.span
    key={isActive ? "active" : "inactive"}
    initial={{ opacity: 0, scale: 0.25, filter: "blur(4px)" }}
    animate={{ opacity: 1, scale: 1, filter: "blur(0px)" }}
    exit={{ opacity: 0, scale: 0.25, filter: "blur(4px)" }}
    transition={{ type: "spring", duration: 0.3, bounce: 0 }}
  >
    <Icon />
  </motion.span>
</AnimatePresence>
```

**CSS (no Motion dependency) — keep both icons in DOM, cross-fade:**
```css
.icon-swap {
  position: relative;
}
.icon-swap .icon-enter {
  position: absolute;
  inset: 0;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: opacity 300ms, scale 300ms, filter 300ms;
  transition-timing-function: cubic-bezier(0.2, 0, 0, 1);
}
.icon-swap .icon-enter[data-active="false"] {
  scale: 0.25;
  opacity: 0;
  filter: blur(4px);
}
.icon-swap .icon-enter[data-active="true"] {
  scale: 1;
  opacity: 1;
  filter: blur(0);
}
```

Use `initial={false}` on `AnimatePresence` to prevent the icon from animating on first page load — only on subsequent state changes.

## The Magic of Clip-Path

`clip-path` is one of the most underrated CSS properties in creative frontend development. It enables:

- **Shape-based reveals** — Animate `clip-path: inset()` from `inset(100% 0 0 0)` to `inset(0)` for a wipe reveal. Use `circle()` for radial reveals from a click point.
- **Non-rectangular layouts** — Elements that aren't boxes. Diagonal sections, curved edges, organic shapes.
- **Image wipes on scroll** — Scroll-driven `clip-path` transitions that progressively reveal images.
- **Hover reveals** — Button hover effects where color fills from a corner or edge using animated `clip-path`.
- **Video masks** — Video content revealed through text shapes or custom paths. `clip-path` on a video element creates dramatic masking effects.

```css
.reveal {
  clip-path: inset(0 100% 0 0);
  transition: clip-path 0.8s cubic-bezier(0.16, 1, 0.3, 1);
}
.reveal.visible {
  clip-path: inset(0 0 0 0);
}
```

## Visual Refinement Details

- **Concentric border radius** — When nesting rounded elements, the outer radius MUST equal the inner radius plus the padding. `outer = inner + padding`. If inner is 12px and padding is 8px, outer is 20px. Mismatched radii are one of the most common unpolished-UI tells.

- **Optical alignment over geometric alignment** — When a button has text + icon, use slightly less padding on the icon side to optically center the content. Play icons and arrow icons often need 1-2px margin adjustment because their visual weight isn't centered in their bounding box. Fix in the SVG itself when possible.

- **Shadows instead of borders** — A layered `box-shadow` creates more depth than a flat `border` and transitions more smoothly on hover. Shadows adapt to any background since they use transparency. Borders don't. Use for cards, buttons, containers — but NOT for dividers or layout separators (those stay as borders).

**Light mode** — three layers: ring, lift, ambient:
```css
:root {
  --shadow-border:
    0 0 0 1px rgba(0, 0, 0, 0.06),
    0 1px 2px -1px rgba(0, 0, 0, 0.06),
    0 2px 4px 0 rgba(0, 0, 0, 0.04);
  --shadow-border-hover:
    0 0 0 1px rgba(0, 0, 0, 0.08),
    0 1px 2px -1px rgba(0, 0, 0, 0.08),
    0 2px 4px 0 rgba(0, 0, 0, 0.06);
}
```

**Dark mode** — simplify to a single white ring (layered depth shadows aren't visible on dark backgrounds):
```css
:root {
  --shadow-border: 0 0 0 1px rgba(255, 255, 255, 0.08);
  --shadow-border-hover: 0 0 0 1px rgba(255, 255, 255, 0.13);
}
```

**Usage:**
```css
.card {
  box-shadow: var(--shadow-border);
  transition-property: box-shadow;
  transition-duration: 150ms;
  transition-timing-function: ease-out;
}
.card:hover {
  box-shadow: var(--shadow-border-hover);
}
```

| Use shadows | Use borders |
|---|---|
| Cards, containers with depth | Dividers between list items |
| Buttons with bordered styles | Table cell boundaries |
| Elevated elements (dropdowns, modals) | Form input outlines (accessibility) |
| Elements on varied backgrounds | Hairline separators in dense UI |

- **Image outlines** — Add `outline: 1px solid rgba(0,0,0,0.1); outline-offset: -1px` to images (or white at 10% in dark mode). Creates subtle depth and consistent edge definition.

- **Focus-visible styling** — Custom focus rings that match the aesthetic instead of browser defaults. Use `:focus-visible` (not `:focus`) to only show on keyboard navigation.
