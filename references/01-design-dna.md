# 01 Design DNA, Physics Laws, Perceptual Color & Pixel Snapping

This document establishes the foundation of the project's motion identity, matter composition, perceptual color interpolation, pixel snapping standards, physics laws, driver models, spatial origin standards, and motion density budgets. All scene specifications and storyboards must reference the tokens and rules defined here.

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
3. **Perceptual Color Space (OKLCH Law):**
   - Color transitions and gradient morphs MUST interpolate in polar perceptual color space (**OKLCH** or **CIELAB**).
   - Standard sRGB interpolation creates desaturated, muddy gray dead-zones midway through transitions. OKLCH preserves constant chroma and perceived luminosity throughout the entire tween.
4. **Pixel Snapping & Sub-Pixel Anti-Aliasing Guard:**
   - Dynamic motion uses smooth sub-pixel float coordinates during transit.
   - Upon arriving at any **Hold or Rest state**, all coordinates and dimensions MUST snap to whole integer pixels (`Math.round`) to prevent edge fuzziness and shimmering artifacts.
5. **Anticipation & Volume Conservation (Squash & Stretch Law):**
   - Major actions must be preceded by a micro counter-momentum or compression.
   - **Conservation of Volume:** When an object compresses or stretches, its 2D area/volume must remain constant:
     $$\text{scaleX} \times \text{scaleY} \approx 1.0$$
6. **Spatial Arcs:**
   - Organic motion never travels along robotic diagonal vectors. Trajectories follow natural gravitational/momentum curves (`arc-convex` or `arc-concave`). Linear paths (`direct-axis`) are reserved for rigid mechanical UI rails.
7. **Asymmetric Easing:**
   - `linear` interpolation is banned except for infinite ambient cycles or raw progress bars.
   - Organic motion requires asymmetric curves: aggressive acceleration (`ease-in`) paired with a long, gentle deceleration/settle (`ease-out`), or mass-damped springs.
8. **Follow-Through & Overlapping Action:**
   - Elements never lock into place on the exact same frame. Secondary layers, attached badges, shadows, and text settle with a 50–150ms delay/offset relative to the primary hero.
9. **Settle & Negative Time:**
   - Elements do not hit target values like a brick wall; they decelerate smoothly into a rest state (`decay`).
   - Every completed action must include intentional negative time (**0.3s – 0.8s hold**) allowing the viewer to absorb the message before the next beat begins.

---

## 2. Transform Origin Standard Library

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

## 3. Blend Modes & Layer Fusion

| Token | CSS / Compositing Mode | Motion Graphics Purpose |
| :--- | :--- | :--- |
| `blend-normal` | `normal` | Opaque solid UI cards, primary typography |
| `blend-screen` | `screen` | Luminous glow overlays, light sweeps, sparks (dark backgrounds) |
| `blend-multiply` | `multiply` | Ink stamps, shadows, texture grain (light backgrounds) |
| `blend-overlay` | `overlay` | Specular highlights, film grain, glass reflection depth |
| `blend-color-dodge` | `color-dodge` | Intense energetic laser/neon sparks and lightning hits |

---

## 4. Interaction & Driver Models

| Driver Model | Control Mechanism | Progression Metric | Application |
| :--- | :--- | :--- | :--- |
| **`clock`** | Time-based execution | Seconds / milliseconds on a timeline | Videos, stings, automated UI reveals, loops |
| **`scroll_scrub`** | Viewport scroll position | Progress ratio `0.0 → 1.0` (with pin boundaries) | Scrollytelling, landing page feature reveals |
| **`velocity_gesture`** | Touch/pointer velocity & momentum | Drag offset + momentum decay + rubber-band | Bottom sheets, swipe carousels, draggable cards |

---

## 5. Matter Taxonomy (What the piece is made of)

Pick **ONE primary matter**. A second matter may exist only as support. Three is a showreel—refuse it.

| Matter | Eye Follows | DNA Stress | Signature Lives In |
| :--- | :--- | :--- | :--- |
| **Type** | Words forming the claim | Type scale, ink vs ground contrast, variable font axes | How the key phrase arrives and locks |
| **UI / Product** | Layout, cursor, component state | Spacing, chrome vs accent, layout geometry | Shared element transitions / state morphs |
| **Data** | Numbers, charts, maps changing | Quiet chrome, signal color | The count-up, path draw, or data join |
| **Material** | Light, shader, grain, 3D surface | Ground + depth atmosphere, one accent | One optical physics event |
| **Mark / Mascot** | Character or brand lockup | Shape language, accent on mark | One signature physical gesture |

---

## 6. Color Roles & Motion Permissions

| Role | Job | Motion Permission |
| :--- | :--- | :--- |
| **Ground** | Largest field. Holds the world. | **Never moves** (stays stable). |
| **Ink** | Primary typography and core structure. | Enters with authority; **never flashes or strobes**. |
| **Quiet** | Secondary typography, grid rules, chrome. | Minimal subtle motion; yields to Ink and Accent. |
| **Accent** | The ONE color that means "this is the point". | **Moves only when earned** (scarce, deliberate). |
| **Signal** | State changes (success, alert, live). | **Animates ONLY upon state transitions**. |
| **Fog / Depth**| Atmosphere (tint, blur, grain, depth). | Static or very slow ambient drift (`glacial`). |

---

## 7. Token Standard Library

### A. Duration Tokens
`instant` (100ms) · `fast` (200ms) · `normal` (350ms) · `slow` (600ms) · `cinematic` (1200ms) · `glacial` (2000ms+)

### B. Easing Tokens
`ease-out-expo` · `ease-out-cubic` · `ease-in-out-cubic` · `ease-out-back` · `spring-snappy` · `spring-gentle` · `spring-heavy` · `linear`

### C. Spatial & Path Tokens
`micro` (2–4px) · `small` (8–12px) · `normal` (16–24px) · `large` (32–48px) · `dramatic` (64–100px) · `viewport` (100vh/100vw)
Paths: `arc-convex`, `arc-concave`, `direct-axis`.

### D. Audio & Sonic Hit Tokens
`sfx-sub` (bass hit) · `sfx-click` (crisp tick) · `sfx-whoosh` (air transit) · `sfx-swell` (tension riser) · `sfx-chime` (resolve)
