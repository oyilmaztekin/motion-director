# 05 Visual Effects, Bokeh Iris Geometry, Mask Feathering & Chromatic Optics

This document defines the optical effects layer, 3D depth planes, aperture bokeh blade geometry, mask edge feathering, atmospheric Kelvin scattering (depth fog), camera focal lengths, compositing blend modes, Fresnel refraction, dual-shadow models, and chromatic dispersion.

---

## 1. The Optical Event Budget & Concurrency Guard

**Hard Rule:** A scene may have **at most ONE primary optical event** occurring simultaneously, accompanied by **no more than TWO ambient baseline shaders**.

| Event Tier | Maximum Concurrent | Allowed Effects | Prohibited Conflicts |
| :--- | :--- | :--- | :--- |
| **Primary Optical Event** | **1** | Camera rack focus, heavy anamorphic flare streak, warp zoom blur, chromatic glitch | Never trigger a chromatic glitch while an active rack-focus or intense light-sweep is executing |
| **Secondary Ambient Layer** | **2** | Subtle OLED blue-noise dither, atmospheric Kelvin depth fog, micro contact shadow | High-intensity bloom flashes, rapid blend-mode cycling |

---

## 2. Bokeh Iris Geometry & Physical Aperture Models

During depth-of-field rack-focus and out-of-focus blurs, specular highlights render with physical aperture blade geometry:

| Bokeh Token | Aperture Geometry | Blade Count | Visual Signature | Best Application |
| :--- | :--- | :--- | :--- | :--- |
| **`bokeh-f1.4-circular`** | Perfect smooth circle | 9–11 curved blades | Ultra-creamy, soft high-end blur | Luxury brand hero sections, portrait depth |
| **`bokeh-f2.8-hexagonal`**| 6-sided faceted polygon | 6 straight blades | Geometric, technological, crisp | SaaS dashboards, fintech telemetry charts |
| **`bokeh-f4.0-octagonal`**| 8-sided faceted polygon | 8 straight blades | Structured, architectural, balanced | Isometric engineering, hardware diagrams |
| **`bokeh-anamorphic`** | 2:1 horizontal oval | Cylindrical lens element | Cinematic Hollywood flare & streak character | Video launch openers, brand stings |

---

## 3. Mask Edge Feathering (Soft vs Hard Inset Clipping)

| Feather Token | Gradient Border Width | Visual Character | Best Application |
| :--- | :--- | :--- | :--- |
| **`feather-none`** | `0px` | Crisp geometric boundary (Hard SVG / UI clip) | Modal containers, card windows, progress bars |
| **`feather-micro`** | `2px – 4px` | Sub-pixel anti-aliased organic edge | Crisp vector UI cards, floating tooltip tags |
| **`feather-soft`** | `12px – 16px` | Organic alpha gradient falloff along edge | Hero typography reveals, editorial photo entries |
| **`feather-diffuse`**| `32px – 48px` | Wide atmospheric dissolve boundary | Fog cards, particle emitter boundaries, dreamscapes |

---

## 4. Atmospheric Scattering & Kelvin Color Temperature (Depth Fog)

In physical optics, distant planes undergo **Rayleigh Scattering**—shifting toward cooler color temperatures and ambient air tint as distance $Z$ increases:

| Plane | Z-Depth | Color Temperature (Kelvin) | Atmosphere Tint | Sharpness / Blur |
| :--- | :--- | :--- | :--- | :--- |
| **`foreground`** | `Z: +100px` | Warm / Intimate (`4000K – 4500K`) | Clean (0% tint) | Micro foreground bokeh blur |
| **`midground` (Hero Focus)**| `Z: 0px` | True Brand Colors (`5000K – 5500K`)| Neutral (0% tint) | 100% Vector Crisp ($0\text{px}$ blur) |
| **`background`** | `Z: -200px` | Cool Ambient (`6500K – 7500K`) | `rgba(18, 24, 38, 0.45)` | Depth fog + $4\text{px}$ blur |
| **`deep-horizon`** | `Z: -600px` | Deep Atmospheric Cold (`8500K – 9500K`)| `rgba(10, 14, 26, 0.80)` | Volumetric haze + $12\text{px}$ blur |

- **Depth Fog Density Formula:** $\rho(z) = 1 - e^{-\beta \cdot |z|}$ where $\beta = 0.0035$ determines atmospheric haze density.

---

## 5. Camera Optics, Focal Lengths, FOV & Rack-Focus

### A. Focal Length Catalog & Lens Profiles
| Lens Token | Focal Length / FOV | Lens Distortion Profile | Perspective Character | Best Application |
| :--- | :--- | :--- | :--- | :--- |
| **`lens-wide-24`** | 24mm (`84° FOV`) | Barrel distortion ($+0.08$) | Exaggerated Z-travel, dynamic perspective | High-energy sting openers, dramatic reveals |
| **`lens-cine-35`** | 35mm (`63° FOV`) | Near-zero distortion ($+0.01$) | Balanced cinematic perspective, natural eye | Hero landing pages, product walkthroughs |
| **`lens-neutral-50`**| 50mm (`47° FOV`) | True orthographic zero ($0.00$) | Pure geometric naturalism, 1:1 scale | Standard UI components, data charts |
| **`lens-macro-85`** | 85mm (`28° FOV`) | Slight pincushion ($-0.02$) | Compressed depth, flattened luxury focus | Close-up typography, hardware spec callouts |
| **`lens-tele-135`** | 135mm (`18° FOV`) | Pincushion distortion ($-0.05$) | Extreme spatial compression, stacked layers | Abstract 2.5D isometric layering |

### B. Optical Rack-Focus Formula
When transitioning focus between Near Plane ($z_1$) and Far Plane ($z_2$):
- **Focal Plane Shift:** Interpolate focal plane $z_f(t)$ using `ease-in-out-cubic`.
- **Blur Radius Calculation:** $\text{Blur}(z) = \left| 1 - \frac{z}{z_f(t)} \right| \times \text{ApertureBlurMax}$.

---

## 6. Refractive Optics, Fresnel Glassmorphism & Caustics

### A. Refraction Index ($n$)
- **`refractive_index: 1.52` (Crown Glass / Crystal Panels):** Standard for translucent spatial UI cards.
- **`refractive_index: 1.33` (Water / Fluid / Liquid Shaders):** Used for fluid asset morphing.
- **`refractive_index: 2.42` (Diamond / Prismatic Glass):** High dispersion chromatic splits.

### B. Physical Fresnel Reflection Formula
On 2.5D cards tilting relative to camera angle $\theta$:

$$F(\theta) = F_0 + (1 - F_0)(1 - \cos\theta)^5$$

- As a glass card tilts away from camera ($\theta \to 90^\circ$), edge specular reflection ($F$) increases automatically from $4\%$ ($F_0 = 0.04$) to $100\%$ white sheen.

### C. Frosted Glass Roughness Spread
- **`roughness: micro-smooth` ($\sigma = 0.05$):** Sharp mirror-like glass reflection.
- **`roughness: frosted-satin` ($\sigma = 0.25$):** visionOS-grade tactile frosted glass with $24\text{px}$ backdrop blur.

---

## 7. Specular Lighting, Bloom Halos & Anamorphic Flares

### A. Specular Light Sweeps (`effects.light-sweep`)
- **Angle & Position:** 45° directional specular line travelling across card surface (`position: -200% → +200%`).
- **Timing & Easing:** Duration `normal` (350–500ms), `ease-out-expo`.
- **Dynamic Light Tilt:** Highlight reflection angle shifts inversely with 3D card rotation ($Angle_{\text{light}} = 45^\circ - \text{rotateY} \times 0.5$).

### B. Luminance Threshold Bloom Halos
- **Threshold:** Pixels with luminance $L > 0.85$ bleed into adjacent pixels with exponential decay:
  $$\text{Bloom}(x, y) = \text{Intensity} \times e^{-\frac{r^2}{2\sigma_{\text{bloom}}^2}}$$
- **Anamorphic Streak:** Horizontal bloom spread ($\sigma_x = 4 \times \sigma_y$) produces signature cinematic blue streak flares.

---

## 8. Compositing & Layer Blending Modes (`mix-blend-mode`)

| Blend Token | Mathematical Operation | Visual Role | Key Usage |
| :--- | :--- | :--- | :--- |
| **`blend-normal`** | Direct alpha over | Opaque solid layers, text blocks | UI cards, primary copy |
| **`blend-screen`** | $1 - (1-A)(1-B)$ | Additive luminous glow, flares | Sparks, laser trails, lens flares |
| **`blend-multiply`** | $A \times B$ | Subtractive dark tint, vignettes | Drop shadows, ink stamps on paper |
| **`blend-overlay`** | Screen/Multiply combo | Contrast enhancement, surface sheen | Grain textures, glass reflections |
| **`blend-color-dodge`**| $B / (1 - A)$ | Hyper-bright energy ignition | Neon impacts, energy shield strikes |

---

## 9. Motion Blur & Shutter Angle Policy

- **`blur-disabled` (0° Shutter):** Mandatory for all readable text, UI buttons, numeric counters, and brutalist cuts.
- **`shutter-180` (180° Shutter):** Standard cinematic motion blur ($50\%$ frame exposure time) for 3D camera dollies, whips, and scene exits.
- **`shutter-360` (360° Shutter):** Hyper-speed motion blur ($100\%$ frame exposure time) strictly for warp transitions and speed-of-light sting cuts.

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

## 11. Physically-Accurate Dual-Shadow Model (AO + Penumbra)

Every elevated 2.5D element generates two simultaneous shadow components:

### A. Contact Seam / Ambient Occlusion (`shadow-ambient-occlusion`)
- **Physics:** High-density light blockage at the exact surface contact line.
- **Specification:** `0px 2px 4px rgba(0, 0, 0, 0.60)` (Invariant with elevation, snaps tightly to object base).

### B. Directional Penumbra (`shadow-directional-penumbra`)
- **Physics:** Soft diffuse shadow expanding and fading as elevation $Z$ increases.
- **Dynamic Formula:**
  - $\text{OffsetY} = Z \times 0.40$
  - $\text{BlurRadius} = Z \times 0.85$
  - $\text{Opacity} = \frac{0.25}{1 + (Z \times 0.005)}$

---

## 12. OLED Anti-Banding, Blue-Noise Dither & HDR Headroom

### A. Temporal Blue-Noise Dither Guard
- Dark background gradients (`#0a0a0c → #181824`) must inject a 2% monochromatic blue-noise dither layer (`dither-grain-subtle`) to eliminate 8-bit quantization banding artifacts on OLED and high-contrast displays.

### B. HDR Specular Peak Headroom
- For HDR master pipelines (Apple XDR / HDR10):
  - Standard UI & Content White: $100\text{ nits}$ ($1.0\times$ SDR reference).
  - Specular Light Sweeps & Laser Flares: $400\text{ – }1000\text{ nits}$ ($4.0\times – 10.0\times$ peak headroom for lifelike luminance punch).

