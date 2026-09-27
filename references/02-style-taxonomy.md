# 02 Motion Style Taxonomy & The Current

This document defines the core motion styles, categorized forms, and overarching directional currents used to structure visual rhythm and scene choreography.

---

## 1. The Current & Reserved Vectors (Directional Law)

Every motion piece must establish **ONE dominant directional flow** (The Current). The default is **`+X` (Left-to-Right)** or **`+Z` (Forward / Camera Push)**.

### Vector Rules:
- **The Current:** Neutral forward narrative progression. 80%+ of standard scene transitions and object entrances must follow this dominant axis (`+X` or `+Z`).
- **Reserved Vectors (Meaningful exceptions — max 20%):**
  - **Upward (`-Y`):** Elevation, ascension, revelation, rising above the context, positive delta.
  - **Downward (`+Y`):** Grounding, gravity, drawer drop, settling into reality.
  - **Z-Forward (`+Z` / Zoom-Through):** Drilling deeper into the exact same thought, micro-inspection, penetrating a boundary.
  - **Z-Backward (`-Z` / Inverse Zoom):** Arrival of something massive, panoramic context, zooming out to take in the whole picture.
  - **Scale-Burst (Blasting outward):** Breaking through a boundary, exiting a world, explosive climax.
  - **Horizontal Return (`-X`):** Historical review, backward step, undo, memory recoil.
- **Rotational Vectors:**
  - **Clockwise (`+R` / `cw` $\circlearrowright$):** Positive progression, time advancing, fastening, gear engagement.
  - **Counter-Clockwise (`-R` / `ccw` $\circlearrowleft$):** Time rewinding, unfastening, disengaging, cycle inversion.
- **Anti-Ping-Pong Rule:** Never reverse directions across consecutive seams without a visible, physically grounded **Causal Force**:
  1. *Elastic Wall Bounce:* Object strikes an off-screen/on-screen bounding barrier and rebounds.
  2. *Direct User Gesture:* Interactive swipe/drag reverse, cursor grab, or scroll direction change.
  3. *Narrative Chapter Shift:* Full-bleed color wash, optical whip, or blackout separating narrative acts.
- **RTL / LTR Automatic Symmetry Matrix:** For Right-to-Left locales (Arabic, Hebrew, Persian, Urdu), standard `+X` forward vector automatically inverts to `-X` (Right-to-Left), mirroring visual hierarchy and clip reveals horizontally, while `Y` and `Z` axes remain invariant.

### 1.1 The 6 Canonical Spatial Axes & Kinetic Intent
| Vector Axis | Spatial Direction | Narrative & Kinetic Intent | Default Easing / Spring | Energy State |
| :--- | :--- | :--- | :--- | :--- |
| **`+X` (Right)** | Horizontal Forward | Narrative progress, reading flow (LTR), chronological forward time | `ease-out-cubic` / `spring-snappy` | Kinetic forward |
| **`-X` (Left)** | Horizontal Return | Historical review, backward step, undo, memory recoil | `ease-in-out-cubic` / `spring-gentle`| Kinetic reverse |
| **`-Y` (Up)** | Vertical Ascension | Elevation, ambition, status unlock, revelation, positive delta | `spring-bouncy` / `ease-out-quart` | Potential energy high |
| **`+Y` (Down)** | Vertical Gravity | Weight, anchor, grounding, drawer drop, settling into reality | `ease-out-back` / `spring-gentle` | Gravitational anchor |
| **`+Z` (Forward / Push)**| Depth Penetration | Deep-dive focus, micro-inspection, breaking through boundary | `ease-in-out-quint` / `spring-snappy` | Concentrated focus |
| **`-Z` (Backward / Pull)**| Panoramic Reveal | Macro context, zoom-out, arrival of massive structure, exit | `ease-out-expo` / `spring-gentle` | Environmental context |

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
- **Intent:** Simplifying complex concepts, pedagogical clarity, sequential narrative unfolding.
- **Pacing & Dynamics:** `moderato` (300–500ms), slightly underdamped ($\zeta = 0.85$, $e = 0.15$), rhythm linked to spoken cadence (110–125 WPM), explicit 600ms holds for comprehension.
- **Optics, Matter & Typography:** `Vector` & `UI / Product` matter, `lens-normal-50`, clean geometric flat/gradient shaders, geometric sans-serif (Inter, Plus Jakarta Sans) with generous line-height ($1.5\times$).
- **Signature Atoms & Transitions:** `slide-in-up`, `vector.path-draw`, `transition.morph-dock`, `counter-up`, `transition.iris-wipe`.
- **Audio Stem Pairing:** `stem-vo` priority (leads motion triggers), playful UI micro-pops on reveals (`stem-sfx-hero`), light acoustic/warm synth bedding (`stem-music`).

### 2. Product Showcase
- **Intent:** High-fidelity hardware or software digital feature presentation, tactile elevation.
- **Pacing & Dynamics:** Deliberate `adagio` (500–900ms), critically damped settling ($\zeta = 0.95$, $e = 0.05$), micro-stagger ($25\text{ms}$).
- **Optics, Matter & Typography:** `Material` & `UI / Product` matter, `lens-macro-85`, `bokeh-f1.8-circular`, subtle specular sweeps (`effects.light-sweep`), contact shadow pinches, clean neo-grotesque type.
- **Signature Atoms & Transitions:** `scale-up`, `camera.dolly-in`, `transition.orbit-axial-flip`, `effects.light-sweep`, `physics.momentum-transfer`.
- **Audio Stem Pairing:** Deep low-end whooshes (`stem-sfx-hero`), metallic sheen accents, spacious cinematic pads (`stem-ambient`), -6dB ducking on macro spec reveals.

### 3. Kinetic Typography
- **Intent:** Text is the hero; pure typographic rhythm, manifestos, high-impact claims.
- **Pacing & Dynamics:** `allegro` / `staccato` (100–300ms), critically damped ($\zeta = 1.00$), syncopated syllable bursts, tight staggers ($15–30\text{ms}$).
- **Optics, Matter & Typography:** `Type` matter, high APCA contrast ($L^c > 85$), variable font optical weight & width morphs, zero-descender clipping masks, bold condensed grotesque or expressive display serif.
- **Signature Atoms & Transitions:** `type.weight-morph`, `type.tracking-breath`, `clip-reveal-left`, `transition.match-cut-type`, `transition.whip-pan`.
- **Audio Stem Pairing:** Per-syllable riser/impact sync, aggressive transient clicks (`stem-sfx-hero`), driving bassline syncopation (`stem-music`).

### 4. Minimalist Motion Graphics
- **Intent:** Swiss design precision, mathematical purity, zero decorative fluff, functional clarity.
- **Pacing & Dynamics:** `moderato` (200–400ms), critically damped ($\zeta = 1.00$, $e = 0.00$), pure linear or exact cubic easings (`ease-out-cubic`).
- **Optics, Matter & Typography:** `Vector` & `Grid / Architecture` matter, `lens-normal-50`, monochrome or duo-tone palette, rigid 8pt baseline grid alignment, pure geometric typography (Helvetica, Neue Haas Grotesk).
- **Signature Atoms & Transitions:** `clip-reveal-left`, `vector.minimal-line-wipe`, `fade-in`, `vector.path-draw`, `transition.cut-straight`.
- **Audio Stem Pairing:** Dry tactile mechanical clicks & ticks (`stem-sfx-hero`), subtle room tone (`stem-ambient`), minimal rhythmic pulse (`stem-music`).

### 5. Mixed Media & Collage
- **Intent:** Layering tangible textures, torn paper, 3D objects, typography, analog grain, and photography.
- **Pacing & Dynamics:** Dynamic variable cadence (`rubato`, 120–450ms bursts), stepped frame rates (`steps(2)` / 12fps posterize feel), zero intermediate smoothing.
- **Optics, Matter & Typography:** `Layered / Collage` matter, analog 35mm grain, halftone screens, chromatic aberration, torn paper edge alpha mattes, eclectic mixed serif + brutalist mono pairing.
- **Signature Atoms & Transitions:** `parallax-shift`, `blend-mode-cycle`, `shake-x`, `transition.dissolve-dither`, `effects.chromatic-aberration`.
- **Audio Stem Pairing:** Textured vinyl crackle, paper tearing/rustle SFX, vintage camera shutter clicks (`stem-sfx-hero`), lo-fi acoustic or tape-saturated music (`stem-music`).

### 6. Shader & Generative Atmosphere
- **Intent:** Continuous mathematical fluid evolution, volumetric ambient depth, hypnotic digital landscapes.
- **Pacing & Dynamics:** `glacial` (1500–4000ms+), heavily overdamped ($\zeta = 1.50$), continuous sinusoidal or noise-driven perpetual flow.
- **Optics, Matter & Typography:** `Fluid / Liquid` & `Ambient / Atmospheric` matter, volumetric raymarching, subsurface scattering, organic gradient mesh deformation, ultra-light geometric typography.
- **Signature Atoms & Transitions:** `gradient-cycle`, `noise-evolution`, `fluid-distortion`, `liquid.blob-morph`, `transition.dissolve-cross`.
- **Audio Stem Pairing:** Deep binaural drones, resonant sub-bass washes (`stem-ambient`), granular texture pads (`stem-music`), zero transient sharp SFX.

### 7. Editorial Luxury
- **Intent:** High-fashion, premium craftsmanship, haute horlogerie, timeless prestige, museum-grade calm.
- **Pacing & Dynamics:** `adagio` (600–1200ms), viscous overdamped settling ($\zeta = 1.40$, $e = 0.00$), slow graceful deceleration.
- **Optics, Matter & Typography:** `Material` & `Type` matter, `lens-macro-85`, `bokeh-f1.4-circular`, high-contrast Didone / editorial variable serifs, soft specular glints (`effects.light-sweep`), `feather-soft` edge masking.
- **Signature Atoms & Transitions:** `type.weight-morph`, `effects.light-sweep`, `physics.hysteresis-settle`, `camera.dolly-in`, `transition.portal-z-zoom`.
- **Audio Stem Pairing:** Warm orchestral strings, delicate acoustic grand piano (`stem-music`), silk fabric foley & soft glass resonance (`stem-sfx-hero`), wide acoustic air (`stem-ambient`).

### 8. Brutalist Raw
- **Intent:** Unapologetic high-energy impact, counter-culture, high-density industrial rhythm.
- **Pacing & Dynamics:** `staccato` (60–150ms), hard zero-duration cuts (`steps(1)`), high-frequency staggers ($8–16\text{ms}$).
- **Optics, Matter & Typography:** `Type` & `Material` matter, `blur-disabled` (0° Shutter), `feather-none` (hard SVG edges), ultra-black grotesque display type, flashing color inversions.
- **Signature Atoms & Transitions:** `typewriter-in`, `scale-pop`, `split-reveal-h`, `transition.whip-pan`, `transition.smear-frame`.
- **Audio Stem Pairing:** Industrial metallic impacts, distortion risers, clipped transients (`stem-sfx-hero`), aggressive fast-tempo breakbeat / electronic (`stem-music`).

### 9. Tactile Glass & Spatial Material
- **Intent:** Tangible 2.5D physical depth, translucent spatial UI layers, Apple-grade visionOS tactile glassmorphism.
- **Pacing & Dynamics:** `moderato` (300–450ms), spring dynamics ($\zeta = 0.70$, $k = 180$), elastic hover reaction.
- **Optics, Matter & Typography:** `UI / Product` & `Material` matter, physical refraction index ($n = 1.52$), micro chromatic aberration, contact shadow pinch, real-time specular bevel reflection.
- **Signature Atoms & Transitions:** `effects.frosted-glass-refract`, `effects.chromatic-aberration`, `camera.dolly-in`, `transition.morph-dock`, `physics.momentum-transfer`.
- **Audio Stem Pairing:** Resonant crystal taps, clean glass clinks, smooth pneumatic air suctions (`stem-sfx-hero`), modern spatial electronic pads (`stem-ambient`).

### 10. Fintech Precision & Technical HUD
- **Intent:** Institutional confidence, high-velocity analytics, algorithmic transparency, real-time market telemetry.
- **Pacing & Dynamics:** `allegro` (150–300ms), critically damped settling ($\zeta = 1.00$, $e = 0.00$), precise sequential polyrhythms.
- **Optics, Matter & Typography:** `Data` & `Grid / Architecture` matter, `bokeh-f2.8-hexagonal`, tabular monospace numeric counters, vector ghost trails (`effects.vector-trail`), sub-pixel grid lines.
- **Signature Atoms & Transitions:** `counter-up`, `vector.path-draw`, `effects.vector-trail`, `transition.iris-wipe`, `vector.trim-offset`.
- **Audio Stem Pairing:** High-frequency digital clicks, terminal chirp blips, data stream ticks (`stem-sfx-hero`), subtle neutral low drone (`stem-ambient`).

### 11. Dark Mode Linear & Neo-SaaS
- **Intent:** Modern B2B software authority (Linear, Stripe, Raycast aesthetic), razor-sharp developer tool prestige, hyper-clean technical elegance.
- **Pacing & Dynamics:** `moderato` (250–400ms), critically damped settling ($\zeta = 1.00$, $e = 0.00$), buttery bezier transitions (`ease-out-quart`).
- **Optics, Matter & Typography:** `UI / Product` & `Grid / Architecture` matter, `#0a0a0c` OLED background, 1px sub-pixel luminous neon borders, subtle linear gradient sweeps (`effects.light-sweep`), crisp neo-grotesque (Inter, Geist Sans).
- **Signature Atoms & Transitions:** `effects.light-sweep`, `vector.minimal-line-wipe`, `transition.morph-dock`, `slide-in-up`, `vector.path-draw`.
- **Audio Stem Pairing:** Soft acoustic key clicks, subtle high-frequency synthetic hum (`stem-sfx-hero`), deep atmospheric sub-bass pad (`stem-ambient`).

### 12. Playful 3D Clay & Tactile Joy
- **Intent:** Warm consumer onboarding, gamification, humanized accessibility, tactile joy (Duolingo, Headspace, Pitch style).
- **Pacing & Dynamics:** `allegro` / `bouncy` (350–550ms), underdamped spring physics ($\zeta = 0.55$, $k = 240$, $e = 0.35$), prominent overshoot and squash-and-stretch.
- **Optics, Matter & Typography:** `Material` & `Fluid / Liquid` matter, matte clay shading (zero specular gloss, soft ambient occlusion), saturated pastel palette, rounded friendly sans-serif (Fredoka, Nunito).
- **Signature Atoms & Transitions:** `scale-pop`, `transition.elastic-pop-through`, `physics.momentum-transfer`, `particles.radial-burst`, `liquid.blob-morph`.
- **Audio Stem Pairing:** Organic bubble pops, rubber plops, wooden xylophone/marimba accents (`stem-sfx-hero`), upbeat acoustic/whimsical groove (`stem-music`).

### 13. Cinematic Monolith & Trailer
- **Intent:** High-stakes filmic gravity, keynote openers, monumental brand statements, Hans Zimmer-grade slow-burn drama.
- **Pacing & Dynamics:** `lento` / `adagio` (800–2500ms), heavy overdamped physics ($\zeta = 1.60$, $e = 0.00$), monolithic slow-moving momentum.
- **Optics, Matter & Typography:** `Material` & `Type` matter, volumetric haze/fog (`fog: rayleigh-atmospheric`), anamorphic lens flare (`effects.glow-flare`), 3D depth field push, heavy wide-tracked serif or monolithic sans (`tracking: +0.20em`).
- **Signature Atoms & Transitions:** `camera.dolly-in`, `transition.portal-z-zoom`, `type.tracking-breath`, `effects.glow-flare`, `transition.dissolve-cross`.
- **Audio Stem Pairing:** Monumental low-end sub-drop (30Hz), brass braam hits, rising strings crescendo (`stem-music`), epic cinematic whooshes (`stem-sfx-hero`).

### 14. Cyber HUD & Retro Glitch
- **Intent:** Futuristic telemetry, cyberpunk / anime terminal interfaces, sci-fi military HUD, retro CRT computing.
- **Pacing & Dynamics:** `staccato` / `erratic` (50–180ms), stepped zero-easing pulses (`steps(1)` / `steps(3)`), micro-staggers ($10\text{ms}$).
- **Optics, Matter & Typography:** `Data` & `Type` matter, CRT phosphor scanlines, RGB chromatic displacement (`effects.chromatic-aberration`), wireframe grids, monospaced terminal fonts (JetBrains Mono, Fira Code).
- **Signature Atoms & Transitions:** `typewriter-in`, `effects.vector-trail`, `effects.chromatic-aberration`, `transition.smear-frame`, `counter-up`.
- **Audio Stem Pairing:** High-pitch modem chirps, electrical static buzz, relays, digitized Geiger clicks (`stem-sfx-hero`), fast industrial drum & bass or synthwave (`stem-music`).

---

## 4. Style Selection Decision Matrix

```text
What is the primary visual anchor and medium?
  ├── Typography is the hero:
  │     ├── Luxury / prestige narrative? ──────────────> [7] Editorial Luxury
  │     ├── Monumental filmic gravity / trailer? ──────> [13] Cinematic Monolith & Trailer
  │     ├── Counter-culture / raw industrial? ─────────> [8] Brutalist Raw
  │     └── Expressive statement / manifesto? ─────────> [3] Kinetic Typography
  ├── Product & UI demonstration:
  │     ├── Modern dark-mode B2B SaaS (Linear/Stripe) ─> [11] Dark Mode Linear & Neo-SaaS
  │     ├── 2.5D spatial glass / tactile depth? ───────> [9] Tactile Glass & Spatial Material
  │     ├── Premium hardware / hero 3D tour? ──────────> [2] Product Showcase
  │     └── Educational / feature explainer? ──────────> [1] Explainer Animation
  ├── Data, Logic & Telemetry:
  │     ├── Sci-fi HUD / cyberpunk / retro terminal ───> [14] Cyber HUD & Retro Glitch
  │     ├── High-velocity financial telemetry ─────────> [10] Fintech Precision & Technical HUD
  │     └── Pure Swiss functional graphics / charts ───> [4] Minimalist Motion Graphics
  └── Experimental, Physical & Ambient:
        ├── Tactile warm 3D clay / playful bouncy UI ──> [12] Playful 3D Clay & Tactile Joy
        ├── Analog textures / paper / mixed media ─────> [5] Mixed Media & Collage
        └── Perpetual fluid / algorithmic landscapes ──> [6] Shader & Generative Atmosphere
```
