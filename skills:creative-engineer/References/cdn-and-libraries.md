# CDN & Library References

Quick-reference for available libraries when building standalone HTML artifacts or adding dependencies to projects.

## Animation

```html
<!-- GSAP core -->
<script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.5/gsap.min.js"></script>

<!-- GSAP plugins -->
<script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.5/ScrollTrigger.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.5/Flip.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.5/Draggable.min.js"></script>

<!-- Lottie (vector animation from After Effects) -->
<script src="https://cdnjs.cloudflare.com/ajax/libs/lottie-web/5.12.2/lottie.min.js"></script>
```

Note: GSAP SplitText is a Club plugin — not available via public CDN. For text splitting in standalone artifacts, split manually into `<span>` elements per word/character.

## 3D

```html
<!-- Three.js -->
<script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>
```

Note: `THREE.CapsuleGeometry` is NOT available in r128. Use `CylinderGeometry`, `SphereGeometry`, or custom geometries instead.

## Smooth Scroll

```html
<!-- Lenis -->
<script src="https://unpkg.com/lenis@1.1.18/dist/lenis.min.js"></script>
```

```js
const lenis = new Lenis({ duration: 1.2, easing: (t) => Math.min(1, 1.001 - Math.pow(2, -10 * t)) });
function raf(time) { lenis.raf(time); requestAnimationFrame(raf); }
requestAnimationFrame(raf);
```

## Fonts

Google Fonts — use the `<link>` approach for HTML artifacts:

```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=FONT_NAME:wght@400;500;700&display=swap" rel="stylesheet">
```

For critical fonts (hero headlines), preload the font file directly:

```html
<link rel="preload" href="https://fonts.gstatic.com/s/FONT_PATH.woff2" as="font" type="font/woff2" crossorigin>
```

Always use `font-display: swap` or `font-display: optional`.

## React Context

When building React artifacts, import directly — no CDN needed:

```js
import * as THREE from 'three';
import * as d3 from 'd3';
```

GSAP in React — use `useEffect` + `useRef`:

```jsx
const ref = useRef(null);
useEffect(() => {
  const ctx = gsap.context(() => {
    gsap.from(ref.current, { opacity: 0, y: 40, duration: 0.8 });
  }, ref);
  return () => ctx.revert();
}, []);
```

Motion (Framer Motion) in React:

```jsx
import { motion, AnimatePresence } from 'motion/react';

<motion.div
  initial={{ opacity: 0, y: 20 }}
  animate={{ opacity: 1, y: 0 }}
  exit={{ opacity: 0 }}
  transition={{ type: 'spring', duration: 0.5, bounce: 0 }}
/>
```
