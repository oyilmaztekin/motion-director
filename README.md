# 🎬 Motion Director (`motion-director`)

> **The Definitive Studio-Grade Motion Choreographer & Storyboarding Skill for Autonomous AI Agents.**  
> *Engine-Agnostic Physics · 18-Point Pre-Flight Validation · Hybrid Markdown & YAML Storyboards.*

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Engine Agnostic](https://img.shields.io/badge/Engine-GSAP%20%7C%20After%20Effects%20%7C%20Rive%20%7C%20CSS-orange.svg)](#-downstream-engine-handoff)
[![Color Space](https://img.shields.io/badge/Color-Polar%20OKLCH-purple.svg)](references/01-design-dna.md)
[![Accessibility](https://img.shields.io/badge/A11y-WCAG%20AAA%20Reduced%20Motion-green.svg)](references/08-cross-platform.md)
[![Quality Gates](https://img.shields.io/badge/Gates-18--Point%20Pre--Flight-brightgreen.svg)](SKILL.md)

---

## ⚡ What is Motion Director?

**Motion Director** is an executive-level motion design and storyboarding intelligence. It bridges the critical gap between abstract creative vision and frame-accurate technical execution.

Instead of writing fragmented, fragile implementation code, **Motion Director** generates mathematically rigorous, studio-grade hybrid storyboards (`STORYBOARD.md`) that downstream developers and motion designers can translate effortlessly into **Web (GSAP/CSS/Framer)**, **Video (After Effects)**, or **Interactive Rive/Lottie** state machines.

```text
               ┌────────────────────────────────────────────────────────┐
               │              🎨 CREATIVE VISION / BRIEF                │
               └───────────────────────────┬────────────────────────────┘
                                           │
                                           ▼
               ┌────────────────────────────────────────────────────────┐
               │        🎬 MOTION DIRECTOR (Physical Storyboard)        │
               │  • Single Focal Anchor      • Viscous Hysteresis (ζ)   │
               │  • G2 Continuous Tangent    • 4-Stem Audio Ducking     │
               │  • Vector Seam QA Matrix    • Strict YAML Specification│
               └───────┬───────────────────┬───────────────────┬────────┘
                       │                   │                   │
                       ▼                   ▼                   ▼
            ┌──────────────────┐  ┌─────────────────┐  ┌───────────────┐
            │  🌐 WEB RUNTIME  │  │  🎥 AFTER FX    │  │  🕹️ RIVE 2D   │
            │  GSAP / CSS /    │  │  3D Camera /    │  │  State Mach.  │
            │  Framer Motion   │  │  Shape Paths    │  │  Inputs/Bones │
            └──────────────────┘  └─────────────────┘  └───────────────┘
```

---

## 🏛️ The 5 Immutable Core Laws

Every animation produced by `motion-director` strictly enforces foundational physics:

1. **Staging & Focal Anchor:** Exactly one primary focal anchor per frame. Competing simultaneous actions are banned to eliminate cognitive fatigue (`Density Budget: max 1 High-Energy + 2 Secondary`).
2. **Anticipation & Volume Conservation:** Physical mass is established via micro counter-momentum before launch. Volume is strictly preserved:
   $$\text{scaleX} \times \text{scaleY} \approx 1.0$$
3. **Viscous Hysteresis & Damping Ratio ($\zeta$):** Springs dissipate energy through calibrated damping:
   - **Underdamped ($\zeta = 0.70$):** High-energy punch with subtle tactile overshoot.
   - **Critically Damped ($\zeta = 1.00$):** Fastest possible arrival with zero overshoot (UI cards, modals).
   - **Overdamped ($\zeta = 1.40$):** Heavy viscous settling for massive luxury hero elements.
4. **Spatial Arcs, G2 Continuity & Tangent Lock:** Trajectories follow natural gravitational curves with zero radial jerk and collinear keyframe handles (`tangent_lock: continuous-g2`).
5. **Settle & Focus Handoff (%70 Rule):** Elements decelerate into rest (`decay`). The active hero must complete **$\ge 70\%$ of its settle hold** before the next focal target accelerates.

---

## 🔬 Studio-Grade Optical & Sonic Intelligence

- **Perceptual Polar OKLCH Color Space:** Color tweens interpolate in polar OKLCH space to eliminate desaturated gray dead-zones, verified against **APCA Perceptual Contrast** ($\ge L^c 75$ body / $\ge L^c 60$ hero).
- **Camera Optics & Bokeh Geometry:** Real-world lens focal lengths (`24mm` to `135mm`), aperture blade shapes (`f1.4-circular`, `f2.8-hexagonal`, `anamorphic`), and multiplane parallax speed multipliers ($v_{\text{fg}}=1.80 \dots v_{\text{bg}}=0.20$).
- **4-Stem Audio Mix Architecture:** Dynamic headroom routing (`stem-vo`, `stem-sfx-hero`, `stem-foley-ui`, `stem-bed-atmos`) with automatic **-6dB ambient ducking** on climax impacts.
- **Dynamic Contact Shadows:** Contact shadow pinch (`0px 2px 4px rgba(0,0,0,0.5)`) on surface contact expanding into diffuse atmospheric elevation during flight.
- **Typographic Optical Precision:** Optical cap-height alignment (zero baseline hop), kinetic kerning collision guards, descender mask padding (`{top: 0.15em, bottom: 0.25em}`), and automatic **RTL Flow Inversion** (`current_vector: RIGHT`).

---

## 🚀 The 6-Phase Production Pipeline

All project specifications are written to disk under `motion-director/<slug>/` with strict phase-by-phase lock gates:

```text
Phase 0: BRIEF.md       ──>  Intent, Matter, Driver Model, Cadence, Target Formats
Phase 1: DIRECTION.md   ──>  Concept & Signature Move
Phase 2: DIRECTION.md   ──>  Design DNA, Still Poster, Color Roles & Token Library
Phase 3: DIRECTION.md   ──>  Motion Vocabulary, Atoms, Camera Optics & Blend Modes
Phase 4: DIRECTION.md   ──>  Scene Spine, Negative Time Holds & Audio Sync
Phase 5: STORYBOARD.md  ──>  Master Hybrid Deliverable (Narrative + Seam QA + YAML)
```

---

## 📋 The Master Storyboard Deliverable (`STORYBOARD.md`)

Every completed storyboard provides a complete blueprint:

```markdown
# Motion Storyboard: SaaS Dashboard — Climax Reveal

## 1. Proof-Frames (The 3 Paused Stills)
- **0.0s (Opening Poster):** Dark OKLCH ground, hero headline masked at rest.
- **2.4s (Climax Payoff):** 2.5D Metric card elevated with hexagonal bokeh rack focus.
- **3.5s (Final Settle):** CTA locked, contact shadow pinched, complete rest hold.

## 2. Beat Choreography & Sonic Table
| Beat | Timestamp | Motion Atom & Camera | Origin & Path | Blend & Mask | Audio Cue & Stem | Hold | Narrative Why |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **01** | `0.0s - 0.6s` | `clip-reveal-left` + `tracking-breath` | `origin-left-center`<br>`direct-axis` | `blend-normal`<br>`feather-soft` | `sfx-whoosh`<br>(stem-foley-ui) | `0.4s` | Establish claim |
| **02** | `1.0s - 1.8s` | `slide-in-up` + `effects.light-sweep` | `origin-bottom-center`<br>`arc-convex (G2)` | `blend-overlay`<br>`shadow-pinch` | `sfx-riser`<br>(stem-foley-ui) | `0.6s` | Evidence payload |
| **03** | `2.4s - 3.2s` | `counter-up` + `particles.radial-burst` | `origin-center`<br>`volume-preserve` | `blend-screen`<br>`bokeh-f2.8` | `sfx-sub`<br>(stem-sfx-hero, -6dB duck) | `0.8s` | Climax payoff |

## 3. Timeline Overview (ASCII)
[0.0s] ───|-- ground (continuous) ----------------------------------------------------->|
[0.0s]    |-- headline [0.6s clip-reveal + breath] --[0.4s hold]--|
[1.0s]          |-- data-card [0.8s slide-in + light-sweep] --[0.6s hold]--|
[2.4s]                |-- celebration-burst [0.8s burst] --[0.8s final settle hold]------>|
[Audio]   [whoosh @0.0s] ─────────── [riser @1.0s] ───────── [sub-bass @2.4s (duck -6dB)]

## 4. Master Specification (Strict Engine-Agnostic YAML)
```yaml
meta:
  project: "SaaS Dashboard"
  piece_type: "timed"
  driver: "clock"
  direction: "ltr"
  total_duration: "3.5s"
  color_space: "oklch"
  density_budget: { max_high_energy: 1, max_secondary: 2 }

layers:
  - id: "hero-headline"
    matter: "Type"
    atom: "entrance.clip-reveal-left"
    apca_contrast: "Lc-82"
    tangent_lock: "continuous-g2"
    mask_optical_padding: { top: "0.15em", bottom: "0.25em" }
    audio_cue: { cue: "sfx-whoosh", mix_stem: "stem-foley-ui", at: "0ms" }
    reduced_motion: { fallback: "entrance.fade-in", duration: "fast" }

  - id: "data-card"
    matter: "Data"
    atom: "entrance.slide-in-up"
    physics: { damping_ratio: 0.70, hysteresis_damping: "natural-asymmetric" }
    shadow: { contact_pinch: true, elevation_falloff: "shadow-elevation-air" }
    camera: { dolly_z: "40px", fov: "lens-cine-35", bokeh: "bokeh-f2.8-hexagonal" }
    audio_cue: { cue: "sfx-riser", mix_stem: "stem-foley-ui", at: "1000ms" }
    reduced_motion: { fallback: "entrance.fade-in", duration: "fast" }
```
```

---

## 🛠️ Downstream Engine Handoff

| Storyboard Token / Feature | Web (GSAP 3 / CSS / Framer) | Video (After Effects) | Interactive (Rive 2D) |
| :--- | :--- | :--- | :--- |
| **`spring-snappy` ($\zeta=0.7$)** | Framer `{damping: 14, stiffness: 200}` | Expression `freq=3.5; decay=7.0;` | Spring (`mass: 1, stiff: 200, damp: 14`) |
| **`vector.path-draw`** | GSAP `DrawSVGPlugin` (`"0% 100%"`) | Shape Layer `Trim Paths` (`0% → 100%`) | Vector Path Trim Constraint |
| **`vector.path-follow`** | CSS `offset-path: path(...)` | Layer `Auto-Orient along Path` | Path Constraint Follower |
| **`liquid.blob-morph`** | SVG `<feGaussianBlur>` + ColorMatrix | `CC Simple Choker` + Fast Box Blur | Vertex Skinning & Bone Morphing |
| **`color_space: oklch`** | CSS `color-mix(in oklch, ...)` | 32bpc Float Working Space | Standard Vector Color Transition |
| **Timeline Markers** | GSAP Timeline Labels (`tl.addLabel(...)`) | Composition Markers (`M_CLIMAX_BURST`) | State Machine Input Triggers |

---

## 📚 Reference Modules

| Reference File | Subject & Scope |
| :--- | :--- |
| [**`01-design-dna.md`**](references/01-design-dna.md) | 13 Core Physics Laws, APCA Contrast, OKLCH, Contact Shadows & Origins |
| [**`02-style-taxonomy.md`**](references/02-style-taxonomy.md) | 10 Motion Styles, The Current Dominant Vector & Decision Matrix |
| [**`03-atomic-motions.md`**](references/03-atomic-motions.md) | Complete Motion Atom Library (Entrance, Exit, Vector, Liquid, Camera) |
| [**`04-text-treatments.md`**](references/04-text-treatments.md) | Typographic Choreography, Variable Fonts, Kerning Guards & RTL Inversion |
| [**`05-visual-effects.md`**](references/05-visual-effects.md) | Lens FOV (24-135mm), Bokeh Geometry, Parallax Multipliers & Ray Fog |
| [**`06-timing-rhythm.md`**](references/06-timing-rhythm.md) | Syncopation, 4-Stem Audio Routing, -6dB Climax Ducking & %70 Focus Handoff |
| [**`07-state-machines.md`**](references/07-state-machines.md) | Clock/Scroll/Gesture Drivers, Ballistic Fling Decay & Fitts 44px Cushion |
| [**`08-cross-platform.md`**](references/08-cross-platform.md) | Aspect Ratios (16:9, 9:16, 1:1), WCAG AAA Reduced Motion & 120Hz $\Delta t$ |
| [**`09-technology-map.md`**](references/09-technology-map.md) | Master Translation Dictionary for GSAP 3, CSS, After Effects & Rive |
| [**`10-storyboard-template.md`**](references/10-storyboard-template.md) | Master Hybrid Markdown + Strict YAML Storyboard Deliverable Schema |

---

## 💻 Installation & Usage

To use `motion-director` in your workspace or agent environment:

1. Clone or symlink this directory into your agent skills path:
   ```bash
   git clone https://github.com/your-username/motion-director.git ~/.agents/skills/motion-director
   ```
2. Prompt your agent to plan any motion piece:
   ```text
   Use /motion-director to storyboard a 4-second B2B SaaS dashboard feature reveal.
   ```
3. The agent will autonomously execute Phase 0 (`BRIEF.md`), iterate through `DIRECTION.md`, and output the final production-ready `STORYBOARD.md`.

---

## 📄 License

MIT © [Motion Director Contributors](LICENSE)
