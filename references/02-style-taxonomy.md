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

## 2. Motion Categories Master Catalog

Select the primary format category for the piece:

| Category Key | Display Name | Narrative Intent | Primary Matter | Default Tempo / Cadence | Signature Atoms | Settle Hold |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **`kinetic-type`** | Kinetic Typography | High-impact claim, manifesto, quote sting | `Type` | `allegro` / `syncopated-burst` | `type.tracking-breath`, `clip-reveal-left` | `0.5s – 0.8s` |
| **`stat-count`** | Hero Metric & Counter | Key KPI count-up, radial gauge, percentage ring | `Data` | `moderato` / `staccato-resolve` | `counter-up`, `physics.momentum-transfer` | `0.6s – 1.0s` |
| **`data-charts`** | Financial & Data Graphics | Multi-series bar, line path, candlestick, area charts | `Data` | `moderato` / `polyrhythmic-offset` | `vector.path-draw`, `vector.trim-offset` | `0.6s – 0.8s` |
| **`product-ui-feature`**| SaaS & Product Feature | Interactive feature walkthrough, modal, card morphs | `UI / Product` | `moderato` / `syncopated-burst` | `transition.morph-dock`, `slide-in-up` | `0.4s – 0.6s` |
| **`logo-reveal-sting`** | Brand Ident & Logo Sting | Signature brand mark ignition, optical reveal | `Mark` | `adagio` / `triplet-accent` | `effects.light-sweep`, `effects.glow-flare` | `0.8s – 1.2s` |
| **`hardware-3d-showcase`**| 2.5D/3D Hardware Tour | Hardware specs, 3D orbit, depth plane layering | `Material` | `adagio` / `moderato` | `camera.dolly-in`, `transition.orbit-axial-flip`| `0.8s – 1.0s` |
| **`social-story-reel`** | 9:16 Vertical Story | High-velocity hook, thumb-stopping vertical reveal | `Type` / `UI` | `allegro` / `staccato` | `transition.whip-pan`, `scale-pop` | `0.3s – 0.5s` |
| **`lower-thirds-overlay`**| Keynote & Broadcast HUD | Speaker name badge, streaming status HUD | `UI / Product` | `moderato` / `staccato-resolve` | `clip-reveal-left`, `vector.minimal-line-wipe` | `1.5s – 3.0s` |
| **`isometric-flowchart`**| Architecture & Node Piping| Cloud data piping, server flow, network nodes | `Grid / Architecture`| `moderato` / `polyrhythmic-offset` | `vector.path-follow`, `particles.directional-flow` | `0.6s – 0.8s` |
| **`liquid-asset-morph`** | Fluid Asset Transformation | Organic shape shifting, brand asset deformation | `Fluid / Liquid`| `slow` / `adagio` | `liquid.blob-morph`, `liquid.surface-tension-merge` | `0.6s – 0.8s` |
| **`onboarding-carousel`**| Guided Card Carousel | Multi-step interactive onboarding walkthrough | `UI / Product` | `velocity_gesture` | `physics.hysteresis-settle`, `transition.morph-dock` | `User-driven` |
| **`celebration-burst`** | Gamification & Reward | Achievement unlock, badge pop, celebratory burst | `Material` | `allegro` / `syncopated-burst` | `particles.radial-burst`, `scale-pop` | `0.6s – 0.8s` |

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

### 7. Editorial Luxury
- **Intent:** High-fashion, premium craftsmanship, timeless authority.
- **Pacing:** `adagio` (600–1200ms) with viscous overdamped settling ($\zeta = 1.40$).
- **Optics & Typography:** `lens-macro-85`, `bokeh-f1.4-circular`, serif variable weight morphing, subtle specular sweeps (`effects.light-sweep`), `feather-soft` masks.
- **Typical Atoms:** `type.weight-morph`, `effects.light-sweep`, `physics.hysteresis-settle`.

### 8. Brutalist Raw
- **Intent:** Unapologetic high-energy impact, counter-culture, high-density rhythm.
- **Pacing:** `staccato` (60–150ms), hard cuts, zero-easing stepped transitions (`steps(1)`).
- **Optics & Typography:** `blur-disabled` (0° Shutter), `feather-none` (hard SVG edges), heavy grotesque display fonts, inverted ink/ground flashes.
- **Typical Atoms:** `typewriter-in`, `scale-pop`, `split-reveal-h`.

### 9. Tactile Glass & Spatial Material
- **Intent:** Tangible 2.5D physical depth, translucent spatial UI, glassmorphism.
- **Pacing:** `moderato` (300–450ms) with spring dynamics ($\zeta = 0.70$).
- **Optics & Material:** Refraction index ($n = 1.52$), chromatic aberration (`split_offset: micro`), dynamic contact shadow pinch (`shadow-contact-pinch`), 2.5D layer tilt.
- **Typical Atoms:** `effects.frosted-glass-refract`, `effects.chromatic-aberration`, `camera.dolly-in`.

### 10. Fintech Precision & Technical HUD
- **Intent:** Institutional confidence, high-velocity analytics, algorithmic clarity.
- **Pacing:** `allegro` (150–300ms) with critically damped settling ($\zeta = 1.00$).
- **Optics & Typography:** `bokeh-f2.8-hexagonal`, tabular monospace numeric counters, vector ghost trails (`effects.vector-trail`), crisp UI lines.
- **Typical Atoms:** `counter-up`, `draw-in`, `effects.vector-trail`.

---

## 4. Style Selection Decision Matrix

```text
Is text the primary argument?
  ├── YES
  │     ├── Is it luxury/editorial? ──> 'editorial-luxury' + 'Type' matter
  │     ├── Is it counter-culture/punchy? ──> 'brutalist-raw' + 'Type' matter
  │     └── Standard kinetic story? ──> 'kinetic-type' + 'Kinetic Typography'
  └── NO
       ├── Is it a product or UI demonstration?
       │     ├── 2.5D translucent tactile glass? ──> 'tactile-glass' + 'UI/Product'
       │     └── Standard web feature? ──> 'webpage-ui' or 'Product Showcase'
       └── Is it numerical or analytical?
             ├── High-velocity data/metrics? ──> 'fintech-precision' + 'Data'
             └── General chart/infographic? ──> 'stat-count' or 'data-charts'
```
