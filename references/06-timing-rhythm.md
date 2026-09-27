# 06 Timing, Rhythm, Frequency Band Binding & Seam Continuity

This document establishes the timing architecture, acoustic frequency band binding, non-linear stagger falloffs, audio ducking, musical cadence, seam continuity laws, sustained motion rules, and loop seam physics.

---

## 1. Acoustic Frequency Band Binding (Audiovisual Resonance)

Audio cues must harmonize with the visual mass and frequency of the animated element:

| Frequency Band | Spectral Range | Visual Atom Binding | Physical Resonance |
| :--- | :--- | :--- | :--- |
| **`low-sub`** | `20Hz – 120Hz` | Heavy container impacts (`squash-impact`), camera rumbles, hero card arrivals | Deep chest resonance, ground mass |
| **`mid-snap`** | `500Hz – 2.5kHz`| UI card flips, button clicks, state toggles, variable font weight snaps | Crisp tactile feedback, ear clarity |
| **`high-air`** | `6kHz – 14kHz` | Specular light sweeps (`effects.light-sweep`), particle bursts, stroke draws | Shimmering luxury, sparkling finish |

---

## 2. Non-Linear Stagger Falloff Distributions

| Stagger Curve | Formula | Visual Dynamic |
| :--- | :--- | :--- |
| **`stagger-linear`** | $d_i = i \cdot s$ | Predictable sequential cascades |
| **`stagger-exponential`**| $d_i = \text{base} \cdot (1.20)^i$ | Fast initial cluster decelerating into a relaxed tail |
| **`stagger-gaussian`** | $d_i = d_{\text{max}} \cdot \exp\left(-\frac{(i - c)^2}{2\sigma^2}\right)$ | Symmetrical ripple fanning out from the focal anchor |
| **`stagger-fibonacci`** | $d_i = F(i) \cdot s$ | Organic golden-ratio acceleration |

---

## 3. Rhythmic Syncopation & Musical Cadence

- **`syncopated-burst`:** `Fast (120ms) → Fast (120ms) → Deliberate Hold (400ms) → Heavy Payoff (600ms)`.
- **`polyrhythmic-offset`:** Primary layer on 3-beat rhythm; background accents on 2-beat counterpoint.
- **`triplet-accent`:** `Short → Short → Long` (`60ms - 60ms - 240ms`) with accent on the 3rd unit.
- **`staccato-resolve`:** Rapid crisp snaps followed by an elongated, weighted deceleration.

---

## 4. Audio Frequency Ducking & Sonic Hit Sync

During major visual and sonic impacts (hero `sfx-sub` or crucial VO claim line), background ambient audio and micro-ticks MUST be dynamically ducked:
$$\text{ambient\_audio\_volume} \mathrel{-}= 6\text{dB}\quad (\text{attack: } 40\text{ms},\; \text{release: } 300\text{ms})$$

---

## 5. Seamless Loop Physics (The Zero-Velocity Hitch Law)

For `Piece Type: Loop` (e.g., ambient hero backgrounds, continuous loaders, Rive state loops), the loop boundary must be mathematically imperceptible:

$$\vec{v}_{\text{exit}}(\text{Frame } N) = \vec{v}_{\text{entry}}(\text{Frame } 0)$$

1. **Velocity Derivative Continuity:** Motion must not decelerate to zero and restart abruptly at the loop seam.
2. **Phase Boundary Matching:** Property values at `t = 0.0s` and `t = total_duration` must be identical with slope-matched easing curves.

---

## 6. The Seam Law & Continuity (Inter-Scene Transitions)

### The Vector Law
> **How Scene A exits dictates how Scene B enters:** same axis, same direction, matched velocity, cut mid-motion on both sides.

1. **Axis Continuity:** X stays X, Y stays Y, Z stays Z. Never switch axes abruptly at a cut.
2. **Directional Continuity:** Never mirror direction. If Scene A exits to the left, Scene B enters from the right moving left.
3. **Speed Matching (`Cut-The-Curve`):** Exit final velocity ≈ Entry initial velocity. Scene B enters at ≥50% through its notional path rather than starting from a dead stop.
4. **Zero Dead Beats:** The cut occurs mid-motion on both sides.

### Cinematic Montage Grammar
Beyond simple vector slides, use intentional editing cuts:
1. **Match Cut (`transition.match-cut`):** Scene A ends on an object that shares exact geometric silhouette, color, or coordinate anchor with Scene B's entering hero (e.g., circular search button morphs into expanding radial chart).
2. **Smash Cut (`transition.smash-cut`):** High-velocity energy cut on a climax impact without intermediate settling, slamming directly into the resolved payload.
3. **Occlusion Wipe (`transition.occlusion-wipe`):** A large passing foreground element acts as a natural shutter, wiping the screen to reveal the next environment.
4. **Concrete Carriers (`transition.morph-dock`):** A physical object (card, cursor, keyword) travels across the cut to anchor the viewer's eye into the new layout slot.

### Causal Motion (Action & Reaction Chain)
`Click → Squash → Spring Release → Flight → Impact → Recoil → Reveal`. Reactions ignite on the exact causing frame.

---

## 7. No Idle Wobble & Sustained Motion Routes

Idle sine wave loops (breathe, float, drift) are **STRICTLY BANNED**. Every span between entrance and exit is owned by a purposeful route:
- **Staged Reveals** · **Camera with Intent** · **Sequenced UI Life** · **Animated Sequences** · **Cursor-Led Action**

---

## 8. Stillness Before Climax (The Dramatic Comma)

Before any major climax, transformation, or punchline, insert a **0.3s – 0.75s deliberate pause**.

---

## 9. Whip Cut Vector Angle Matching

When utilizing high-velocity whip transitions across scenes:
- Exit trajectory angle must match entry trajectory angle:
  $$\theta_{\text{exit}} = \theta_{\text{entry}} \pm 0.0^{\circ}$$
- Motion blur streak orientation in Scene A must seamlessly align with Scene B entrance streaks to prevent visual disorientation.

---

## 10. Audio Mix Stem Architecture & Dynamic Headroom

Audio choreography must designate sound events into discrete mix stems:

| Mix Stem | Dynamic Priority | Typical Elements | Headroom Policy |
| :--- | :--- | :--- | :--- |
| **`stem-vo`** | Highest (0dB reference) | Voiceover claim lines, spoken narrative | Sits on top; triggers -6dB ducking on all other stems |
| **`stem-sfx-hero`** | High (-2dB) | Climax sub-bass hits (`sfx-sub`), impact punches | Uncompressed transients; ducks ambient bed |
| **`stem-foley-ui`** | Medium (-8dB) | Micro-clicks, card flips, variable font ticks | Crisp high-air transient; zero low-end mud |
| **`stem-bed-atmos`**| Low (-14dB to -20dB) | Continuous drone, atmospheric room tone | Dynamically ducks during VO and hero impacts |

---

## 11. Focus Handoff Anchoring (%70 Settle Rule)

To protect visual cognitive continuity and prevent saccadic eye fatigue:
- When transitioning focal emphasis between two UI elements or scenes, the currently active hero anchor must reach **$\ge 70\%$ of its settle hold** before the next element begins its acceleration trajectory.
- Never trigger simultaneous competing entrances on opposite sides of the viewport.
