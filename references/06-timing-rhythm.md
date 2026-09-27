# 06 Timing, Rhythm, Audio Sync & Seam Continuity

This document establishes the timing architecture, audio/SFX hit point synchronization, seam continuity laws (cross-scene cuts), and sustained motion rules.

---

## 1. Audio & Sonic Hit Synchronization (Sonic Motion)

Sound and vision are co-dependent: audio provides weight and tactical clarity to visual keyframes.

### Sonic Hit Rules:
1. **Zero Audio Lag:** SFX triggers must land on the **exact frame** of initial visual contact, impact, or trigger ignition.
2. **Audio Cue Types:**
   - **`whoosh` / `air-rush`:** Attached to high-velocity seam transitions along the Current.
   - **`impact` / `sub-bass`:** Triggered when the hero focal anchor locks into its final resting position.
   - **`click` / `mechanical-tick`:** Triggered upon state changes (`pressed`, `toggle`).
   - **`riser` / `tension-swell`:** Placed during Anticipation (recoil) leading up to a major climax.
   - **`chime` / `resolution`:** Triggered on completion of a data count-up or goal achievement.
3. **Voiceover (VO) Pacing:** If a voiceover track is present, scene keyframes and word reveals must lock to actual word timestamp boundaries, not arbitrary slots.

---

## 2. The Seam Law & Continuity (Inter-Scene Transitions)

A multi-scene animation must feel like **ONE continuous flow**, not a disconnected stack of slides.

### The Vector Law
> **How Scene A exits dictates how Scene B enters:** same axis, same direction, matched velocity, cut mid-motion on both sides.

1. **Axis Continuity:** X stays X, Y stays Y, Z stays Z. Never switch axes abruptly at a cut.
2. **Directional Continuity:** Never mirror direction. If Scene A exits to the left, Scene B enters from the right moving left.
3. **Speed Matching (`Cut-The-Curve`):** Exit final velocity ≈ Entry initial velocity. Scene B enters at ≥50% through its notional path rather than starting from a dead stop.
4. **Zero Dead Beats:** The cut occurs mid-motion on both sides. Do not wait for Scene A to fully stop before Scene B starts.

### Concrete Carriers
The eye follows physical objects, not abstract dissolves. The strongest scene transitions pass a **concrete carrier** across the cut:
- A floating card docking into the next scene's grid.
- An interactive cursor clicking an element and leading the eye into the new viewport.
- A hero mark or word group expanding to become the next scene's header.
- **Never use crossfades as a lazy default**—crossfades have zero carrier continuity.

### Causal Motion (Nedensellik)
Chain movements so each action visibly triggers the next:
- `Click → Squash → Spring Release → Flight → Impact → Recoil → Reveal`.
- Reactions must ignite on the **exact causing frame**, not with an awkward delay.

---

## 3. No Idle Wobble & Sustained Motion Routes

Idle sine wave loops (breathe, float, drift, pulsing glow to fill time) are **STRICTLY BANNED** as sustained motion. They signal to the viewer that the animation has stalled.

Every duration between entrance and exit must be assigned one of these **Sustained Motion Routes**:

| Route | Mechanism | When to Use |
| :--- | :--- | :--- |
| **Staged Reveals** | Information is held back and revealed in rhythm with narration/reading beats. | Multi-bullet lists, feature cards |
| **Camera with Intent** | Mapped pan/zoom path: Establish wide → Travel → Arrive on detail. | Large dashboards, spatial canvas |
| **Sequenced UI Life** | Product behaves realistically: Progress advances, counter ticks, tabs switch. | Product demos, SaaS workflows |
| **Animated Sequences** | Physical assembly: Cards stack, items sort, graph lines draw. | Data stories, infographics |
| **Cursor-Led Action** | A cursor guides the eye to an interactive trigger, igniting the next beat. | UI tutorials, interactive previews |

---

## 4. Orchestration Modes

1. **Sequential:** Unit B starts only when Unit A completes (`delayB = delayA + durationA`).
2. **Overlapping (Standard):** Unit B starts when Unit A is at **60–70% completion**.
3. **Parallel:** Units A and B launch on the same frame with distinct durations/curves.
4. **Cascade / Stagger:** Sequential delay added per item in a collection (`30–80ms`).

---

## 5. Tempo Classifications

| Tempo | Character | Duration Scale | Stagger Scale | Target Application |
| :--- | :--- | :--- | :--- | :--- |
| `staccato` | Sharp, snappy | `100–200ms` | `30–50ms` | Micro-interactions, toggles, icon flips |
| `allegro` | Energetic, crisp | `200–350ms` | `50–80ms` | Interactive apps, kinetic typography |
| `moderato` | Balanced, readable | `350–500ms` | `80–120ms` | Standard landing pages, explainer videos |
| `adagio` | Cinematic, luxurious | `500–800ms` | `120–200ms` | Luxury brand showcases, hero openers |
| `glacial` | Ambient evolution | `2000ms+` | None | Background shaders, depth atmosphere |

---

## 6. Stillness Before Climax (The Dramatic Comma)

Before any major climax, transformation, or punchline, insert a **0.3s – 0.75s deliberate pause**.
This stillness creates anticipation, focuses the viewer's gaze, and amplifies the impact of the payoff.
