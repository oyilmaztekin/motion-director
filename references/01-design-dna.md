# 01 Design DNA, Physics Laws, Perceptual Color & Material Dynamics

This document establishes the foundation of the project's motion identity, matter composition, perceptual color interpolation, pixel snapping standards, physics laws, driver models, spatial origin standards, material friction, mathematical easing curves, and motion density budgets. All scene specifications and storyboards must reference the tokens and rules defined here.

---

## 1. The Core Motion & Physics Laws

Every animated scene produced by `motion-director` must satisfy these foundational laws:

1. **Staging & Single Focal Anchor:**
   - Every frame has exactly ONE primary focal point (anchor). Visual hierarchy, secondary elements, and camera framing exist solely to guide the eye toward it.
2. **Motion Density Budget:**
   - At any given timestamp, the composition may contain:
     - **At most ONE High-Energy Hero Action** (e.g., major card entrance, hero title reveal, dramatic camera push).
     - **At most TWO Low-Energy Secondary Actions** (e.g., subtle particle drift, specular light sheen, background counter tick).
   - Violating this budget causes cognitive visual fatigue.
3. **Perceptual Color Space & APCA Contrast Law:**
   - Color transitions and gradient morphs MUST interpolate in polar perceptual color space (**OKLCH** or **CIELAB**).
   - Standard sRGB interpolation creates desaturated, muddy gray dead-zones midway through transitions. OKLCH preserves constant chroma and perceived luminosity throughout the entire tween.
   - **APCA Contrast Conformance:** Dynamic typography moving over backgrounds or blurred surfaces must maintain minimum Accessible Perceptual Contrast Algorithm levels:
     - **Body Text / Micro-Labels:** $\ge L^c 75$ contrast.
     - **Hero Headlines / Display Claims:** $\ge L^c 60$ contrast.
4. **Pixel Snapping & Sub-Pixel Anti-Aliasing Guard:**
   - Dynamic motion uses smooth sub-pixel float coordinates during transit.
   - Upon arriving at any **Hold or Rest state**, all coordinates and dimensions MUST snap to whole integer pixels (`Math.round`) to prevent edge fuzziness and shimmering artifacts.
5. **Anticipation & Volume Conservation (Squash & Stretch Law):**
   - Major actions must be preceded by a micro counter-momentum or compression.
   - **Conservation of Volume:** When an object compresses or stretches, its 2D area/volume must remain constant:
     $$\text{scaleX} \times \text{scaleY} \approx 1.0$$
6. **Viscous Hysteresis & Asymmetric Spring Dissipation:**
   - Physical mass does not oscillate symmetrically. Energy dissipates through asymmetric viscous damping:
     $$\text{Overshoot } (60\%) \longrightarrow \text{Rebound } (20\%) \longrightarrow \text{Micro-Settle } (3\%) \longrightarrow \text{Locked Rest}$$
7. **Spatial Arcs, G2 Curvature Continuity & Continuous Tangent Lock:**
   - Organic motion never travels along robotic diagonal vectors. Trajectories follow natural gravitational curves (`arc-convex` or `arc-concave`) with **G2 Curvature Continuity** (continuous acceleration derivative across path joins, zero radial jerk).
   - **Continuous Tangent Lock (`tangent_lock: continuous-g2`):** Bezier control handles at keyframe joins must remain collinear ($\theta_{\text{in}} = \theta_{\text{out}}$) to eliminate spatial kinks and unnatural velocity spikes.
8. **Harmonic Oscillation & Damping Ratio ($\zeta$):**
   - Every physical spring must declare its dimensionless damping ratio ($\zeta$):
     - **Underdamped ($\zeta = 0.70$):** High-energy punch, subtle tactile overshoot.
     - **Critically Damped ($\zeta = 1.00$):** Fastest possible arrival with zero overshoot (UI cards, modal dialogs).
     - **Overdamped ($\zeta = 1.40$):** Heavy viscous settling for massive luxury hero objects.
9. **Dynamic Contact Shadows & Elevation Physics:**
   - As an object rises along the Z-axis, its shadow expands in radius and diffuses in opacity ($Z \uparrow \implies \text{radius} \uparrow,\; \text{alpha} \downarrow$).
   - Upon landing, the shadow pinches into a tight, dark contact line (`contact-shadow-pinch`).
10. **Material Drag & Aerodynamic Friction ($\mu$):**
    - High-velocity bodies experience environmental drag. Particles and cards decelerate proportional to their aerodynamic profile ($\vec{F}_{\text{drag}} = -\mu \vec{v}$).
11. **Elastic Restitution & Momentum Transfer:**
    - High-mass arrivals transfer kinetic energy to adjacent low-mass elements proportionally ($m_1 v_1 = m_2 v_2$) with calibrated restitution coefficient ($e$).
12. **Asymmetric Easing:**
    - `linear` interpolation is banned except for infinite ambient cycles or raw progress bars.
    - Organic motion requires asymmetric curves: aggressive acceleration (`ease-in`) paired with a long, gentle deceleration/settle (`ease-out`), or mass-damped springs.
13. **Follow-Through & Overlapping Action:**
    - Elements never lock into place on the exact same frame. Secondary layers, attached badges, shadows, and text settle with a 50–150ms delay/offset relative to the primary hero.
14. **Focus Handoff Anchoring (%70 Settle Rule):**
    - When transferring viewer attention across scenes or layers, the current primary focal anchor must complete **$\ge 70\%$ of its settle hold** before the next focal target begins accelerating.
15. **Kinetic Hierarchy & Motion Magnitude Ratio ($1.0 : 0.35 : 0.10$):**
    - Simultaneous layer displacements must strictly observe energy scaling:
      - **Primary Hero Action ($1.0\times$):** Full travel distance / scale transformation (Commands 100% of eye tracking).
      - **Secondary Supporting Layer ($\le 0.35\times$):** Badges, shadows, adjacent cards move at $\le 35\%$ the hero's travel distance.
      - **Ambient / Micro Accent ($\le 0.10\times$):** Grain modulation, micro-ticks, light sheen move at $\le 10\%$ displacement.

---

## 2. Materiality, Mass & Surface Physics

Objects in motion possess physical weight, surface friction, and restitution:

| Material Class | Mass Multiplier | Aerodynamic Drag ($\mu$) | Restitution Coefficient ($e$) | Typical Elements | Visual Character |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **`material-heavy`** | `2.00` | `0.45` (Viscous) | `0.15` (Low bounce) | Metal containers, modal windows, hero 3D hardware | Authoritative, massive, overdamped |
| **`material-medium`**| `1.00` | `0.85` (Standard air) | `0.50` (Tactile spring) | UI cards, data widgets, buttons, typography blocks | Snappy, responsive, crisp |
| **`material-light`** | `0.25` | `0.95` (High resistance)| `0.80` (Bouncy) | Notification badges, spark particles, cursor indicators | Agile, playful, floating |
| **`material-fluid`** | Variable | `0.60` (Viscous shear) | `0.00` (Plastic deformation)| Liquid blobs, wave wipes, surface tension bridges | Organic, continuous, cohesive |

---

## 3. Mathematical Easing & Spring Catalog

All motion timing must reference these exact mathematical curves:

| Easing Token | Mathematical Definition / Bezier | Profile Character | Best Application |
| :--- | :--- | :--- | :--- |
| **`ease-out-expo`** | `cubic-bezier(0.16, 1, 0.3, 1)` | Explosive initial ignition, ultra-long velvet deceleration | Primary UI entrances, card arrivals, typography masks |
| **`ease-out-circ`** | `cubic-bezier(0, 0.55, 0.45, 1)` | Sudden aggressive braking | Rapid micro-interactions, tooltip reveals |
| **`ease-out-back`** | `cubic-bezier(0.34, 1.56, 0.64, 1)` | Controlled tactile overshoot (108%) with crisp rebound | Icon pops, playful accent badges, toggle switches |
| **`ease-in-out-quart`**| `cubic-bezier(0.76, 0, 0.24, 1)` | Symmetric cinematic acceleration and deceleration | Camera pans, 3D world transitions, background color sweeps |
| **`ease-in-expo`** | `cubic-bezier(0.7, 0, 0.84, 0)` | Accelerating dive into zero visibility | Scene exits, whip transitions, plunge cut exits |
| **`spring-snappy`** | $\zeta = 0.70$ (`stiffness: 200, damping: 14`) | High-energy tactile punch with single micro-rebound | Interactive clicks, state switches, data counter bursts |
| **`spring-critical`** | $\zeta = 1.00$ (`stiffness: 120, damping: 22`) | Maximum velocity arrival with zero overshoot | Critical UI dialogs, forms, layout shifts |
| **`spring-viscous`** | $\zeta = 1.40$ (`stiffness: 60, damping: 24`) | Heavy, luxurious overdamped liquid resistance | Luxury brand reveals, heavy hardware showcases |

---

## 4. 9-Point Spatial Anchor & 3D Origin Standard

Every scaling, rotating, or morphing element MUST declare its transform anchor point:

```text
  [origin-top-left]       [origin-top-center]       [origin-top-right]
        (0% 0%)                 (50% 0%)                (100% 0%)
           ┌───────────────────────┬───────────────────────┐
           │                       │                       │
 [origin-left-center]       [origin-center]      [origin-right-center]
        (0% 50%)                (50% 50%)               (100% 50%)
           │                       │                       │
           └───────────────────────┴───────────────────────┘
 [origin-bottom-left]    [origin-bottom-center]  [origin-bottom-right]
        (0% 100%)               (50% 100%)              (100% 100%)
```

### 3D Depth Origin Tokens:
- **`origin-z-surface`:** `Z: 0px` (Anchor sits on the element's front face).
- **`origin-z-deep`:** `Z: -200px` (Element rotates around an anchor point set deep behind it).
- **`origin-z-camera`:** `Z: +500px` (Element pivots relative to the camera viewport).

---

## 5. Extended Matter Taxonomy (What the piece is made of)

Pick **ONE primary matter**. A second matter may exist only as support. Three is a showreel—refuse it.

| Matter | Eye Follows | Physics Defaults | DNA Stress | Signature Lives In |
| :--- | :--- | :--- | :--- | :--- |
| **`Type`** | Words forming the claim | `mass: 1.0`, `drag: 0.85` | Type scale, ink vs ground contrast, variable font axes | How the key phrase arrives and locks |
| **`UI / Product`** | Layout, cursor, component state | `mass: 1.0`, `restitution: 0.5` | Spacing, chrome vs accent, layout geometry | Shared element transitions / state morphs |
| **`Data`** | Numbers, charts, maps changing | `mass: 0.5`, `spring: snappy` | Quiet chrome, signal color | The count-up, path draw, or data join |
| **`Material`** | Light, shader, grain, 3D surface | `mass: 2.0`, `viscous: 1.4` | Ground + depth atmosphere, one accent | One optical physics event |
| **`Mark / Mascot`** | Character or brand lockup | `mass: 1.0`, `elastic: 0.75` | Shape language, accent on mark | One signature physical gesture |
| **`Fluid / Liquid`** | Organic blob & wave deformation | `viscosity: 0.82`, `mass: variable` | Surface tension, gooey bridge, cohesion | Droplet tear-off, viscous wave wipe |
| **`Grid / Architecture`**| Structural lines, modular slices | `mass: 2.0`, `friction: 0.99` | Monospace alignment, hairline precision | Swiss grid displacement, modular fold |

---

## 6. Color Roles & Motion Permissions

| Role | Job | APCA Minimum Contrast | Motion Permission |
| :--- | :--- | :--- | :--- |
| **Ground** | Largest field. Holds the world. | Baseline (`L^c 0`) | **Never moves** (stays stable). |
| **Ink** | Primary typography and core structure. | $\ge L^c 75$ (body) / $\ge L^c 60$ (hero) | Enters with authority; **never flashes or strobes**. |
| **Quiet** | Secondary typography, grid rules, chrome. | $\ge L^c 45$ | Minimal subtle motion; yields to Ink and Accent. |
| **Accent** | The ONE color that means "this is the point". | $\ge L^c 60$ vs Ground | **Moves only when earned** (scarce, deliberate). |
| **Signal** | State changes (success, alert, live). | State-dependent | **Animates ONLY upon state transitions**. |
| **Fog / Depth**| Atmosphere (tint, blur, grain, depth). | Ambient tint | Static or very slow ambient drift (`glacial`). |

---

## 7. Responsive Spatial Displacement Scale

Spatial offsets scale dynamically across display viewports:

| Spatial Token | Desktop Scale (`px`) | Mobile Scale (`px / rem`) | 3D Depth Travel (`Z-px`) | Application |
| :--- | :--- | :--- | :--- | :--- |
| **`spatial-micro`** | `2px – 4px` | `1px – 2px` | `Z: +10px` | Active button press, subtle hover lift |
| **`spatial-small`** | `8px – 12px` | `4px – 6px` | `Z: +40px` | List item staggers, tooltip reveals |
| **`spatial-normal`**| `16px – 24px` | `8px – 12px` | `Z: +100px` | Standard card entrance, modal slide |
| **`spatial-large`** | `32px – 48px` | `16px – 24px` | `Z: +250px` | Hero headline entrance, section sweep |
| **`spatial-hero`** | `64px – 100px` | `32px – 48px` | `Z: +500px` | Massive dramatic reveal, plunge intro |
| **`spatial-viewport`**| `100vw / 100vh`| `100vw / 100dvh` | `Z: +1500px` | Full scene transition, wipe exit |

---

## 8. Blend Modes & Layer Fusion

| Token | CSS / Compositing Mode | Motion Graphics Purpose |
| :--- | :--- | :--- |
| `blend-normal` | `normal` | Opaque solid UI cards, primary typography |
| `blend-screen` | `screen` | Luminous glow overlays, light sweeps, sparks (dark backgrounds) |
| `blend-multiply` | `multiply` | Ink stamps, shadows, texture grain (light backgrounds) |
| `blend-overlay` | `overlay` | Specular highlights, film grain, glass reflection depth |
| `blend-color-dodge` | `color-dodge` | Intense energetic laser/neon sparks and lightning hits |

---

## 9. Interaction & Driver Models

| Driver Model | Control Mechanism | Progression Metric | Application |
| :--- | :--- | :--- | :--- |
| **`clock`** | Time-based execution | Seconds / milliseconds on a timeline | Videos, stings, automated UI reveals, loops |
| **`scroll_scrub`** | Viewport scroll position | Progress ratio `0.0 → 1.0` (with pin boundaries) | Scrollytelling, landing page feature reveals |
| **`velocity_gesture`** | Touch/pointer velocity & momentum | Drag offset + momentum decay + rubber-band | Bottom sheets, swipe carousels, draggable cards |

---

## 10. Duration Standard Scale

| Token | Duration | Optimal Rhythm & Use Case |
| :--- | :--- | :--- |
| **`instant`** | `100ms` | Haptic micro-feedback, state toggles, click feedback |
| **`fast`** | `200ms` | Tooltips, dropdown opens, hover lifts, icon pops |
| **`normal`** | `350ms` | Card reveals, button transitions, variable font morphs |
| **`slow`** | `600ms` | Hero headline reveals, multiplane parallax shifts |
| **`cinematic`**| `1200ms` | 3D camera dollies, world transitions, atmospheric unfolds |
| **`glacial`** | `2000ms+` | Ambient background particle drift, continuous fluid loops |
