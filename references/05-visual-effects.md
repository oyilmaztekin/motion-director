# 05 Visual Effects, Camera Optics, Atmospheric Scattering & Chromatic Dispersion

This document defines the optical effects layer, 3D depth planes, atmospheric Kelvin scattering (depth fog), camera focal lengths, compositing blend modes, and chromatic dispersion.

---

## 1. The Optical Event Budget

**Rule:** A scene may have **at most ONE primary optical event** occurring simultaneously.
- If a high-intensity blur-in is happening, do not simultaneously trigger a chromatic aberration glitch or rapid gradient morph.
- Effects must serve depth, hierarchy, or state feedback—never decorative clutter.

---

## 2. Atmospheric Scattering & Kelvin Color Temperature (Depth Fog)

In physical optics, distant planes undergo **Rayleigh Scattering**—shifting toward cooler color temperatures and ambient air tint:

| Plane | Z-Depth | Color Temperature (Kelvin) | Atmosphere Tint | Sharpness / Blur |
| :--- | :--- | :--- | :--- | :--- |
| **`foreground`** | `Z: +100px` | Neutral / Warm (`4500K`) | Clean (0% tint) | Micro bokeh blur |
| **`midground` (Focal Anchor)**| `Z: 0px` | True Brand Colors (`5000K`) | Sharp (0% tint) | 100% Vector Crisp |
| **`background`** | `Z: -200px` | Cool Ambient (`6500K - 7500K`) | `rgba(18, 24, 38, 0.45)` | Depth fog + 4px blur |

---

## 3. Camera Optics, Focal Length & Field of View (FOV)

| Lens Token | Focal Length / FOV | Visual Character | Best Application |
| :--- | :--- | :--- | :--- |
| `lens-wide-24` | 24mm (`84° FOV`) | Extreme dynamic perspective, exaggerated z-travel | High-energy sting openers, dramatic reveals |
| `lens-cine-35` | 35mm (`63° FOV`) | Balanced cinematic perspective, natural human eye | Hero landing pages, product walkthroughs |
| `lens-neutral-50`| 50mm (`47° FOV`) | Zero distortion, 1:1 orthographic-like naturalism | Standard UI components, data charts |
| `lens-macro-85` | 85mm (`28° FOV`) | Compressed depth, flattened perspective, luxury | Close-up typography, hardware spec callouts |
| `lens-tele-135` | 135mm (`18° FOV`) | Extreme spatial compression, stacked layers | Abstract 2.5D isometric layering |

---

## 4. Chromatic Dispersion & Refractive Optics

- **Chromatic Aberration (`effects.chromatic-aberration`):** Color fringe splitting (Red/Blue channel offset) on high-contrast edges during high-speed camera motion.
  - `split_offset: micro` (1–2px) for luxury glass; `split_offset: normal` (4–8px) for high-speed impact.
- **Refraction Index:**
  - `refractive_index: 1.52` (Crown Glass / Crystal panels)
  - `refractive_index: 1.33` (Fluid / Liquid distortion)

---

## 5. Specular Lighting & Surface Sheen (Light Sweeps)

- **Specular Sweep (`effects.light-sweep`):** A 45° directional light reflection travelling across a glass/metal surface.
  - `background: linear-gradient(135deg, transparent 40%, rgba(255,255,255,0.4) 50%, transparent 60%)`.
  - `background-position: -200% → 200%`, `duration: normal`, `easing: ease-out-expo`.
- **Dynamic Light Tilt:** Highlight angle shifts with layer rotation to simulate physical light reflection.

---

## 6. Compositing & Layer Blending Modes (`mix-blend-mode`)

- `blend-normal`: Opaque solid UI cards, primary typography.
- `blend-screen`: Luminous glow, sparks, lens flares (black pixels become transparent).
- `blend-multiply`: Ink stamps, drop shadows, dark vignettes on light backgrounds.
- `blend-overlay`: Specular highlights, subtle film grain, surface reflections.
- `blend-color-dodge`: High-energy neon impacts, laser charges, hyper-bright highlights.

---

## 7. Motion Blur & Shutter Angle Policy

- **`blur-disabled` (Crisp UI, 0° Shutter):** Mandatory for UI micro-interactions, text reading, buttons.
- **`shutter-180` (Cinematic, 180° Shutter):** Standard motion blur for scene transitions and 3D pans.
- **`shutter-360` (Hyper-Speed, 360° Shutter):** Extreme streak blur for warp transitions.
