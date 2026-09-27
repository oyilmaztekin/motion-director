# 05 Visual Effects, Depth Planes, Blending Modes & Specular Lighting

This document defines the optical effects layer, 3D depth plane parallax systems, compositing blend modes, specular light sweeps, and motion blur rules.

---

## 1. The Optical Event Budget

**Rule:** A scene may have **at most ONE primary optical event** occurring simultaneously.
- If a high-intensity blur-in is happening, do not simultaneously trigger a chromatic aberration glitch or rapid gradient morph.
- Effects must serve depth, hierarchy, or state feedback—never decorative clutter.

---

## 2. Specular Lighting & Surface Sheen (Light Sweeps)

In premium motion graphics, light movement accentuates materiality:

- **Specular Sweep (`effects.light-sweep`):** A 45° directional light reflection travelling across a glass/metal surface.
  - **Properties:** `background: linear-gradient(135deg, transparent 40%, rgba(255,255,255,0.4) 50%, transparent 60%)`.
  - **Angle & Position:** `background-position: -200% → 200%`, `duration: normal`, `easing: ease-out-expo`.
- **Dynamic Light Tilt:** As a 3D layer rotates along X/Y, its gradient highlight angle shifts proportionally to simulate physical light reflection.

---

## 3. Compositing & Layer Blending Modes (`mix-blend-mode`)

Use blending modes to fuse visual effects seamlessly into backgrounds:

| Mode | Token | Visual Character |
| :--- | :--- | :--- |
| `screen` | `blend-screen` | Luminous glow, sparks, lens flares (black pixels become transparent). |
| `multiply` | `blend-multiply` | Ink stamps, drop shadows, dark vignettes on light backgrounds. |
| `overlay` | `blend-overlay` | Specular highlights, subtle film grain, surface reflections. |
| `color-dodge` | `blend-color-dodge` | High-energy neon impacts, laser charges, hyper-bright highlights. |

---

## 4. Motion Blur & Shutter Angle Policy

| Token | Shutter Angle | Application Rule |
| :--- | :--- | :--- |
| **`blur-disabled` (Crisp UI)** | `0°` | **Mandatory for UI micro-interactions**, typography reading, buttons, cards. Zero blur preserves crisp vector borders. |
| **`shutter-180` (Cinematic)** | `180°` | Standard cinematic motion blur for rapid scene wipes, camera pans, and flying 3D elements. |
| **`shutter-360` (Hyper-Speed)** | `360°` | Extreme speed streaks during `zoom-through` or warp transitions. |

---

## 5. 3D Depth Planes & Parallax Ratios

| Depth Plane | Z-Position | Parallax Travel Ratio | Blur / Atmosphere | Primary Content |
| :--- | :--- | :--- | :--- | :--- |
| **`foreground`** | `Z: +100px` | `1.4x` (Fast travel) | Micro depth-of-field blur | Floating badges, particles, cursor |
| **`midground` (Focal Plane)**| `Z: 0px` | `1.0x` (1:1 Anchor) | Sharp (Zero blur) | Hero typography, main UI card, charts |
| **`background`** | `Z: -200px` | `0.4x` (Slow drift) | Soft atmosphere / grain | Grid lines, ambient gradients, cards |

---

## 6. Visual Effects Specification

### A. Shadow & Elevation (Depth Layering)
- `elevation-flat`: `box-shadow: none`
- `elevation-card`: `box-shadow: 0 4px 12px rgba(0,0,0,0.08)`
- `elevation-lifted`: `box-shadow: 0 12px 32px rgba(0,0,0,0.16)`
- `elevation-modal`: `box-shadow: 0 24px 64px rgba(0,0,0,0.24)`

### B. Glow & Luminous Accent (Signal Feedback)
- **Parameters:** `box-shadow: 0 0 [spread]px var(--accent-glow)`, `opacity: [ghost → visible]`.
- **Constraint:** Glow is strictly derived from the brand Accent or Signal color. It pulses only on state changes (`fast` or `normal` duration).

### C. Glassmorphism & Materials
- **Backdrop Filter:** `backdrop-filter: blur(16px) saturate(140%)`.
- **Border Spec:** 1px solid `rgba(255, 255, 255, 0.12)`.
