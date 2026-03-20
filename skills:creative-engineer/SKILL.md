---
name: creative-engineer
description: Create distinctive, production-grade frontend interfaces with high design quality. Use this skill when the user asks to build web components, pages, artifacts, posters, or applications (examples include websites, landing pages, dashboards, React components, HTML/CSS layouts, or when styling/beautifying any web UI). Generates creative, polished code and UI design that avoids generic AI aesthetics. Covers the full creative development spectrum including WebGL, 3D, shaders, scroll-driven animation, motion design, typography, layout, micro-interactions, and landing page craft.
---

This skill guides creation of distinctive, production-grade frontend interfaces that match the quality bar set by studios like Locomotive, Active Theory, and Lusion — and the design engineering craft of Linear, Vercel, and Raycast.

## Design Thinking

**MANDATORY: Before writing ANY code, state your three decisions explicitly.** Write them out as a brief creative brief. Do not skip this step. Do not default to safe choices. The output must include your reasoning.

### 1. Concept
What is the ONE thing someone will remember about this interface? Not "it looked nice" — a specific, defensible idea. Examples:
- "The entire page is a single scroll-driven camera move through a 3D scene"
- "Typography IS the interface — no images, no icons, just type at extreme scale"
- "Every section uses a different clip-path reveal triggered by scroll"
- "The site feels like opening a physical book — page turns, paper texture, serif type"

If you can't state the concept in one sentence, you don't have one yet.

### 2. Aesthetic Temperature
Pick a position and commit fully. But **do not default to dark background + warm accent + editorial serif.** That is the AI-generated portfolio default. Actively pick something less obvious.

Spectrum positions:
- Brutally minimal → Luxury/refined → Editorial/magazine → Art deco/geometric
- Soft/organic/wabi → Retro-futuristic → Maximalist chaos → Brutalist/raw
- Industrial/utilitarian → Playful/toy-like → Noir/cinematic → Warm humanist
- 8-bit/pixel → Glassmorphic → Neubrutalist → Swiss/grid-strict

**Variety mechanism:** Before choosing, consider the current date. Use it to rotate your starting instinct — if today's date is even, start from the bottom half of the spectrum. If odd, the top half. Then synthesize from there. The goal is to never produce the same aesthetic twice.

### 3. Technical Strategy
Match the stack to the vision — don't reach for everything:
- Pure CSS animation for elegant reveals and micro-interactions
- GSAP + ScrollTrigger for scroll-driven storytelling and complex timelines
- Three.js / R3F for 3D scenes, particle systems, and shader effects
- Motion (Framer Motion) for React-first declarative UI transitions and gestures
- Lottie for designer-grade vector animations
- Canvas 2D for custom particle effects and generative visuals
- CSS-only when restraint IS the aesthetic

Pick ONE primary strategy. Adding a particle canvas AND scroll animations AND custom cursors AND a marquee is not a strategy — it's a grab bag.

## Default Traps

These aren't anti-patterns (they can be done well) — but they're what AI defaults to when it has no strong concept. If you catch yourself reaching for any of these, pause and ask whether you chose it or fell into it:

- Dark background (#0A0A0A) + warm/gold accent + Instrument Serif
- Particle constellation canvas in the hero
- "Let's build *something*" or "Let's work *together*" contact CTA
- Stacked work list with hover-slide-right animation
- Hero → About → Marquee → Work → Feature → Contact → Footer structure
- Custom cursor as the primary interaction novelty
- Noise texture overlay + vignette as the only atmospheric treatment
- Marquee/ticker as a section divider

Any of these can be great if it's a deliberate choice that serves the concept. None of them are great as a default.

## Core Rules

These apply to every frontend output. No exceptions.

### Typography
- Never use: Inter, Roboto, Arial, Helvetica, system-ui, Open Sans, Lato, Montserrat, Poppins, Space Grotesk
- Choose distinctive fonts. Every project should use a different combination.
- `-webkit-font-smoothing: antialiased` on body
- `text-wrap: balance` on headings
- `font-variant-numeric: tabular-nums` on dynamic numbers
- Fluid sizing with `clamp()` — no hardcoded pixel values for type

### Color
- One dominant color owns 70%+ of the canvas. One accent used sparingly.
- CSS custom properties for every color token. No hardcoded values.
- Background has depth — never a flat solid. Use gradient meshes, noise textures, dot grids, vignettes, or layered transparencies.

### Motion
- Animation earns its place: if removing it changes nothing, cut it.
- Enter animations: split content into semantic chunks, stagger at `~100ms`. Headlines split into words at `~80ms`. Combine `opacity: 0`, `translateY(8px)`, `blur(4px)`. Enter duration: `300–400ms`.
- Exit animations: subtle. Use `translateY(-12px)` + `opacity: 0`, not full slide-outs. Exit duration: `~150ms` — shorter than enter.
- Animations must be interruptible when the user can re-trigger them. Use CSS transitions for interactive states (hover, toggle, open/close). Reserve keyframes for one-shot sequences.
- Scale on press: `scale(0.96)` on `:active` for tactile button feedback. Never below `0.95`.
- `prefers-reduced-motion` is always respected.
- Easing matters more than duration. Use `cubic-bezier(0.16, 1, 0.3, 1)` for snappy, `cubic-bezier(0.83, 0, 0.17, 1)` for smooth. Never `linear` for UI motion.
- Duration guide: micro-interactions `150–250ms`, standard transitions `200–350ms`, complex sequences `400–800ms`. Over `500ms` for a simple interaction feels sluggish.
- Animate only `transform` and `opacity` for 60fps.

### Performance
- Never use `transition: all`. Always specify exact properties: `transition-property: scale, opacity`.
- Use `will-change` sparingly — only for `transform`, `opacity`, `filter`. Never `will-change: all`. Only add it when you see first-frame stutter.
- Icon swaps: animate with `opacity`, `scale(0.25 → 1)`, and `blur(4px → 0)` — never toggle visibility instantly.

### Layout
- Asymmetric layouts create tension. One large + one small beats two medium.
- Vary section spacing to create rhythm — not identical padding everywhere.
- Use CSS Grid with `clamp()` for fluid sizing. `auto-fit` + `minmax` for self-responsive grids.
- Cap content width: `width: min(100% - 2rem, 1200px)`. Body text max `65ch`.

### Polish
- Nested rounded elements: `outer radius = inner radius + padding`
- Shadows over borders for depth on cards/containers
- Hover and focus-visible states on all interactive elements
- Semantic HTML (`nav`, `main`, `section`, `article`, `header`, `footer`)
- Touch targets minimum 44x44px
- Viewport meta tag: `<meta name="viewport" content="width=device-width, initial-scale=1">`

## Anti-Patterns

These signal generic AI output. Avoid all of them:

- Purple-to-blue gradients on white backgrounds
- Card grids with uniform border-radius and subtle shadows
- Mismatched border radii on nested elements
- Generic icon + heading + paragraph card layouts
- Uniform spacing with no rhythm variation
- `border-radius: 12px` on everything
- Emojis as visual elements in professional interfaces
- Glassmorphism without purpose
- "Hero → features grid → testimonials → CTA" template structure
- Stock illustration style without customization
- Gratuitous blur/glow effects without compositional intent
- Non-interruptible animations on re-triggerable elements
- Identical enter and exit animations
- Over-animation with no hierarchy or purpose

The cure: commit to a specific aesthetic concept and let every decision flow from it. If you can swap the palette and fonts and it looks the same, the design has no point of view.

## Reference Files

Read these **only when the task requires deeper guidance** in that domain. The core rules above are sufficient for most work.

| Read this | When the task involves |
|---|---|
| `References/typography.md` | Choosing fonts, kinetic type, variable font animation, text reveals |
| `References/color-and-theme.md` | Building a new palette, theme switching, atmospheric backgrounds |
| `References/motion.md` | Complex animation sequences, GSAP/ScrollTrigger, Motion gestures, scroll experiences |
| `References/layout.md` | Full page layouts, grid-breaking, spatial composition, non-linear navigation |
| `References/responsive-design.md` | Multi-viewport support, fluid systems, responsive images, mobile-specific concerns |
| `References/micro-interactions.md` | Custom cursors, magnetic buttons, clip-path reveals, visual refinement details |
| `References/landing-pages.md` | Page archetypes, hero patterns, scroll storytelling, page transitions, video integration |
| `References/3d-and-webgl.md` | Three.js, shaders, 3D performance, particle systems |
| `References/accessibility-and-performance.md` | WCAG compliance, performance budgets, font loading, code splitting |
| `References/cdn-and-libraries.md` | CDN links, library setup, React patterns for GSAP/Three.js/Motion, font loading |

