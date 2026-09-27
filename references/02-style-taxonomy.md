# 02 Motion Style Taxonomy & The Current

This document defines the core motion styles, categorized forms, and overarching directional currents used to structure visual rhythm and scene choreography.

---

## 1. The Current & Reserved Vectors (Directional Law)

Every motion piece must establish **ONE dominant directional flow** (The Current). Default is **LEFT** (or Forward Z).

### Vector Rules:
- **The Current:** Neutral forward narrative progression. 80%+ of standard scene transitions must follow this axis.
- **Reserved Vectors (Meaningful exceptions):**
  - **Upward:** Elevation, ascension, revelation, rising above the context.
  - **Z-Forward (Zoom-Through):** Drilling deeper into the exact same thought or detail.
  - **Z-Backward (Inverse Zoom):** Arrival of something massive or taking in the whole picture.
  - **Scale-Burst (Blasting outward):** Breaking through a boundary / exiting a world.
- **Anti-Ping-Pong Rule:** Never reverse directions across consecutive seams without a visible causal force (such as an impact, button click, or chapter marker).

---

## 2. Motion Categories

Select the primary format category:

| Category | Intent | Key Characteristics |
| :--- | :--- | :--- |
| **`kinetic-type`** | Punchy claim, title, kinetic quote | Type scale, ink/ground contrast, staggered word arrival |
| **`stat-count`** | Hero metric / count-up + ring/bar | Number interpolation, signal accent, settle hold |
| **`data-charts`** | Bar, line, radial, area data hit | Path drawing, sequential bar rises, quiet chrome |
| **`logo-reveal`** | Brand ident / signature sting | Mask reveal, optical highlight, single signature settle |
| **`lower-thirds`** | Name / title / UI overlay badge | Mask slide-in, restrained secondary motion, clean exit |
| **`webpage-ui`** | Product walkthrough, state change | Cursor anticipation, card morphs, shared element travel |
| **`asset-fusion`** | Geometric asset morphs into chart/data | Morph-shape, seamless coordinate transformation |

---

## 3. Style Catalog & Characteristics

### 1. Explainer Animation
- **Intent:** Simplifying complex concepts through sequential visual storytelling.
- **Pacing:** `moderato` (300–500ms) with explicit holds for voiceover / reading.
- **Typical Atoms:** `slide-in-up`, `morph-shape`, `clip-reveal-up`, `counter-up`.

### 2. Product Showcase
- **Intent:** High-fidelity hardware or software digital feature presentation.
- **Pacing:** Deliberate `adagio` (500–800ms) with macro focus.
- **Typical Atoms:** `scale-up`, `parallax-shift`, `rotate-in`, `glow-pulse`.

### 3. Kinetic Typography
- **Intent:** Text is the hero; rhythm and emotion driven by typographic scaling.
- **Pacing:** `allegro` / `staccato` (100–350ms) with tight stagger.
- **Typical Atoms:** `split-reveal-horizontal`, `typewriter-in`, `scale-pop`, `blur-in`.

### 4. Minimalist Motion Graphics
- **Intent:** Swiss design precision, zero decorative fluff, functional clarity.
- **Pacing:** `moderato` / `staccato` with exact mathematical easings.
- **Typical Atoms:** `clip-reveal-left`, `slide-in-up`, `fade-in`, `draw-in`.

### 5. Mixed Media & Collage
- **Intent:** Layering textures, 3D, typography, and photography.
- **Pacing:** Dynamic, variable bursts (`rubato`).
- **Typical Atoms:** `parallax-shift`, `blend-mode-cycle`, `shake-x`.

### 6. Shader & Generative Atmosphere
- **Intent:** Fluid, mathematical continuous background evolution.
- **Pacing:** `glacial` (2000ms+) with linear or ultra-soft sinusoidal flow.
- **Typical Atoms:** `gradient-cycle`, `noise-evolution`, `fluid-distortion`.

---

## 4. Style Selection Decision Matrix

```text
Is text the primary argument?
  ├── YES ──> Choose 'kinetic-type' + 'Kinetic Typography' style
  └── NO
       ├── Is it a product or UI demonstration?
       │     ├── YES ──> Choose 'webpage-ui' or 'Product Showcase'
       │     └── NO
       │          ├── Is it numerical or analytical?
       │          │     ├── YES ──> Choose 'stat-count' or 'data-charts'
       │          │     └── NO  ──> Choose 'Explainer' or 'Minimalist'
```
