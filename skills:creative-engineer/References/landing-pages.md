# Landing Pages & Page Craft

## Landing Page Archetypes

The best creative landing pages follow recognizable structural patterns. Choose one as a starting point:

### 1. Cinematic Scroll Storytelling
Pin sections, scrub through animations, reveal narrative beats as the user scrolls. The entire page is one continuous story. Examples: Apple product pages, Active Theory case studies.
- Hero with a single bold statement or 3D scene
- Pinned sections that transform while the user scrolls
- Content reveals timed to scroll position
- Minimal navigation — scrolling IS the navigation
- Works best for: product launches, brand stories, portfolio showcases

### 2. Typographic Hero with Staggered Reveal
The text IS the design. Oversized headlines, per-word animation, minimal imagery. Examples: Locomotive sites, editorial portfolios.
- XXL display type dominates the viewport
- Staggered word/character animation on load
- Scroll reveals secondary content below
- High contrast (dark bg, light type or vice versa)
- Works best for: agency sites, personal portfolios, SaaS with a bold message

### 3. WebGL Hero + Clean 2D Below
A stunning 3D or particle hero that captures attention, followed by clean, readable content. Examples: Lusion, Stripe, many Awwwards winners.
- Interactive 3D scene or particle system in the hero
- Clear transition to traditional layout below
- The 3D is the "wow," the content below is the "substance"
- Works best for: tech products, creative studios, developer tools

### 4. Horizontal Scroll Showcase
Content scrolls horizontally within a vertically-scrolling page. Creates a gallery or timeline feel.
- A pinned container with horizontal translation driven by vertical scroll
- Cards or images that slide through the viewport
- Progress indicator showing position
- Works best for: portfolios, product catalogs, timelines

### 5. Split-Screen / Dual Narrative
Two halves of the screen show different content, possibly scrolling independently.
- Fixed image on one side, scrolling text on the other
- Or alternating left/right content blocks
- Works best for: comparison pages, before/after, services

### 6. Single-Focus Conversion
Minimal distraction, one hero message, one CTA. Everything serves the conversion.
- Hero headline + subtext + single CTA above the fold
- Social proof immediately below
- Feature/benefit section
- Repeated CTA
- Works best for: SaaS signups, waitlists, product launches

## Hero Section Patterns

The hero is the first 2-5 seconds. Make them count:

- **Staggered load reveal** — Logo → headline → subtext → CTA, each 80-100ms apart. The most reliable "premium feel" technique.
- **Video loop hero** — Full-bleed autoplay muted video. Use `object-fit: cover`. Overlay with semi-transparent gradient for text readability.
- **Particle/generative background** — Canvas or WebGL particles that react to cursor. Subtle enough to not distract from content.
- **Kinetic headline** — Words that rotate, fill, or animate. Variable font weight morphing. Clip-path reveals.
- **3D product showcase** — Interactive model the user can rotate or that rotates on scroll.
- **Static with one perfect detail** — A beautifully set headline with one animated accent. Sometimes restraint is the statement.

## Page Transitions

The best sites don't just have animated components — navigating between pages is itself an orchestrated moment:

- **Crossfade** — Old page fades out, new page fades in. Simplest, always works. 300-400ms.
- **Shared element transitions** — An element (image, card, headline) that exists on both pages animates between its two positions. Creates spatial continuity. Use View Transitions API or Motion's `layoutId`.
- **Clip-path wipe** — New page reveals via an expanding `clip-path: circle()` from the click point, or `inset()` from an edge.
- **Slide** — Pages slide in from a direction that matches the navigation hierarchy (forward = left, back = right).
- **Overlay** — New page slides up over the current one like a sheet.

**Key principle:** Page transitions should maintain spatial continuity. The user should understand WHERE the new content came from relative to where they were.

## Video Integration

Video is a first-class element on top creative sites, not just an embed:

- **Autoplay hero loops** — Short (5-15s), muted, looping. `playsinline` for mobile. Compressed to 2-5MB. Use `<video>` not `<iframe>`.
- **Scroll-linked video scrubbing** — Video playback position tied to scroll position. The user "scrubs" through a video by scrolling. Use `requestAnimationFrame` to set `video.currentTime` based on scroll progress.
- **Video-as-texture in WebGL** — Feed a `<video>` element into a Three.js texture. Apply it to a plane with custom shader distortion.
- **Video mask reveals** — Video visible only through a text shape or custom clip-path. The text becomes a window into the video.
- **Hover-triggered video** — Thumbnail that plays a preview video on hover (like Active Theory's portfolio tiles). Use `mouseenter`/`mouseleave` to play/pause.

## The Preloader as First Impression

The loading sequence is the first 1–3 seconds of the experience. On sites where performance allows it, treat the preloader as a choreographed entrance — not a spinner.

**When to invest in a preloader:**
- The site loads heavy assets (WebGL, video, large images) and needs to buy time
- The brand has a strong visual identity that can be introduced through motion
- The experience is meant to feel immersive or cinematic

**When to skip it:**
- The site is lightweight and loads in under a second
- The audience values speed over ceremony (SaaS, e-commerce, documentation)
- The content is the attraction, not the wrapper

**Approaches:**
- **Logo animation** — The brand mark assembles, fills, or reveals through clip-path or stroke animation. Sets the visual tone before content appears.
- **Progress-driven reveal** — A progress bar or counter tied to actual asset loading. Honest about the wait.
- **Narrative text** — Short phrases that appear in sequence, building anticipation. Works for storytelling sites.
- **Coordinated handoff** — The preloader dispatches events when complete, and page animations begin in response. The preloader ending and the page beginning should feel like one continuous motion.

The preloader should match the site's aesthetic temperature exactly. A minimal site needs a minimal preloader. A cinematic site earns a cinematic entrance.

## Non-Standard Navigation

Standard nav (logo left, links right, hamburger on mobile) works for most projects. But for portfolio, creative, and immersive sites, the navigation itself can be part of the concept.

**Approaches:**
- **Hidden/reveal menus** — Navigation that only appears on interaction (click, hover, scroll to top). Maximizes canvas space for content.
- **Metaphorical navigation** — Replacing "About/Work/Contact" with language that fits the concept. A game studio might use game terminology. A geography-themed site might use place names. The navigation vocabulary reinforces the world.
- **The interface IS the navigation** — The entire site is a navigable space (a game world, a map, a terminal, a timeline). No traditional nav exists because movement through the space IS navigation.
- **Scroll-as-navigation** — Sections flow as a continuous narrative. No nav links needed — the user discovers content by scrolling. A subtle progress indicator shows position.
- **Mega menus with staggered animation** — Full-screen overlays that animate in with staggered reveals. The menu opening is itself a moment of delight.

The navigation approach should match the project's purpose. An immersive portfolio can afford experimental navigation. A SaaS product page cannot — users need to find pricing fast.

## Scroll-Driven Storytelling Through Theme

The color palette doesn't have to be static across the page. Shifting the entire theme — background, text color, accent — as the user scrolls through sections creates narrative progression through atmosphere.

**How it works:**
- Each section declares its own theme via a data attribute (`[data-theme="dark"]`, `[data-theme="warm"]`, etc.)
- CSS custom properties update per-section, and transitions smooth the shift
- Or use ScrollTrigger to interpolate between palette values based on scroll position

**When it works best:**
- Pages that tell a story with distinct chapters or moods
- Product pages that shift from problem (dark, tense) to solution (light, open)
- Portfolios where each project has its own visual identity

**When to avoid:**
- Short pages where the shift would feel abrupt
- Functional interfaces where consistency aids usability
- Pages where the user jumps between sections via nav links (the scroll progression is lost)

The shift should feel inevitable, not jarring. Transition between palettes that share at least one common value (a shared neutral, a consistent accent) so the change reads as evolution rather than a break.

## The Human Touch

In a world of AI-generated perfection, intentional imperfection signals authenticity:

- **Hand-drawn elements** — A rough underline, a sketched arrow, slightly misaligned decorative elements
- **Candid photography** — Images that look real, not stock. Imperfect lighting, natural crops
- **Texture** — Paper grain, fabric weave, concrete, wood. Real-world materials as digital backgrounds
- **Organic shapes** — Blobs, hand-drawn circles, imperfect curves instead of perfect geometric forms
- **Personality in copy** — Writing that sounds human, not corporate. This extends to UI labels, error messages, empty states

These don't conflict with polish — they complement it. A technically perfect site with intentional human touches feels more inviting than one that's perfect in every dimension.
