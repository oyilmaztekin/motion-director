# 10 Master Storyboard Template (Hybrid Markdown + YAML)

This document defines the definitive deliverable template produced by `motion-director`. It combines human-readable narrative tables, audio synchronization points, and a machine-verifiable, engine-agnostic YAML specification.

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
   - *Optical Event:* [The primary optical event in effect]
   - *Sonic Hit:* [Corresponding audio cue]
3. **Final Settle Hold ([total]s — The Resting State):**
   - *Composition:* [The final resolved layout and CTA during the terminal hold]

---

## 2. Beat-by-Beat Choreography & Sonic Table

| Beat | Timestamp | Still Composition & Safe Zone | Motion, Atom & Camera | Origin & Path | Carrier Across Seam | Audio / SFX Cue | Hold / Negative Time | Narrative Why |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **01** | `0.0s - 0.6s` | Ground established, Hero headline | `clip-reveal-left` [Settle] | `origin-left-center`<br>`direct-axis` | Headline text line | `sfx-whoosh` (air rush) | `0.4s hold` | Establish core claim |
| **02** | `1.0s - 1.8s` | Data card emerges (Midground) | `slide-in-up` [Anticipation] + `camera.dolly-in` | `origin-bottom-center`<br>`arc-convex` | Card border | `sfx-riser` (tension) | `0.6s hold` | Evidence payload |
| **03** | `2.4s - 3.2s` | Metric counts to 99% + Squash impact | `counter-up` + `squash-impact` | `origin-center`<br>`volume-preserve` | Signal accent ring | `sfx-sub` (bass hit) | `0.8s hold` | Climax payoff |

---

## 3. Timeline Overview (ASCII)

```text
[0.0s] ───|-- ground/bg (continuous) ----------------------------------->|
[0.0s]    |-- headline [0.6s clip-reveal] --[0.4s hold]--|
[1.0s]          |-- data-card [0.8s slide-in + dolly] --[0.6s hold]--|
[2.4s]                |-- metric-counter [0.8s count] --[0.8s final hold]--|
[Audio]   [whoosh @0.0s] ───────── [riser @1.0s] ─────── [sub-bass @2.4s]
```

---

## 4. Master Specification (Strict Engine-Agnostic YAML)

```yaml
meta:
  project: "[Project Name]"
  piece_type: "timed" # timed | interactive | loop
  driver: "clock" # clock | scroll_scrub | velocity_gesture
  category: "kinetic-type"
  total_duration: "3.5s"
  tempo: "moderato"
  current_vector: "left"
  primary_matter: "Type"
  formats: ["16:9", "9:16"]
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
    spatial_path: "direct-axis"
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
      stagger: { type: "from-start", amount: 60ms }
      variable_font: { axis: "wght", from: 300, to: 800 }
    audio_cue:
      type: "whoosh"
      cue: "sfx-whoosh"
      at: 0ms
    reduced_motion:
      fallback: "entrance.fade-in"
      duration: "fast"

  - id: "data-card"
    element: "div.metric-card"
    z: 20
    depth_plane: "midground"
    matter: "Data"
    transform_origin: "origin-bottom-center"
    spatial_path: "arc-convex"
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
    anticipation:
      recoil: { translateY: "4px", scaleY: 0.95, scaleX: 1.05 } # Volume preserved
      duration: "fast"
    camera:
      dolly_z: { from: 0, to: "40px" }
    carrier:
      element: "div.metric-card"
      target_slot: "next-scene-dock"
    audio_cue:
      type: "swell"
      cue: "sfx-riser"
      at: 1000ms
    reduced_motion:
      fallback: "entrance.fade-in"
      duration: "fast"
```
```
