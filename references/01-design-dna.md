# 01 Design DNA & Core Motion Laws

This document establishes the foundation of the project's motion identity, matter composition, color permissions, physics laws, driver models, and spatial origin standards. All scene specifications and storyboards must reference the tokens and rules defined here.

---

## 1. The Core Motion & Physics Laws

Every animated scene produced by `motion-director` must satisfy these foundational laws:

1. **Staging & Single Focal Anchor (Tek Odak):**
   - Every frame has exactly ONE primary focal point (anchor). Visual hierarchy, secondary elements, and camera framing exist solely to guide the eye toward it.
   - Simultaneous competing high-energy actions are strictly forbidden (prevents cognitive overload).
2. **Anticipation & Volume Conservation (Squash & Stretch Hacim Yasası):**
   - Major actions must be preceded by a micro counter-momentum or compression.
   - **Conservation of Volume:** When an object compresses or stretches, its 2D area/volume must remain constant:
     $$\text{scaleX} \times \text{scaleY} \approx 1.0$$
     *(Example: A 20% vertical squash `scaleY: 0.80` mandates an horizontal stretch `scaleX: 1.25` so the object does not lose perceived physical mass).*
3. **Spatial Arcs (Kavisli Yörüngeler):**
   - Organic motion never travels along robotic diagonal vectors. Trajectories follow natural gravitational/momentum curves (`arc-convex` or `arc-concave`). Linear paths (`direct-axis`) are reserved for rigid mechanical UI rails.
4. **Asymmetric Easing (Asimetrik Eğriler):**
   - `linear` interpolation is banned except for infinite ambient cycles or raw progress bars.
   - Organic motion requires asymmetric curves: aggressive acceleration (`ease-in`) paired with a long, gentle deceleration/settle (`ease-out`), or mass-damped springs.
5. **Follow-Through & Overlapping Action (Kademeli Tamamlanma):**
   - Elements never lock into place on the exact same frame. Secondary layers, attached badges, shadows, and text settle with a 50–150ms delay/offset relative to the primary hero.
6. **Settle & Negative Time (Sindirme & Dinlenme):**
   - Elements do not hit target values like a brick wall; they decelerate smoothly into a rest state (`decay`).
   - Every completed action must include intentional negative time (**0.3s – 0.8s hold**) allowing the viewer to absorb the message before the next beat begins.

---

## 2. Transform Origin Standard Library (Eksen Noktası)

Every scaling, rotating, or morphing element MUST declare its transform anchor point:

| Token | Coordinates | Typical Use Case |
| :--- | :--- | :--- |
| `origin-center` | `50% 50%` | Radial scale-pops, circular loaders, floating icons |
| `origin-top-left` | `0% 0%` | Dropdown unfurls, corner badges, accordion reveals |
| `origin-top-center` | `50% 0%` | Hanging signboards, 3D flip-downs, vertical curtains |
| `origin-bottom-center`| `50% 100%` | Bar chart growth, jump anticipation, ground-anchored cards |
| `origin-left-center` | `0% 50%` | Progress bars, book-fold reveals, line stroke draws |
| `origin-custom` | `(x, y)` | Focal points tied to exact cursor click or anchor coordinates |

---

## 3. Interaction & Driver Models

| Driver Model | Control Mechanism | Progression Metric | Application |
| :--- | :--- | :--- | :--- |
| **`clock`** | Time-based execution | Seconds / milliseconds on a timeline | Videos, stings, automated UI reveals, loops |
| **`scroll_scrub`** | Viewport scroll position | Progress ratio `0.0 → 1.0` (with pin boundaries) | Scrollytelling, landing page feature reveals |
| **`velocity_gesture`** | Touch/pointer velocity & momentum | Drag offset + momentum decay + rubber-band | Bottom sheets, swipe carousels, draggable cards |

---

## 4. Matter Taxonomy (What the piece is made of)

Pick **ONE primary matter**. A second matter may exist only as support. Three is a showreel—refuse it.

| Matter | Eye Follows | DNA Stress | Signature Lives In |
| :--- | :--- | :--- | :--- |
| **Type** | Words forming the claim | Type scale, ink vs ground contrast, variable font axes | How the key phrase arrives and locks |
| **UI / Product** | Layout, cursor, component state | Spacing, chrome vs accent, layout geometry | Shared element transitions / state morphs |
| **Data** | Numbers, charts, maps changing | Quiet chrome, signal color | The count-up, path draw, or data join |
| **Material** | Light, shader, grain, 3D surface | Ground + depth atmosphere, one accent | One optical physics event |
| **Mark / Mascot** | Character or brand lockup | Shape language, accent on mark | One signature physical gesture |

---

## 5. Color Roles & Motion Permissions

| Role | Job | Motion Permission |
| :--- | :--- | :--- |
| **Ground** | Largest field. Holds the world. | **Never moves** (stays stable). |
| **Ink** | Primary typography and core structure. | Enters with authority; **never flashes or strobes**. |
| **Quiet** | Secondary typography, grid rules, chrome. | Minimal subtle motion; yields to Ink and Accent. |
| **Accent** | The ONE color that means "this is the point". | **Moves only when earned** (scarce, deliberate). |
| **Signal** | State changes (success, alert, live). | **Animates ONLY upon state transitions**. |
| **Fog / Depth**| Atmosphere (tint, blur, grain, depth). | Static or very slow ambient drift (`glacial`). |

---

## 6. Token Standard Library

### A. Duration Tokens
| Token | Duration | Usage |
| :--- | :--- | :--- |
| `instant` | 100ms | Micro-feedback (state toggle, opacity snap) |
| `fast` | 200ms | Snappy UI responses (hover, focus ring, tap) |
| `normal` | 350ms | Standard transitions (panel slide, card flip, text line) |
| `slow` | 600ms | Dramatic entrances (hero reveal, section transition) |
| `cinematic` | 1200ms | Statement moments (logo reveal, scene climax) |
| `glacial` | 2000ms+ | Continuous ambient evolution (gradient cycle, atmosphere) |

### B. Easing Tokens
| Token | Value / Curve | Usage |
| :--- | :--- | :--- |
| `ease-out-expo` | `cubic-bezier(0.16, 1, 0.3, 1)` | Dramatic deceleration, hero entrances |
| `ease-out-cubic` | `cubic-bezier(0.33, 1, 0.68, 1)` | Smooth, natural stop for standard UI |
| `ease-in-out-cubic`| `cubic-bezier(0.65, 0, 0.35, 1)` | Balanced S-curve for scene transitions |
| `ease-out-back` | `cubic-bezier(0.34, 1.56, 0.64, 1)` | Controlled overshoot with personality |
| `ease-in-quad` | `cubic-bezier(0.11, 0, 0.5, 0)` | Accelerating departure/exit |
| `spring-snappy` | `{ mass: 1, stiffness: 200, damping: 20 }` | Direct tactile interactive response |
| `spring-gentle` | `{ mass: 1.5, stiffness: 100, damping: 14 }` | Soft, premium, weighted settling |
| `spring-heavy` | `{ mass: 2.5, stiffness: 80, damping: 12 }` | Heavy containers, card stacks, modals |
| `linear` | `linear` | Ambient continuous loops and timers only |

### C. Spatial & Path Tokens
- `micro`: 2–4px | `small`: 8–12px | `normal`: 16–24px | `large`: 32–48px | `dramatic`: 64–100px | `viewport`: 100vh / 100vw
- **Paths:** `arc-convex` (upward arc), `arc-concave` (scooping arc), `direct-axis` (straight line).

### D. Audio & Sonic Hit Tokens
- `sfx-sub`: Low-frequency sub-bass impact (climax hit, hero arrival)
- `sfx-click`: Crisp mechanical transient (toggle, button trigger)
- `sfx-whoosh`: Directional air rush (seam cut, fast transit along Current)
- `sfx-swell`: Rising tension tonal sweep (anticipation before payoff)
- `sfx-chime`: High-frequency positive resolution (success, unlock)
