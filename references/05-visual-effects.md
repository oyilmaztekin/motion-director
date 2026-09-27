# 05 Visual Effects, Depth Planes & Shutter Motion Blur

This document defines the optical effects layer, 3D depth plane parallax systems, camera coordinates, and motion blur / shutter angle rules.

---

## 1. The Optical Event Budget

**Rule:** A scene may have **at most ONE primary optical event** occurring simultaneously.
- If a high-intensity blur-in is happening, do not simultaneously trigger a chromatic aberration glitch or rapid gradient morph.
- Effects must serve depth, hierarchy, or state feedback—never decorative clutter.

---

## 2. Motion Blur & Shutter Angle Policy

High-speed movement requires deliberate optical blur settings to balance sharpness with fluidity:

| Token | Shutter Angle | Application Rule |
| :--- | :--- | :--- |
| **`blur-disabled` (Crisp UI)** | `0°` | **Mandatory for UI micro-interactions**, typography reading, buttons, cards. Zero blur preserves crisp vector borders. |
| **`shutter-180` (Cinematic)** | `180°` | Standard cinematic motion blur for rapid scene wipes, camera pans, and flying 3D elements. |
| **`shutter-360` (Hyper-Speed)** | `360°` | Extreme speed streaks during `zoom-through` or warp transitions. |

---

## 3. 3D Depth Planes & Parallax Ratios

When constructing layered spatial compositions, assign every layer to a canonical depth plane:

| Depth Plane | Z-Position | Parallax Travel Ratio | Blur / Atmosphere | Primary Content |
| :--- | :--- | :--- | :--- | :--- |
| **`foreground`** | `Z: +100px` | `1.4x` (Fast travel) | Micro depth-of-field blur | Floating badges, particles, cursor |
| **`midground` (Focal Plane)**| `Z: 0px` | `1.0x` (1:1 Anchor) | Sharp (Zero blur) | Hero typography, main UI card, charts |
| **`background`** | `Z: -200px` | `0.4x` (Slow drift) | Soft atmosphere / grain | Grid lines, ambient gradients, cards |

---

## 4. Camera Transforms & Cinematic Moves

The camera represents the viewer's eye moving through 3D space:

- **`camera.pan(x, y)`:** Smooth lateral viewpoint sweep along the Current (`ease-out-expo`).
- **`camera.dolly(z)`:** Moving the camera forward/backward to tighten focus or reveal surroundings.
- **`camera.rack_focus(from_plane, to_plane)`:** Shifting sharp focus from background to foreground over `normal` duration.

---

## 5. Visual Effects Specification

### A. Shadow & Elevation (Depth Layering)
| Token | Properties | Usage |
| :--- | :--- | :--- |
| `elevation-flat` | `box-shadow: none` | Base planar surface |
| `elevation-card` | `box-shadow: 0 4px 12px rgba(0,0,0,0.08)` | Resting card / component |
| `elevation-lifted`| `box-shadow: 0 12px 32px rgba(0,0,0,0.16)` | Active hover state / dragging |
| `elevation-modal` | `box-shadow: 0 24px 64px rgba(0,0,0,0.24)` | Top-level modal dialog |

### B. Glow & Luminous Accent (Signal Feedback)
- **Parameters:** `box-shadow: 0 0 [spread]px var(--accent-glow)`, `opacity: [ghost → visible]`.
- **Constraint:** Glow is strictly derived from the brand Accent or Signal color. It pulses only on state changes (`fast` or `normal` duration).

### C. Blur & Depth of Field
- **Entrance Blur:** `blur(12px) → blur(0)` with `opacity: 0 → 1`.
- **Background Dim/Veil:** Background content blurs to `blur(8px)` while foreground modal arrives.

### D. Glassmorphism & Materials
- **Backdrop Filter:** `backdrop-filter: blur(16px) saturate(140%)`.
- **Border Spec:** 1px solid `rgba(255, 255, 255, 0.12)`.
- **Rule:** Use sparingly on floating navigation or modals; never apply to multiple nested layers.

### E. Masking & Clipping
- **Inset Wipe:** `clip-path: inset([top] [right] [bottom] [left])`.
- **Circle Expand:** `clip-path: circle(0% at [x] [y]) → circle(150% at [x] [y])`.
