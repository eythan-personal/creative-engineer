# Motion & Animation

Motion separates good interfaces from unforgettable ones. The top creative developers treat animation as functional UX, not decoration. A core principle from design engineering: "The best animations are the ones you don't notice." If someone says "nice animation," you've probably overdone it.

## Hierarchy of Motion Tools

### Level 1 — CSS Transitions & Keyframes (use first, always)
For hover states, focus indicators, color shifts, simple reveals. Hardware-accelerated via transform and opacity. Zero dependencies.

```css
.element {
  transition: transform 0.6s cubic-bezier(0.16, 1, 0.3, 1), opacity 0.6s ease;
}
```

### Level 2 — GSAP + ScrollTrigger (the industry standard for scroll-driven work)
The creative development community has converged on GSAP as the animation backbone. ScrollTrigger enables pinning, scrubbing, and scroll-linked animation. SplitText enables per-character and per-word animation.

Key patterns:
- **Staggered reveals**: Elements animate in sequence with `stagger: 0.08` for cascading entrances
- **Scroll-scrub**: `scrub: true` ties animation progress directly to scroll position
- **Pin sections**: Pin a container while its content transforms, creating storytelling sequences
- **Text mask reveals**: Split text into chars, wrap in overflow-hidden containers, animate translateY from 100% to 0
- **Parallax layers**: Different `data-scroll-speed` values on layered elements
- **Timeline orchestration**: `gsap.timeline()` sequences multiple tweens with precise offsets

```js
gsap.from('.fade-in', {
  scrollTrigger: {
    trigger: '.fade-in',
    start: 'top 80%',
    toggleActions: 'play none none reverse'
  },
  y: 60,
  opacity: 0,
  duration: 1,
  ease: 'power3.out'
});
```

### Level 3 — Motion / Framer Motion (React-specific)
For component-level transitions, layout animations, AnimatePresence mount/unmount, and gesture-driven interactions. Declarative and composable.

Motion's gesture system maps every user action to an animated response. The six gesture types:
- **`whileHover`** — Scale, rotation, color shifts, reveal effects. Spring animations feel more natural than CSS easing.
- **`whileTap`** — Use `scale: 0.95` for satisfying button press feedback. Cancels if pointer moves away. Keyboard accessible (`return` key triggers it).
- **`whileDrag`** — Makes elements directly draggable. Use `dragConstraints` to keep elements within bounds. Great for dismissible cards, reorderable lists.
- **`onPan`** — No `while-` prop, use event handlers. Ideal for custom sliders and scrubbers.
- **`whileFocus`** — Follows `:focus-visible` logic. Keep focus animations restrained — complex motion during keyboard navigation is disorienting.
- **`whileInView`** — Scroll-based reveals. Pair with `initial` for enter animations. Use `viewport={{ amount: 0.5 }}` for half-visible trigger.

**Spring animations over CSS easing for gestures.** Springs model physical behavior. Use `type: "spring"` with `duration` and `bounce: 0` for snappy, non-oscillating springs. Motion's JS animations run on the compositor thread — performance parity with CSS, sometimes better for independent transforms.

### Level 4 — Lottie (designer-grade vector animation)
For complex illustrative animations exported from After Effects. Small file sizes, resolution-independent. Use for onboarding flows, empty states, loading indicators.

## Motion Principles

- **Easing matters more than duration.** `cubic-bezier(0.16, 1, 0.3, 1)` (ease-out expo) feels snappy and modern. `cubic-bezier(0.83, 0, 0.17, 1)` (ease-in-out circ) feels smooth and intentional. Never use `linear` for UI motion.
- **One well-orchestrated page load beats scattered micro-interactions.** A staggered hero reveal (logo → headline → subtext → CTA, each 80ms apart) creates more delight than random hover effects.

### Why These Durations Work: The Human Processor Model

Animation timings aren't arbitrary — they're grounded in how the human perceptual system processes information. The Human Processor Model provides the cognitive science behind why certain durations feel right.

| Human parameter | Mean | Range | What it means for animation |
|---|---|---|---|
| Perceptual processor cycle | 100ms | 50–200ms | **Stagger delay floor.** Below ~80ms the brain can't distinguish sequence order — items blur together. At 80–100ms each item registers as a distinct beat. |
| Eye movement time | 230ms | 70–700ms | **Standard transition sweet spot.** A 200–350ms transition completes by the time the eye settles on the new state — the change feels instantaneous. |
| Visual image storage decay | 200ms | 90–1000ms | **Micro-interaction ceiling.** At 150–250ms the animation completes within one cycle of visual memory — the user perceives the change without consciously "watching" it. |
| Cognitive processor cycle | 70ms | 25–170ms | **Exit animation baseline.** At ~150ms (about two cognitive cycles), the brain registers that something left without dwelling on it. Shorter feels abrupt, longer steals attention. |
| Working memory capacity | 7 chunks | 5–9 chunks | **Stagger group limit.** Break content into 5–7 staggered groups max. More than that overloads working memory — the sequence stops feeling orchestrated and starts feeling chaotic. |
| Working memory decay (3 chunks) | 7 sec | 5–34 sec | **Scroll sequence pacing.** If a scroll-driven narrative has more than ~3 key beats, earlier ones fade from working memory. Reinforce important information or keep sequences under 7 seconds of scroll time. |

**Duration guide, grounded in these parameters:**

| Animation type | Duration | Why |
|---|---|---|
| Micro-interactions (hover, press, toggle) | 150–250ms | Within visual storage decay — feels instant |
| Standard transitions (modals, panels, tabs) | 200–350ms | Matches eye movement time — completes as gaze settles |
| Enter stagger delay | 80–100ms | One perceptual cycle — each item registers as distinct |
| Exit animations | ~150ms | Two cognitive cycles — noticed but not dwelt on |
| Complex sequences (page reveals, scroll stories) | 400–800ms | Multiple perceptual cycles — allows the eye to track |
| Anything over 500ms for a simple interaction | Too slow | Exceeds visual storage decay — user is waiting, not experiencing |

### Interruptible Animations

CSS transitions interpolate toward the latest state and can be interrupted mid-animation. CSS keyframe animations run on a fixed timeline and restart from the beginning if re-triggered. If a user can trigger an animation again before it finishes, it MUST be interruptible.

| | CSS Transitions | CSS Keyframe Animations |
|---|---|---|
| **Behavior** | Interpolate toward latest state | Run on a fixed timeline |
| **Interruptible** | Yes — retargets mid-animation | No — restarts from beginning |
| **Use for** | Interactive state changes (hover, toggle, open/close) | Staged sequences that run once (enter animations, loading) |

```css
/* Good — interruptible transition for a toggle */
.drawer {
  transform: translateX(-100%);
  transition: transform 200ms ease-out;
}
.drawer.open {
  transform: translateX(0);
}
/* Clicking again mid-animation smoothly reverses */

/* Bad — keyframe animation for interactive element */
.drawer.open {
  animation: slideIn 200ms ease-out forwards;
}
/* Closing mid-animation snaps or restarts — feels broken */
```

### Enter Animations: Split and Stagger

Don't animate an entire container as one block. Break it into sections (title, description, buttons) with ~100ms stagger. For headlines, split into words at ~80ms. Combine `opacity: 0`, `translateY(8px)`, and `filter: blur(4px)`. Enter duration: 300-400ms.

**Motion (Framer Motion):**
```tsx
function PageHeader() {
  return (
    <motion.div
      initial="hidden"
      animate="visible"
      variants={{
        visible: { transition: { staggerChildren: 0.1 } },
      }}
    >
      <motion.h1
        variants={{
          hidden: { opacity: 0, y: 12, filter: "blur(4px)" },
          visible: { opacity: 1, y: 0, filter: "blur(0px)" },
        }}
      >
        Welcome
      </motion.h1>
      <motion.p
        variants={{
          hidden: { opacity: 0, y: 12, filter: "blur(4px)" },
          visible: { opacity: 1, y: 0, filter: "blur(0px)" },
        }}
      >
        A description of the page.
      </motion.p>
    </motion.div>
  );
}
```

**CSS-only stagger:**
```css
.stagger-item {
  opacity: 0;
  transform: translateY(8px);
  filter: blur(4px);
  animation: fadeInUp 400ms cubic-bezier(0.16, 1, 0.3, 1) forwards;
}
.stagger-item:nth-child(1) { animation-delay: 0ms; }
.stagger-item:nth-child(2) { animation-delay: 100ms; }
.stagger-item:nth-child(3) { animation-delay: 200ms; }

@keyframes fadeInUp {
  to {
    opacity: 1;
    transform: translateY(0);
    filter: blur(0);
  }
}
```

### Exit Animations

Exits should be softer than enters. Use a small fixed `translateY(-12px)` — not the full container height. Exit duration ~150ms, shorter than enter.

```tsx
/* Good — subtle exit */
<motion.div
  exit={{
    opacity: 0,
    y: -12,
    filter: "blur(4px)",
    transition: { duration: 0.15, ease: "easeIn" },
  }}
/>

/* Bad — dramatic exit that steals focus */
<motion.div
  exit={{
    opacity: 0,
    y: "-100%",
    scale: 0.5,
    transition: { duration: 0.4, ease: "easeIn" },
  }}
/>

/* Bad — no exit animation (element just vanishes) */
```

### Scale on Press

A subtle `scale(0.96)` on click gives buttons tactile feedback. Never use a value smaller than `0.95`.

```css
/* CSS */
.button {
  transition-property: scale;
  transition-duration: 150ms;
  transition-timing-function: ease-out;
}
.button:active {
  scale: 0.96;
}
```

```tsx
/* Motion */
<motion.button whileTap={{ scale: 0.96 }}>Click me</motion.button>
```

### Reduced Motion

- **Respect `prefers-reduced-motion`.** Always. Use `matchMedia` in GSAP or `@media (prefers-reduced-motion: reduce)` in CSS.

```css
@media (prefers-reduced-motion: reduce) {
  *, *::before, *::after {
    animation-duration: 0.01ms !important;
    animation-iteration-count: 1 !important;
    transition-duration: 0.01ms !important;
  }
}
```

### Performance

- **60fps is non-negotiable.** Animate only `transform` and `opacity` via CSS. Avoid animating `width`, `height`, `top`, `left`, `margin`, or `padding`.
- **Never use `transition: all`.** Always specify exact properties: `transition-property: scale, opacity, filter`.
- **Use `will-change` sparingly.** Only for `transform`, `opacity`, `filter` — properties the GPU can composite. Never `will-change: all`. Only add when you see first-frame stutter.

```css
/* Good — specific transition properties */
.card {
  transition-property: scale, opacity;
  transition-duration: 200ms;
  transition-timing-function: ease-out;
}

/* Bad — transition everything */
.card {
  transition: all 200ms ease-out;
}
```

| Property | GPU-compositable | Worth `will-change` |
|---|---|---|
| `transform` | Yes | Yes |
| `opacity` | Yes | Yes |
| `filter` (blur, brightness) | Yes | Yes |
| `clip-path` | Yes | Yes |
| `top`, `left`, `width`, `height` | No | No |
| `background`, `border`, `color` | No | No |

## Scroll Experience

Smooth scrolling is table stakes. The two dominant approaches:

**Lenis** — The modern default. Lightweight, performant, uses the native scrollbar. Locomotive Scroll v5 is built on top of it.
```js
const lenis = new Lenis({ duration: 1.2, easing: (t) => Math.min(1, 1.001 - Math.pow(2, -10 * t)) });
function raf(time) { lenis.raf(time); requestAnimationFrame(raf); }
requestAnimationFrame(raf);
```

**Locomotive Scroll v5** — A thin opinionated wrapper around Lenis adding in-view detection, progress tracking as CSS variables, and parallax via data attributes. 9.4kB gzipped.

**Scroll-triggered patterns:**
- Elements fading/sliding in as they enter the viewport (Intersection Observer or ScrollTrigger)
- Progress bars driven by scroll position (CSS custom properties updated on scroll)
- Parallax depth layers at different scroll speeds
- Horizontal scroll sections within a vertical page
- Pinned storytelling sequences (pin a section, scrub through its animation, then release)
