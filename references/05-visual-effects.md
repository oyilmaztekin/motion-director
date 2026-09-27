# 05 Visual Effects, Camera Optics, Lens FOV & Chromatic Dispersion

This document defines the optical effects layer, 3D depth plane parallax systems, camera focal length / field of view (FOV), compositing blend modes, specular light sweeps, and chromatic dispersion.

---

## 1. The Optical Event Budget

**Rule:** A scene may have **at most ONE primary optical event** occurring simultaneously.
- If a high-intensity blur-in is happening, do not simultaneously trigger a chromatic aberration glitch or rapid gradient morph.
- Effects must serve depth, hierarchy, or state feedback—never decorative clutter.

---

## 2. Camera Optics, Focal Length & Field of View (FOV)

Camera movement must declare its virtual lens focal length to govern spatial compression and perspective distortion:

| Lens Token | Focal Length / FOV | Visual Character | Best Application |
| :--- | :--- | :--- | :--- |
| `lens-wide-24` | 24mm (`84° FOV`) | Extreme dynamic perspective, exaggerated z-travel | High-energy sting openers, dramatic reveals |
| `lens-cine-35` | 35mm (`63° FOV`) | Balanced cinematic perspective, natural human eye | Hero landing pages, product walkthroughs |
| `lens-neutral-50`| 50mm (`47° FOV`) | Zero distortion, 1:1 orthographic-like naturalism | Standard UI components, data charts |
| `lens-macro-85` | 85mm (`28° FOV`) | Compressed depth, flattened perspective, luxury | Close-up typography, hardware spec callouts |
| `lens-tele-135` | 135mm (`18° FOV`) | Extreme spatial compression, stacked layers | Abstract 2.5D isometric layering |

---

## 3. Chromatic Dispersion & Refractive Optics

Simulate physical light transmission through glass, crystal, and lens edges:

- **Chromatic Aberration (`effects.chromatic-aberration`):** Color fringe splitting (Red/Blue channel offset) on high-contrast edges during high-speed camera motion.
  - **Offset Token:** `micro` (1–2px split) for luxury glass; `normal` (4–8px split) for high-speed impact.
- **Refraction Index:**
  - `refractive_index: 1.52` (Crown Glass / Crystal panels)
  - `refractive_index: 1.33` (Fluid / Liquid distortion)

---

## 4. Specular Lighting & Surface Sheen (Light Sweeps)

- **Specular Sweep (`effects.light-sweep`):** A 45° directional light reflection travelling across a glass/metal surface.
  - **Properties:** `background: linear-gradient(135deg, transparent 40%, rgba(255,255,255,0.4) 50%, transparent 60%)`.
  - **Angle & Position:** `background-position: -200% → 200%`, `duration: normal`, `easing: ease-out-expo`.
- **Dynamic Light Tilt:** As a 3D layer rotates along X/Y, its gradient highlight angle shifts proportionally to simulate physical light reflection.

---

## 5. Compositing & Layer Blending Modes (`mix-blend-mode`)

| Mode | Token | Visual Character |
| :--- | :--- | :--- |
| `screen` | `blend-screen` | Luminous glow, sparks, lens flares (black pixels become transparent). |
| `multiply` | `blend-multiply` | Ink stamps, drop shadows, dark vignettes on light backgrounds. |
| `overlay` | `blend-overlay` | Specular highlights, subtle film grain, surface reflections. |
| `color-dodge` | `blend-color-dodge` | High-energy neon impacts, laser charges, hyper-bright highlights. |

---

## 6. Motion Blur & Shutter Angle Policy

| Token | Shutter Angle | Application Rule |
| :--- | :--- | :--- |
| **`blur-disabled` (Crisp UI)** | `0°` | **Mandatory for UI micro-interactions**, typography reading, buttons, cards. Zero blur preserves crisp vector borders. |
| **`shutter-180` (Cinematic)** | `180°` | Standard cinematic motion blur for rapid scene wipes, camera pans, and flying 3D elements. |
| **`shutter-360` (Hyper-Speed)** | `360°` | Extreme speed streaks during `zoom-through` or warp transitions. |

---

## 7. 3D Depth Planes & Parallax Ratios

| Depth Plane | Z-Position | Parallax Travel Ratio | Blur / Atmosphere | Primary Content |
| :--- | :--- | :--- | :--- | :--- |
| **`foreground`** | `Z: +100px` | `1.4x` (Fast travel) | Micro depth-of-field blur | Floating badges, particles, cursor |
| **`midground` (Focal Plane)**| `Z: 0px` | `1.0x` (1:1 Anchor) | Sharp (Zero blur) | Hero typography, main UI card, charts |
| **`background`** | `Z: -200px` | `0.4x` (Slow drift) | Soft atmosphere / grain | Grid lines, ambient gradients, cards |
