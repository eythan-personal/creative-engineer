# Layout & Spatial Composition

**Break the grid intentionally, not accidentally.**

## Core Principles

- **Asymmetric layouts** create visual tension and guide the eye. One large element + one small element beats two medium elements.
- **Overlap** creates depth. Let images bleed under text. Let sections overlap by 10-20%. Use negative margins or absolute positioning.
- **Generous negative space** signals confidence and luxury. Dense layouts signal information-richness and energy. Choose based on concept.
- **Viewport-filling sections** for impact. Full-height hero sections with a single statement.
- **Grid-breaking elements** that span unexpected columns or extend beyond the container create visual surprise.
- **Z-axis layering** — elements at different visual depths (blur, scale, opacity) create atmosphere without 3D.

**CSS Grid is the layout backbone.** Use named grid areas for complex layouts. Use `subgrid` for nested alignment. Use `clamp()` for fluid sizing that respects minimum and maximum bounds.

## Bento Grids

For product/feature showcases, bento grids (mixed-size cards in a grid) create visual hierarchy without requiring asymmetric free-form layout. The key is variation — not every card the same size.

**Principles:**
- One or two cards should be visually dominant (2x width or 2x height)
- Smaller cards cluster around the dominant ones
- Each card earns its size — the most important feature gets the largest card
- Avoid perfectly uniform grids where every card is identical. That's the anti-pattern.
- Use `grid-template-columns` with explicit spans rather than `auto-fit` — bento grids need deliberate sizing, not automatic flow

## Sticky Navigation with Glass

Sticky headers with `backdrop-filter: blur()` and semi-transparent backgrounds are purposeful — they maintain navigation access without obscuring content. This is NOT gratuitous glassmorphism.

```css
nav {
  position: sticky;
  top: 0;
  background: rgba(255, 255, 255, 0.8);
  backdrop-filter: blur(24px);
  -webkit-backdrop-filter: blur(24px);
  z-index: 100;
}
```

For dark themes, use `rgba(0, 0, 0, 0.7)` or similar. The transparency should be just enough to hint at content scrolling beneath — not so much that the nav text becomes unreadable.

## Spatial Rhythm

Don't use identical spacing everywhere. Vary section padding to create rhythm:
- Hero section: generous (120-200px vertical padding)
- Content sections: moderate (80-120px)
- Tight functional areas: compact (40-60px)
- Between related elements: tight (16-24px)

The variation in density creates visual breathing — sections feel like they have different weights and importance.

## Non-Linear Navigation

The top creative sites in 2026 are moving beyond standard "Home/About/Contact" structures:
- Hidden menus that reveal on click or hover
- Playful cursors that react to movement
- Interactive hotspots that guide non-linear exploration
- Scroll-as-navigation where sections flow like a story
- Mega menus with staggered animations and section reveals
