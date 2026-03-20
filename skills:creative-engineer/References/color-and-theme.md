# Color & Theme

## Principles

- Dominant + accent beats evenly distributed palettes. One color should own 70%+ of the canvas.
- Dark canvases (#0B0B0B, #0A0A0A, #111) let color and light detonate — this is why Active Theory, Lusion, and most WebGL-heavy sites go dark. Light themes work when the aesthetic demands warmth or editorial clarity.
- A single accent color used sparingly (CTAs, progress indicators, highlights) creates more impact than a rainbow.
- CSS custom properties for every color token. No hardcoded values.
- HSL is more intuitive than hex for programmatic color manipulation.

## Palette Construction

```css
:root {
  --bg: #0B0B0B;
  --fg: #F5F5F0;
  --fg-muted: #8A8A8A;
  --accent: #A970FF;       /* Use sparingly — CTAs, highlights only */
  --accent-subtle: #A970FF22;
  --surface: #161616;
  --border: #2A2A2A;
}
```

Vary this dramatically between projects. Some should be warm cream on charcoal. Others electric blue on pure black. Others muted earth tones. Others high-contrast black and white with a single red accent. The palette should feel inevitable for the concept, not interchangeable.

## The Human Touch Counter-Trend

As AI-generated visuals flood the web, intentional imperfection signals authenticity. This shows up in color and visual treatment:

- **Paper grain / noise textures** — Subtle noise overlay at 3-8% opacity using SVG `feTurbulence` or a tiling PNG. Use `mix-blend-mode: overlay`. Breaks digital flatness.
- **Slightly off-white backgrounds** — #FAFAF8, #F5F0EB, #FAF9F6 feel warmer and more human than pure #FFFFFF.
- **Desaturated, earthy palettes** — Muted greens, warm grays, terracotta, sage. Not everything needs to be electric.
- **Photography that isn't too polished** — Lighting that isn't perfect. Cropping that feels candid. Textures that show material.
- **Hand-drawn elements** — A rough underline, a sketched arrow, slightly misaligned decorative elements. These signal human craft.

## Backgrounds & Atmosphere

Never default to flat solid colors. Create depth and atmosphere:

- **Gradient meshes** — Multi-point gradients with organic shapes using `radial-gradient` layering or SVG filters
- **Noise textures** — SVG `feTurbulence` filter or a tiling noise PNG at low opacity
- **Geometric patterns** — Repeating SVG patterns, dot grids, line grids
- **Layered transparencies** — Semi-transparent overlapping shapes with `backdrop-filter: blur()`
- **Dynamic gradients** — Gradients that shift color based on scroll position or mouse movement
- **Vignette** — Subtle darkening at edges using `radial-gradient` overlay
- **Dot grid / graph paper** — A subtle repeating dot or line pattern using CSS `background-image` with `radial-gradient`
