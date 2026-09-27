# 10 Master Storyboard Template (Hybrid Markdown + YAML)

This document defines the definitive deliverable template produced by `motion-director`. It combines human-readable narrative tables, audio synchronization points, vector seam validation matrices, timeline marker manifests, and a machine-verifiable, engine-agnostic YAML specification.

---

## Storyboard Document Template (`STORYBOARD.md`)

```markdown
# Motion Storyboard: [Project Name] — [Scene / Piece Title]

**Status:** locked
**Audience:** [Target Audience]
**Core Message:** This piece tells [audience] that [message].
**Style:** [Style Name from 02-style-taxonomy]
**Primary Matter:** [Type | UI/Product | Data | Material | Mark]
**Driver Model:** [clock | scroll_scrub | velocity_gesture]
**The Current:** [LEFT | RIGHT | FORWARD-Z]
**Color Space:** OKLCH (Perceptual)
**Pixel Snapping:** dynamic_integer_lock
**Lens FOV:** [lens-cine-35 | lens-macro-85 | lens-neutral-50]
**Bokeh Geometry:** [bokeh-f1.4-circular | bokeh-f2.8-hexagonal | bokeh-anamorphic]
**Rhythmic Cadence:** [syncopated-burst | polyrhythmic-offset | triplet-accent]
**Target Formats:** [16:9 widescreen, 9:16 vertical reels, 1:1 square]
**Signature Move:** [The single memorable kinetic mechanism]

---

## 1. Proof-Frames (The 3 Canonical Paused Stills)

1. **Opening State (0.0s — The Poster):**
   - *Composition:* [Description of focal point, ink vs ground, hierarchy before motion begins]
   - *Safe Zone:* [Checked for 16:9 and 9:16 safe framing]
   - *Why it reads paused:* [How the still states the message without animation]
2. **Signature Climax Frame ([t]s — The Payoff):**
   - *Composition:* [The peak moment of transformation or reveal]
   - *Optical Event:* [Primary optical event / specular sheen / chromatic split]
   - *Sonic Hit & Ducking:* [Corresponding audio cue + ducking level]
3. **Final Settle Hold ([total]s — The Resting State):**
   - *Composition:* [The final resolved layout and CTA during the terminal hold]

---

## 2. Beat-by-Beat Choreography & Sonic Table

| Beat | Timestamp | Still Composition & Safe Zone | Motion, Atom & Camera | Origin & Path | Blend & Mask | Carrier Across Seam | Audio Cue, Band & Ducking | Hold / Negative Time | Narrative Why |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **01** | `0.0s - 0.6s` | Ground established, Hero headline | `clip-reveal-left` [Settle] + `type.tracking-breath` | `origin-left-center`<br>`direct-axis` | `blend-normal`<br>`feather-soft` | Headline text line | `sfx-whoosh`<br>(mid-snap) | `0.4s hold` | Establish core claim |
| **02** | `1.0s - 1.8s` | Data card emerges (Midground) | `slide-in-up` [Anticipation] + `camera.dolly-in` | `origin-bottom-center`<br>`arc-convex (G2)` | `effects.light-sweep`<br>`blend-overlay` | Card border | `sfx-riser`<br>(high-air) | `0.6s hold` | Evidence payload |
| **03** | `2.4s - 3.2s` | Metric counts to 99% + Burst | `counter-up` + `physics.momentum-transfer` | `origin-center`<br>`volume-preserve` | `blend-screen`<br>`depth-fog-cool` | Signal accent ring | `sfx-sub`<br>(low-sub, -6dB duck) | `0.8s hold` | Climax payoff |

---

## 3. Vector Seam Continuity Matrix (Inter-Scene QA)

| Seam # | Cut Time | Scene A Exit Vector | Scene B Entry Vector | Carrier Element | Velocity Continuity | Vector Law Status |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **Seam 1→2** | `0.8s` | `X: -100vw (left)` | `X: +100vw → 0 (left)` | Headline Text Group | Matched mid-motion (≥50%) | **PASS (Vector Matched)** |
| **Seam 2→3** | `2.0s` | `Z: push-forward (+40px)` | `Z: scale-up (push-forward)` | Metric Card Frame | Matched scale-velocity sign | **PASS (Z-Sign Matched)** |

---

## 4. Timeline Markers & Production Handoff Manifest

| Marker Name | Timestamp | Trigger Type | AE Comp Marker | Rive Input Trigger | GSAP Label |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `M_INTRO_START` | `0.0s` | Auto Scene Ignition | `Intro_Start` | `trig_start` | `introStart` |
| `M_HEADLINE_LOCK` | `0.6s` | Audio Hit / Tracking Lock | `Headline_Lock` | `state_headline_locked` | `headlineLock` |
| `M_DATA_REVEAL` | `1.0s` | Card Dolly & Light Sweep | `Data_Reveal` | `trig_data_reveal` | `dataReveal` |
| `M_CLIMAX_BURST` | `2.4s` | Sub-Bass Hit / Ducking | `Climax_Burst` | `trig_climax` | `climaxBurst` |
| `M_FINAL_SETTLE` | `3.2s` | Complete Rest Hold | `Final_Settle` | `state_settled` | `finalSettle` |

---

## 5. Timeline Overview (ASCII)

```text
[0.0s] ───|-- ground/bg (continuous) ----------------------------------->|
[0.0s]    |-- headline [0.6s clip-reveal + breath] --[0.4s hold]--|
[1.0s]          |-- data-card [0.8s slide-in + dolly] --[0.6s hold]--|
[2.4s]                |-- metric-counter [0.8s count + burst] --[0.8s final hold]--|
[Audio]   [whoosh @0.0s] ───────── [riser @1.0s] ─────── [sub-bass @2.4s (duck -6dB)]
```

---

## 6. Master Specification (Strict Engine-Agnostic YAML)

```yaml
meta:
  project: "[Project Name]"
  piece_type: "timed" # timed | interactive | loop
  driver: "clock" # clock | scroll_scrub | velocity_gesture
  category: "kinetic-type"
  total_duration: "3.5s"
  tempo: "moderato"
  cadence: "syncopated-burst"
  current_vector: "left"
  color_space: "oklch"
  pixel_snapping: "dynamic_integer_lock"
  lens_fov: "lens-cine-35"
  bokeh_iris: "bokeh-f1.4-circular"
  primary_matter: "Type"
  formats: ["16:9", "9:16"]
  density_budget: { max_high_energy: 1, max_secondary: 2 }
  signature_move: "[Description of signature mechanism]"

tokens:
  durations:
    fast: 200ms
    normal: 350ms
    slow: 600ms
  easings:
    ease-out-expo: "cubic-bezier(0.16, 1, 0.3, 1)"
    spring-snappy: { mass: 1, stiffness: 200, damping: 20 }
  spatials:
    small: 8px
    normal: 16px
    large: 32px

layers:
  - id: "hero-headline"
    element: "h1.claim"
    z: 10
    depth_plane: "midground"
    matter: "Type"
    transform_origin: "origin-left-center"
    vertical_alignment: "cap-height-centered"
    spatial_path: "direct-axis"
    path_continuity: "G2-smooth"
    blend_mode: "blend-normal"
    mask_feather: "feather-soft"
    motion_blur: "blur-disabled"
    atom: "entrance.clip-reveal-left"
    timing:
      delay: 0ms
      duration: "slow"
      easing: "ease-out-expo"
      hold_after: 400ms
    properties:
      clipPath: { from: "inset(0 100% 0 0)", to: "inset(0 0 0 0)" }
      opacity: { from: 0, to: 1 }
    text_treatment:
      level: "line"
      stagger: { type: "from-start", amount: 60ms, curve: "stagger-exponential" }
      variable_font: { axis: "wght", from: 300, to: 800 }
      kerning_guard: "dynamic-pair-protection"
      tracking_breath: { in_flight: "0.06em", at_rest: "-0.02em" }
    audio_cue:
      type: "whoosh"
      cue: "sfx-whoosh"
      frequency_band: "mid-snap"
      mix_stem: "stem-foley-ui"
      at: 0ms
    reduced_motion:
      fallback: "entrance.fade-in"
      duration: "fast"

  - id: "data-card"
    element: "div.metric-card"
    z: 20
    depth_plane: "midground"
    parallax_multiplier: 0.55
    matter: "Data"
    transform_origin: "origin-bottom-center"
    spatial_path: "arc-convex"
    path_continuity: "G2-smooth"
    blend_mode: "blend-overlay"
    motion_blur: "shutter-180"
    atom: "entrance.slide-in-up"
    timing:
      delay: 1000ms
      duration: "slow"
      easing: "ease-out-expo"
      hold_after: 600ms
    properties:
      translateY: { from: "var(--spatial-large)", to: "0px" }
      opacity: { from: 0, to: 1 }
    shadow:
      contact_pinch: true
      elevation_falloff: "shadow-elevation-air"
    effects:
      - type: "effects.light-sweep"
        angle: "135deg"
        timing: { delay: 1200ms, duration: "normal" }
      - type: "effects.chromatic-aberration"
        split_offset: "micro"
    anticipation:
      recoil: { translateY: "4px", scaleY: 0.95, scaleX: 1.05 } # Volume preserved
      duration: "fast"
    physics:
      momentum_transfer: { target: "div.adjacent-badge", recoil: "-6px" }
      hysteresis_damping: "natural-asymmetric"
      damping_ratio: 0.70 # Underdamped punch
    camera:
      dolly_z: { from: 0, to: "40px" }
      fov: "lens-cine-35"
      bokeh: "bokeh-f1.4-circular"
    carrier:
      element: "div.metric-card"
      target_slot: "next-scene-dock"
    audio_cue:
      type: "swell"
      cue: "sfx-riser"
      frequency_band: "high-air"
      mix_stem: "stem-foley-ui"
      at: 1000ms
    reduced_motion:
      fallback: "entrance.fade-in"
      duration: "fast"

  - id: "celebration-burst"
    element: "canvas.particles"
    z: 30
    depth_plane: "foreground"
    parallax_multiplier: 1.80
    blend_mode: "blend-screen"
    atom: "particles.radial-burst"
    timing:
      delay: 2400ms
      duration: "fast"
    properties:
      count: 20
      spread: "360deg"
      gravity: 0.4
    audio_cue:
      type: "impact"
      cue: "sfx-sub"
      frequency_band: "low-sub"
      mix_stem: "stem-sfx-hero"
      at: 2400ms
      ducking: "-6dB"
    reduced_motion:
      fallback: "none"
```
```
