# 3D & WebGL

For projects that need 3D, Three.js is the standard. React Three Fiber (R3F) brings it into React's component model.

## Performance-First 3D

The top creative devs maintain blazing performance even with heavy shaders:

- **Matcaps over real-time lighting.** One of the most celebrated 3D web portfolios uses matcap materials that fake lighting with a single texture lookup — no light calculations needed. Massive performance win.
- **Baked lighting.** Pre-compute lighting in Blender and bake it into textures. The scene looks photorealistic but renders like a flat texture.
- **Draco compression** for mesh assets. Active Theory's site achieves 1.3s LCP despite heavy 3D by compressing meshes with Draco.
- **Lazy loading.** Load 3D assets after `requestIdleCallback`. Show a loading state or 2D fallback first.
- **LOD (Level of Detail).** Swap high-poly meshes for low-poly versions at distance or on mobile.
- **Instancing** for repeated geometry (particles, trees, buildings). `InstancedMesh` renders thousands of objects in a single draw call.
- **Compressed GLTF models** — Use `.glb` format. Always provide a static fallback for low-power devices.

## Shader Fundamentals

Custom GLSL shaders separate the top tier. Even basic knowledge enables:

- Noise-based distortion (curl noise, simplex noise, Perlin noise)
- SDF (Signed Distance Field) rendering for organic shapes
- Post-processing effects (bloom, chromatic aberration, film grain, vignette)
- Custom material effects (iridescence, holographic, liquid, glass refraction)

Lusion's work demonstrates the ceiling: they store SDF data in PNG textures (RGB for gradient normals, alpha for signed distance) and do GPU-based collision detection on 16K+ objects in real-time.

## Common 3D Patterns for Landing Pages

- **Floating 3D element in hero** — A single rotating product or abstract shape. Responds to cursor via subtle rotation.
- **Particle systems** — Thousands of points forming shapes, dispersing on interaction, reforming. GPU-driven via InstancedMesh or custom shaders.
- **Scroll-driven 3D camera movement** — Camera position/rotation tied to scroll. User "moves through" a 3D scene by scrolling.
- **Cursor-reactive 3D** — 3D objects that tilt, rotate, or deform based on mouse position. Use `mousemove` to calculate normalized coordinates and pass to shader uniforms.
- **3D text** — Extruded or beveled 3D typography. Use sparingly — one 3D headline, not an entire page.

## In Artifact Context

For React artifacts, Three.js is available via `import * as THREE from 'three'`. Use it for hero backgrounds, interactive elements, or full 3D scenes. Keep the 3D contained — a stunning 3D hero with clean 2D content below is more effective than 3D everywhere.

Note: `THREE.CapsuleGeometry` is NOT available in r128. Use `CylinderGeometry`, `SphereGeometry`, or create custom geometries instead.
