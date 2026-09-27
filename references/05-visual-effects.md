# 05 Visual Effects, Bokeh Iris Geometry, Mask Feathering & Chromatic Optics

This document defines the optical effects layer, 3D depth planes, aperture bokeh blade geometry, mask edge feathering, atmospheric Kelvin scattering (depth fog), camera focal lengths, compositing blend modes, and chromatic dispersion.

---

## 1. The Optical Event Budget

**Rule:** A scene may have **at most ONE primary optical event** occurring simultaneously.
- If a high-intensity blur-in is happening, do not simultaneously trigger a chromatic aberration glitch or rapid gradient morph.
- Effects must serve depth, hierarchy, or state feedback—never decorative clutter.

---

## 2. Bokeh Iris Geometry & Aperture Physics

During depth-of-field rack-focus and out-of-focus blurs, specular highlights render with physical aperture blade geometry:

| Bokeh Token | Optical Shape | Visual Signature | Best Application |
| :--- | :--- | :--- | :--- |
| `bokeh-f1.4-circular` | Perfect smooth disc | Ultra-creamy, soft high-end blur | Luxury brand hero sections, portraits |
| `bokeh-f2.8-hexagonal`| 6-sided faceted polygon | Geometric, technological, crisp | SaaS dashboards, fintech charts |
| `bokeh-anamorphic` | 2:1 horizontal streak oval | Cinematic Hollywood lens flare character | Video stings, tech launch openers |

---

## 3. Mask Edge Feathering (Soft vs Hard Inset Clipping)

| Feather Token | Gradient Width | Visual Character | Best Application |
| :--- | :--- | :--- | :--- |
| `feather-none` | `0px` | Crisp geometric boundary (Hard SVG / UI clip) | Modal containers, card windows, progress bars |
| `feather-soft` | `12px – 16px` | Organic alpha gradient falloff along edge | Hero typography reveals, editorial photo entries |
| `feather-diffuse`| `32px – 48px` | Wide atmospheric dissolve boundary | Fog cards, particle emitter boundaries, dreamscapes |

---

## 4. Atmospheric Scattering & Kelvin Color Temperature (Depth Fog)

In physical optics, distant planes undergo **Rayleigh Scattering**—shifting toward cooler color temperatures and ambient air tint:

| Plane | Z-Depth | Color Temperature (Kelvin) | Atmosphere Tint | Sharpness / Blur |
| :--- | :--- | :--- | :--- | :--- |
| **`foreground`** | `Z: +100px` | Neutral / Warm (`4500K`) | Clean (0% tint) | Micro bokeh blur |
| **`midground` (Focal Anchor)**| `Z: 0px` | True Brand Colors (`5000K`) | Sharp (0% tint) | 100% Vector Crisp |
| **`background`** | `Z: -200px` | Cool Ambient (`6500K - 7500K`) | `rgba(18, 24, 38, 0.45)` | Depth fog + 4px blur |

---

## 5. Camera Optics, Focal Length & Field of View (FOV)

| Lens Token | Focal Length / FOV | Visual Character | Best Application |
| :--- | :--- | :--- | :--- |
| `lens-wide-24` | 24mm (`84° FOV`) | Extreme dynamic perspective, exaggerated z-travel | High-energy sting openers, dramatic reveals |
| `lens-cine-35` | 35mm (`63° FOV`) | Balanced cinematic perspective, natural human eye | Hero landing pages, product walkthroughs |
| `lens-neutral-50`| 50mm (`47° FOV`) | Zero distortion, 1:1 orthographic-like naturalism | Standard UI components, data charts |
| `lens-macro-85` | 85mm (`28° FOV`) | Compressed depth, flattened perspective, luxury | Close-up typography, hardware spec callouts |
| `lens-tele-135` | 135mm (`18° FOV`) | Extreme spatial compression, stacked layers | Abstract 2.5D isometric layering |

---

## 6. Chromatic Dispersion & Refractive Optics

- **Chromatic Aberration (`effects.chromatic-aberration`):** Color fringe splitting (Red/Blue channel offset) on high-contrast edges during high-speed camera motion.
  - `split_offset: micro` (1–2px) for luxury glass; `split_offset: normal` (4–8px) for high-speed impact.
- **Refraction Index:**
  - `refractive_index: 1.52` (Crown Glass / Crystal panels)
  - `refractive_index: 1.33` (Fluid / Liquid distortion)

---

## 7. Specular Lighting & Surface Sheen (Light Sweeps)

- **Specular Sweep (`effects.light-sweep`):** A 45° directional light reflection travelling across a glass/metal surface.
  - `background: linear-gradient(135deg, transparent 40%, rgba(255,255,255,0.4) 50%, transparent 60%)`.
  - `background-position: -200% → 200%`, `duration: normal`, `easing: ease-out-expo`.
- **Dynamic Light Tilt:** Highlight angle shifts with layer rotation to simulate physical light reflection.

---

## 8. Compositing & Layer Blending Modes (`mix-blend-mode`)

- `blend-normal`: Opaque solid UI cards, primary typography.
- `blend-screen`: Luminous glow, sparks, lens flares (black pixels become transparent).
- `blend-multiply`: Ink stamps, drop shadows, dark vignettes on light backgrounds.
- `blend-overlay`: Specular highlights, subtle film grain, surface reflections.
- `blend-color-dodge`: High-energy neon impacts, laser charges, hyper-bright highlights.

---

## 9. Motion Blur & Shutter Angle Policy

- **`blur-disabled` (Crisp UI, 0° Shutter):** Mandatory for UI micro-interactions, text reading, buttons.
- **`shutter-180` (Cinematic, 180° Shutter):** Standard motion blur for scene transitions and 3D pans.
- **`shutter-360` (Hyper-Speed, 360° Shutter):** Extreme streak blur for warp transitions.

---

## 10. Multiplane Parallax Depth Speed Ratios

When the camera dollies or pans, layer velocity scales inversely with optical distance:

| Depth Plane | Z-Translation | Parallax Velocity Multiplier | Visual Role |
| :--- | :--- | :--- | :--- |
| **`plane-foreground`** | `Z: +100px` | $v_{\text{fg}} = 1.80 \cdot v_{\text{camera}}$ | Floating micro-particles, bokeh elements |
| **`plane-hero`** | `Z: 0px` | $v_{\text{hero}} = 1.00 \cdot v_{\text{camera}}$ | Primary content payload (Focal Anchor) |
| **`plane-midground`** | `Z: -100px` | $v_{\text{mid}} = 0.55 \cdot v_{\text{camera}}$ | Secondary cards, layout grid lines |
| **`plane-background`**| `Z: -300px` | $v_{\text{bg}} = 0.20 \cdot v_{\text{camera}}$ | Ambient depth fog, distant typography |
| **`plane-deep`** | `Z: -800px` | $v_{\text{deep}} = 0.05 \cdot v_{\text{camera}}$| Horizon gradient, atmospheric haze |

---

## 11. Dynamic Contact Shadow Pinch & Elevation

- **Contact Pinch (`shadow-contact-pinch`):** Zero offset, `0px 2px 4px rgba(0,0,0,0.5)`, tight hard edge on surface contact.
- **Floating Elevation (`shadow-elevation-air`):** Dynamic expansion `0px 24px 48px rgba(0,0,0,0.18)` as $Z$ increases.

---

## 12. Gradient Dither & OLED Anti-Banding Guard

- Smooth color ramps across dark backgrounds must inject dynamic monochromatic noise (`dither-grain-subtle`, 2% opacity) to eliminate 8-bit banding artifacts on high-contrast OLED displays.
