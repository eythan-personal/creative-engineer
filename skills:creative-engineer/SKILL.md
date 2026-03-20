---
name: creative-engineer
description: Create distinctive, production-grade frontend interfaces with high design quality. Use this skill when the user asks to build web components, pages, artifacts, posters, or applications (examples include websites, landing pages, dashboards, React components, HTML/CSS layouts, or when styling/beautifying any web UI). Generates creative, polished code and UI design that avoids generic AI aesthetics. Covers the full creative development spectrum including WebGL, 3D, shaders, scroll-driven animation, motion design, typography, layout, micro-interactions, and landing page craft.
---

This skill guides creation of distinctive, production-grade frontend interfaces. The goal is not to build sites that look good — it's to build interfaces that feel alive. Every decision about type, color, motion, and space should serve an emotional intent. The best interfaces don't announce their craft — they make you feel something before you've consciously noticed a single design choice.

## Design Thinking

**MANDATORY: Before writing ANY code, state your three decisions explicitly.** Write them out as a brief creative brief. Do not skip this step. Do not default to safe choices. The output must include your reasoning.

### 1. Concept
Start with a feeling, not a feature. What emotional state should someone be in after 5 seconds on this page? Not "impressed by the animation" — something more specific: *momentum*, *stillness*, *tension*, *warmth*, *precision*, *play*. That feeling becomes the concept, and every technical decision flows from it.

Then define it in one sentence — not what the site looks like, but what it feels like to use:
- "The site feels like it's already in motion when you arrive — everything has velocity"
- "It feels like opening a physical book — quiet, tactile, considered"
- "It feels like being inside a cockpit — dark, focused, instrument-precise"
- "It feels like walking through a gallery — generous space, each piece given room to breathe"
- "It feels like nothing — the interface disappears and only the content exists"

If you can't describe the feeling, you don't have a concept yet. You have a layout.

**The strongest concepts make the medium the message.** A portfolio that IS an interactive experience is more memorable than one that shows screenshots of interactive experiences. A product page that feels like using the product is more persuasive than one that describes it. Ask: can the interface itself embody what it's communicating?

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
- **Nothing.** Zero animation, zero effects — when the content and typography are strong enough to carry the page alone. Some of the most respected product and luxury sites use almost no motion. Restraint is not a failure of imagination — it's a deliberate choice that signals confidence.

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
- Think in tiers, not pairs. The strongest typographic systems use 3–4 fonts with distinct roles: **display** (headlines, hero), **body** (readable prose), **mono** (code, labels, data), and optionally **accent** (pull quotes, special elements). Each tier serves a different function — don't use two fonts doing the same job.
- `-webkit-font-smoothing: antialiased` on body
- `text-wrap: balance` on headings
- `font-variant-numeric: tabular-nums` on dynamic numbers
- Fluid sizing with `clamp()` — no hardcoded pixel values for type

### Color
- One dominant color owns 70%+ of the canvas. One accent used sparingly.
- CSS custom properties for every color token. No hardcoded values.
- **Content should feel lit, not placed.** The background isn't just a surface — it's an environment. Dark canvases make images feel like they're glowing on a lightbox. Light canvases with warm undertones make content feel sunlit. The relationship between background and content creates atmosphere. A flat `#FFFFFF` background creates no atmosphere.
- Build depth into the canvas: gradient meshes, noise textures, dot grids, vignettes, or layered transparencies. Grain/noise overlay at 3–5% opacity with `mix-blend-mode: overlay` is baseline — it breaks digital flatness on nearly every project.
- **Consider scroll-driven palette shifts.** The color scheme doesn't have to be static — sections can transition between palettes as the user scrolls, using `[data-theme]` attributes or CSS custom property updates tied to scroll position. This creates narrative progression through atmosphere alone.

### Motion
- **Not every project needs animation.** Luxury, editorial, and enterprise product sites often achieve their best work with near-zero motion — just perfect typography, spacing, and image treatment. If the brief calls for "professional" or "clean," consider whether restraint serves the intent better than animation. Quiet confidence doesn't need to move.
- **When you do animate, define the physics first.** Every interface has an implied physical character. Is it heavy or light? Fast or deliberate? Does it have momentum or is it precise? Define this before choosing easing curves. A site about speed should have elements that enter fast and decelerate with control — like braking into a corner. A site about craft should have motion that's slow, intentional, and weighty. The easing and timing follow from the feeling, not the other way around.
- **Elements should arrive, not appear.** Nothing should simply pop into existence. Everything enters from somewhere — sliding in with purpose, scaling up from a point, wiping in from an edge. The direction of entry should imply where the element came from, creating spatial coherence even in 2D.
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
- **Pace the scroll like a director paces a film.** Some sections should breathe — generous space, a single image, room for the eye to rest. Then tighten up — dense grids, tight spacing, rapid information. Then open back up. This push-and-pull between immersion and scanning keeps the user engaged without fatiguing them. A page with uniform density is monotonous. A page with tempo changes is alive.
- Vary section spacing to create rhythm — not identical padding everywhere. Hero sections: generous (120–200px). Content: moderate (80–120px). Dense functional areas: compact (40–60px).
- **Break scroll direction when the content calls for it.** A horizontal scroll section inside a vertical page forces the user to engage differently — it interrupts muscle memory and creates a distinct moment. Use sparingly and intentionally.
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

The cure: start with a feeling. If you can describe how the interface should make someone feel — and every decision (palette, type, motion, spacing) serves that feeling — the output will have a point of view. If you can swap the palette and fonts and it feels the same, you started with technique instead of intent.

## Reference Files

Read these **only when the task requires deeper guidance** in that domain. The core rules above are sufficient for most work.

| Read this | When the task involves |
|---|---|
| `References/typography.md` | Choosing fonts, kinetic type, variable font animation, text reveals |
| `References/color-and-theme.md` | Building a new palette, theme switching, atmospheric backgrounds |
| `References/motion.md` | Complex animation sequences, GSAP/ScrollTrigger, Motion gestures, scroll experiences |
| `References/layout.md` | Full page layouts, grid-breaking, spatial composition, bento grids, sticky glass nav, non-linear navigation |
| `References/responsive-design.md` | Multi-viewport support, fluid systems, responsive images, mobile-specific concerns |
| `References/micro-interactions.md` | Custom cursors, magnetic buttons, clip-path reveals, visual refinement details |
| `References/landing-pages.md` | Page archetypes, hero patterns, scroll storytelling, page transitions, video integration, preloaders, non-standard navigation, scroll-driven theming |
| `References/3d-and-webgl.md` | Three.js, shaders, 3D performance, particle systems |
| `References/accessibility-and-performance.md` | WCAG compliance, performance budgets, font loading, code splitting |
| `References/cdn-and-libraries.md` | CDN links, library setup, React patterns for GSAP/Three.js/Motion, font loading |

