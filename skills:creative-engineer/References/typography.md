# Typography

Typography is the highest-leverage design decision. The top creative studios treat type as architecture, not decoration.

## Principles from the best

- Pair a distinctive display font with a refined body font. The contrast between them creates hierarchy and character.
- XXL headlines are a signature of award-winning sites. Active Theory uses Monument Grotesk at massive scale on a strict 12-column grid. Locomotive sites often feature type that dominates the viewport.
- Variable fonts unlock weight and width animation — use them for hover states and scroll-driven type transitions.
- Negative tracking on large display type creates density and presence. Positive tracking on small caps and labels creates breathing room.
- Overflow-hidden on containers with translateY animation on inner text creates masked reveal effects (a GSAP SplitText signature technique).

## Text Rendering

- Apply `-webkit-font-smoothing: antialiased` (or `antialiased` in Tailwind) to the body. Subpixel rendering on macOS makes text appear heavier than intended — antialiased rendering produces thinner, crisper type, especially light text on dark backgrounds.
- Use `text-wrap: balance` on headings to distribute text evenly across lines and prevent orphaned words. Use `text-wrap: pretty` on body text for a similar effect with a different algorithm.
- Use `font-variant-numeric: tabular-nums` on any numbers that update dynamically (counters, prices, timers, stats). This makes digits equal width so the layout doesn't shift when values change.

## Font Selection

**NEVER use these:**
Inter, Roboto, Arial, Helvetica, system-ui, Open Sans, Lato, Montserrat, Poppins, Space Grotesk (overused in AI contexts)

**Reach for these categories instead:**
- Display: Editorial New, Playfair Display, Clash Display, Syne, Cabinet Grotesk, General Sans, Satoshi, Switzer, Gambetta, Instrument Serif, Fraunces
- Monospace with character: JetBrains Mono, Berkeley Mono, Geist Mono, IBM Plex Mono, Fira Code
- Refined sans: Geist, Plus Jakarta Sans, DM Sans, Outfit, Manrope, Wix Madefor Display
- Serifs with warmth: Lora, Source Serif Pro, Newsreader, Literata

Import from Google Fonts or use CDN links. Every project should use a DIFFERENT font combination — never converge on the same pairing across generations.

## Kinetic Typography

Text as motion element, not just static content. Techniques used by top creative studios:

- **Scroll-driven text fill** — Use `clip-path` or `background-clip: text` with a gradient that shifts based on scroll position. Text appears to fill with color as the user scrolls.
- **Per-character stagger reveals** — Split headlines into `<span>` per character, animate each with translateY from below + opacity + blur, staggered at ~50-80ms. Wrap container in `overflow: hidden` for a masked reveal effect.
- **Rotating headline variations** — Cycle through different words/phrases in a headline using AnimatePresence or GSAP timeline. Common on SaaS hero sections: "Build [faster/better/smarter]"
- **Variable font animation** — Animate `font-weight` or `font-variation-settings` on hover or scroll. Weight morphing between 300 and 900 creates a breathing, organic effect.
- **Marquee / ticker** — Infinitely scrolling horizontal text using CSS animation with `translateX`. Double the content to create a seamless loop. Use `will-change: transform` for GPU acceleration.
- **Text outline / stroke** — `-webkit-text-stroke: 1px currentColor` with transparent fill creates elegant outlined type. Alternate between filled and outlined words for rhythm.
- **Scale on scroll** — Headlines that grow or shrink as the user scrolls, using ScrollTrigger scrub. Creates a dramatic zoom-in/zoom-out storytelling moment.

## Font Loading Strategy

- `font-display: swap` or `optional`. Preload critical fonts with `<link rel="preload" as="font" type="font/woff2" crossorigin>`.
- Load display fonts first (hero headline), body fonts can swap in.
- Subset fonts to only the characters needed when possible.
