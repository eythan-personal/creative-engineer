# Creative Engineer

An [Agent Skill](https://code.claude.com/docs/en/skills) for AI coding assistants (Claude Code, Codex, etc.) that produces distinctive, production-grade frontend interfaces — and kills AI slop.

Most AI-generated UI looks the same: purple gradients, uniform card grids, `border-radius: 12px` on everything. This skill teaches your agent to make intentional design decisions grounded in how the best creative studios and design engineers actually work.

## What it covers

| Domain | What's inside |
|---|---|
| **Typography** | Font selection, banned defaults, kinetic type, fluid sizing with `clamp()`, font smoothing, `text-wrap: balance` |
| **Color & Theme** | Palette construction, dominant/accent hierarchy, CSS custom properties, atmospheric backgrounds, dark mode |
| **Motion** | Enter/exit animations, stagger timing, interruptibility, easing curves, scale on press, scroll experiences |
| **Timing** | Duration guide grounded in the Human Processor Model — cognitive science behind why 100ms staggers and 200ms transitions feel right |
| **Layout** | Asymmetric composition, spatial rhythm, CSS Grid patterns, fluid sizing, content width capping |
| **Responsive** | Mobile-first strategy, breakpoints, fluid typography/spacing, container queries, responsive images |
| **Micro-interactions** | Custom cursors, magnetic buttons, clip-path reveals, icon animations, shadow systems, optical alignment |
| **Performance** | `transition: all` ban, `will-change` rules, 60fps constraints, GPU-compositable properties |
| **Landing pages** | Page archetypes, hero patterns, scroll storytelling, page transitions, video integration |
| **3D & WebGL** | Three.js, shaders, matcaps, baked lighting, Draco compression, performance-first 3D |
| **Accessibility** | `prefers-reduced-motion`, semantic HTML, focus management, WCAG contrast, touch targets |

## Structure

```
skills/creative-engineer/
├── SKILL.md                                  # Core skill — design thinking, rules, anti-patterns
└── References/
    ├── typography.md                         # Font selection, kinetic type, variable fonts
    ├── color-and-theme.md                    # Palettes, dark/light, atmospheric backgrounds
    ├── motion.md                             # Animation hierarchy, timing, Human Processor Model
    ├── layout.md                             # Spatial composition, grid-breaking, asymmetry
    ├── responsive-design.md                  # Breakpoints, fluid systems, mobile concerns
    ├── micro-interactions.md                 # Polish details, shadows, cursors, clip-path
    ├── landing-pages.md                      # Page archetypes, hero patterns, scroll stories
    ├── 3d-and-webgl.md                       # Three.js, shaders, performance-first 3D
    ├── accessibility-and-performance.md      # WCAG, perf budgets, font loading
    └── cdn-and-libraries.md                  # CDN links, React patterns, library setup
```

The skill is self-contained — core rules are inline so most tasks don't require reading reference files. References are consulted only when deeper guidance is needed for a specific domain.

## Installation

```bash
npx skills add eythan-personal/creative-engineer
```

## Usage

Once installed, the skill activates automatically when building frontend interfaces, components, or pages.

You can also invoke it manually:

```
/creative-engineer
```

## How it's different

Most UI skills focus on polish details — concentric border radius, font smoothing, tabular numbers. That's table stakes.

This skill starts with **design thinking** — concept, aesthetic temperature, technical strategy — before touching code. It covers the full creative development spectrum from typography selection to WebGL shaders, with animation timing grounded in cognitive science rather than vibes.

## Anti-patterns it prevents

- Purple-to-blue gradients on white backgrounds
- Card grids with uniform border-radius and subtle shadows
- Generic icon + heading + paragraph layouts
- `border-radius: 12px` on everything
- Uniform spacing with no rhythm variation
- `transition: all` and non-interruptible animations
- Over-animation with no hierarchy or purpose

## License

MIT
