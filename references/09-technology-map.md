# 09 Technology Translation Map (Engine-Agnostic Handoff)

`motion-director` produces **engine-agnostic specifications**. The storyboard focuses strictly on pure physics, timing tokens, layers, states, and choreography.

This document serves as a conceptual translation dictionary for downstream implementers when converting the master storyboard into target execution environments.

---

## 1. Token Translation Reference

| Storyboard Token | CSS / Web Standard | GSAP 3 | After Effects / Video | Rive / 2D Interactive |
| :--- | :--- | :--- | :--- | :--- |
| **`instant` (100ms)** | `0.1s` | `0.1` | 3 frames (@30fps) | 6 frames (@60fps) |
| **`fast` (200ms)** | `0.2s` | `0.2` | 6 frames | 12 frames |
| **`normal` (350ms)** | `0.35s` | `0.35` | 10–11 frames | 21 frames |
| **`slow` (600ms)** | `0.6s` | `0.6` | 18 frames | 36 frames |
| **`cinematic` (1200ms)**| `1.2s` | `1.2` | 36 frames | 72 frames |
| **`ease-out-expo`** | `cubic-bezier(0.16, 1, 0.3, 1)` | `"expo.out"` | Keyframe Velocity (In: 85%, Out: 0%) | Cubic curve `(0.16, 1, 0.3, 1)` |
| **`ease-out-cubic`**| `cubic-bezier(0.33, 1, 0.68, 1)`| `"power2.out"` | Keyframe Velocity (In: 65%, Out: 0%) | Cubic curve `(0.33, 1, 0.68, 1)` |
| **`spring-snappy` ($\zeta=0.7$)** | CSS `linear(...)` spring / Framer `{damping: 14, stiffness: 200}` | `CustomBounce` / Elastic | Expression `freq=3.5; decay=7.0;` | Rive Spring (`mass: 1, stiffness: 200, damping: 14`) |
| **`spring-gentle` ($\zeta=1.0$)** | Framer `{damping: 20, stiffness: 100}` (Critical) | `"power3.out"` | Keyframe Velocity (In: 75%, Out: 0%) | Rive Spring (`mass: 1, stiffness: 100, damping: 20`) |
| **`spring-heavy` ($\zeta=1.4$)** | Framer `{damping: 28, stiffness: 100}` (Overdamped)| `"expo.out"` | Keyframe Velocity (In: 90%, Out: 0%) | Rive Spring (`mass: 1.5, stiffness: 80, damping: 28`) |
| **`color_space: oklch`**| `color-mix(in oklch, c1, c2)` / `oklch(L C H)` | GSAP string / OKLCH plugin | Project Working Space: 32bpc Float Rec.709 | Hex / RGBA linear interpolation |

---

## 2. Downstream Environment Guidelines

### A. Web (GSAP / Framer Motion / CSS)
- **Transforms & GPU Promotion:** Map layers to `transform: translate3d(x, y, 0) scale(s) rotate(r)` and manage `will-change: transform, opacity` dynamically during active spans.
- **Cinematic Transitions:** Map `transition.morph-dock` and `transition.match-cut` to GSAP `Flip` plugin or Framer `layoutId`. Map `transition.mask-portal-expand` to CSS `clip-path: circle(...)`.
- **Vectors & Path Following:** Map `vector.path-draw` to GSAP `DrawSVGPlugin` (`drawSVG: "0% 100%"`) or CSS `stroke-dashoffset`. Map `vector.path-follow` to CSS `offset-path: path(...)` or GSAP `MotionPathPlugin`.
- **Liquid Morphs:** Map `liquid.blob-morph` to SVG `<feGaussianBlur>` + `<feColorMatrix>` gooey filter pipeline.
- **Color Interpolation:** Use CSS `color-mix(in oklch, ...)` or interpolate lightness/chroma channels independently.
- **Accessibility:** Wrap animations in `@media (prefers-reduced-motion: reduce)` fallback blocks or use Framer Motion's `useReducedMotion()`.

### B. Video & Motion Graphics (After Effects / Premiere / Remotion)
- **Timeline Markers:** Scene beats map directly to composition markers (`Intro_Start`, `Data_Reveal`, `Climax_Burst`, `Final_Settle`).
- **Montage Transitions:** Map `transition.whip-pan` to Null Object Camera Pans with Directional Blur. Map `transition.occlusion-wipe` to Alpha/Luma Track Mattes. Map `transition.scale-plunge` to 3D Layer Camera Z-Dolly.
- **Path & Shape Vectors:** Map `vector.trim-offset` directly to Shape Layer `Trim Paths` (`Start`, `End`, `Offset`). Map `vector.path-follow` to Layer `Auto-Orient along Path`.
- **Liquid Dynamics:** Map `liquid.blob-morph` to `CC Simple Choker` + `Fast Box Blur` adjustment layer stack.
- **Hold Spans:** Negative time translates to freeze spans between keyframe clusters.
- **Optics & Depth:** Focal lengths (`35mm`, `85mm`) map directly to After Effects 3D Camera layer properties.

### C. 2D Interactive (Rive / Lottie)
- **State Machine Layers:** The storyboard's `state_machine` maps directly to Rive State Machine Layers, Transitions, and Inputs (`trig_start`, `trig_climax`, `state_settled`).
- **Portals & Morphs:** Map `transition.mask-portal-expand` to Clipping Paths. Map `transition.morph-dock` to Bone Constraints and Vertex Interpolation.
- **Vector Paths:** Animate vector vertices and path trim directly on Rive shape paths with bones/constraints.
- **Hit-Area Protection:** Use transparent collision geometry to ensure interactive bounds conform to the Fitts's Law 44x44px standard.

---

## 3. Production Engine Implementation Recipes (The 5 Core VFX)

When implementing the storyboard into a target engine, implementers MUST use these exact technical recipes:

### Recipe 1: Liquid / Organic Metaballs (`effects.liquid-metaball`)

#### A. After Effects (ExtendScript / Adjustment Layer)
```javascript
// 1. Group moving shape elements inside a Pre-Comp ("Liquid_Precomp")
// 2. Add an Adjustment Layer on top with this exact effect stack:
var blur = adjLayer.Effects.addProperty("ADBE Fast Blur");
blur.property("Blurriness").setValue(60); // 40-80px range
blur.property("Repeat Edge Pixels").setValue(1);

var choker = adjLayer.Effects.addProperty("ADBE CC Simple Choker");
choker.property("Choke Matte").setValue(30); // 20-40px range

var displace = adjLayer.Effects.addProperty("ADBE Turbulent Displace");
displace.property("Size").setValue(25);
displace.property("Amount").setValue(15);
displace.property("Evolution").expression = "time * 120;";
```

#### B. CSS / SVG (Web / Canvas / GSAP)
```html
<svg class="goo-filter" style="display:none;">
  <defs>
    <filter id="liquid-goo">
      <feGaussianBlur in="SourceGraphic" stdDeviation="16" result="blur" />
      <feColorMatrix in="blur" mode="matrix" 
        values="1 0 0 0 0  
                0 1 0 0 0  
                0 0 1 0 0  
                0 0 0 24 -11" result="goo" />
      <feComposite in="SourceGraphic" in2="goo" operator="atop" />
    </filter>
  </defs>
</svg>
<style>
  .liquid-container { filter: url(#liquid-goo); }
</style>
```

#### C. GSAP MorphSVG Pipeline
```javascript
gsap.to(".liquid-droplet", {
  duration: 0.6,
  morphSVG: ".liquid-target-shape",
  ease: "expo.out",
  stagger: 0.04
});
```

#### D. Rive (2D Interactive)
- Use **Feathered Vertex Blends**: Deform mesh vertices using 2 dual bones with overlapping weights ($0.5 / 0.5$).
- Use a **Clipping Path** driven by an animated Path constraint with smoothing bezier handles.

#### E. WebGL / GLSL (SDF Metaballs)
```glsl
float smin(float a, float b, float k) {
    float h = clamp(0.5 + 0.5 * (b - a) / k, 0.0, 1.0);
    return mix(b, a, h) - k * h * (1.0 - h);
}
// Combine sphere SDFs with k = 0.35
float d = smin(length(p - p1) - r1, length(p - p2) - r2, 0.35);
```

---

### Recipe 2: Deep Cosmic Glow & Multi-Tier Optical Bloom (`effects.cosmic-glow`)

#### A. After Effects (32bpc Linear Stack)
```javascript
// 1. Core Luminous Layer (Blend Mode: Add / Screen)
// 2. Inner Glow Pass
var innerGlow = glowLayer.Effects.addProperty("ADBE Glo2");
innerGlow.property("Glow Threshold").setValue(75); // %
innerGlow.property("Glow Radius").setValue(18);    // px
innerGlow.property("Glow Intensity").setValue(2.2);

// 3. Outer Volumetric Atmosphere Pass
var outerGlow = glowLayer.Effects.addProperty("ADBE Glo2");
outerGlow.property("Glow Threshold").setValue(40);
outerGlow.property("Glow Radius").setValue(120);
outerGlow.property("Glow Intensity").setValue(0.9);

// 4. Anamorphic Flare Streak (Horizontal Stretch)
var streak = glowLayer.Effects.addProperty("ADBE Directional Blur");
streak.property("Direction").setValue(90); // Horizontal
streak.property("Blur Length").setValue(140);
```

#### B. CSS / Web
```css
.cosmic-glow-hero {
  filter: 
    drop-shadow(0 0 4px rgba(255, 255, 255, 0.95))
    drop-shadow(0 0 16px rgba(0, 229, 255, 0.85))
    drop-shadow(0 0 64px rgba(99, 102, 241, 0.50))
    drop-shadow(0 0 120px rgba(168, 85, 247, 0.30));
  mix-blend-mode: screen;
}
```

#### C. GSAP Animated Glow Pulse
```javascript
gsap.to(".cosmic-emitter", {
  filter: "drop-shadow(0 0 24px rgba(0,229,255,1.0)) drop-shadow(0 0 96px rgba(99,102,241,0.8))",
  duration: 0.8,
  yoyo: true,
  repeat: -1,
  ease: "sine.inOut"
});
```

#### D. Rive
- Use a **Multi-Stop Radial Gradient** on an overlay circle (`#FFFFFF 0%` -> `#00E5FF 25%` -> `#6366F1 60%` -> `transparent 100%`).
- Set Layer Blend Mode to **Screen** or **PlusLighter**.

---

### Recipe 3: Kinetic Speed Trails & Velocity Echoes (`effects.speed-trail`)

#### A. After Effects (Echo / Particle Stream)
```javascript
var echo = leadLayer.Effects.addProperty("ADBE Echo");
echo.property("Echo Time (seconds)").setValue(-0.015);
echo.property("Number of Echoes").setValue(10);
echo.property("Starting Intensity").setValue(1.0);
echo.property("Decay").setValue(0.85);
echo.property("Echo Operator").setValue(4); // Composite Behind (or Add)
```

#### B. CSS / SVG (Path Streaming)
```css
.velocity-trail-path {
  stroke-dasharray: 120 400;
  stroke-dashoffset: 0;
  animation: streamTrail 0.8s cubic-bezier(0.16, 1, 0.3, 1) infinite;
}
@keyframes streamTrail {
  0% { stroke-dashoffset: 0; opacity: 1; }
  100% { stroke-dashoffset: -520; opacity: 0; }
}
```

#### C. GSAP Physics Velocity Wake
```javascript
gsap.to(".trail-node", {
  x: "+=400",
  stagger: {
    each: 0.018,
    from: "start"
  },
  scale: (i) => 1 - (i * 0.08),
  opacity: (i) => Math.pow(0.85, i),
  ease: "expo.out"
});
```

---

### Recipe 4: Chromatic Dispersion & RGB Split (`effects.chromatic-split`)

#### A. After Effects (3-Channel Layer Split)
```javascript
// 1. Duplicate layer 3 times: Layer_Red, Layer_Green, Layer_Blue
// 2. Set blend mode to SCREEN for all 3 layers
// 3. Apply Shift Channels:
//    - Layer_Red:   Red from Red,   Green: Off, Blue: Off -> Position: [X - 4, Y]
//    - Layer_Green: Red: Off,       Green from Green, Blue: Off -> Position: [X, Y]
//    - Layer_Blue:  Red: Off,       Green: Off, Blue from Blue -> Position: [X + 4, Y]
```

#### B. CSS / Canvas
```css
.chromatic-glitch {
  text-shadow: 
    -3px 0 0 rgba(255, 0, 85, 0.75),
     3px 0 0 rgba(0, 230, 255, 0.75);
  animation: chromatic-twitch 0.3s steps(2) infinite;
}
```

---

### Recipe 5: Refractive Glass & Dual Contact Shadow (`effects.glass-caustics`)

#### A. After Effects (Frosted Panel & Dual Shadow)
```javascript
// AO Contact Shadow
var ao = cardLayer.Effects.addProperty("ADBE Drop Shadow");
ao.property("Distance").setValue(2);
ao.property("Softness").setValue(4);
ao.property("Opacity").setValue(153); // 60%

// Dynamic Penumbra
var penumbra = cardLayer.Effects.addProperty("ADBE Drop Shadow");
penumbra.property("Distance").setValue(24);
penumbra.property("Softness").setValue(48);
penumbra.property("Opacity").setValue(51); // 20%
```

#### B. CSS (visionOS Standard)
```css
.frosted-glass-card {
  background: rgba(255, 255, 255, 0.08);
  backdrop-filter: blur(24px) saturate(180%);
  -webkit-backdrop-filter: blur(24px) saturate(180%);
  border: 1px solid rgba(255, 255, 255, 0.18);
  border-top-color: rgba(255, 255, 255, 0.35);
  box-shadow: 
    0 2px 4px rgba(0, 0, 0, 0.60),       /* AO Contact */
    0 16px 32px -4px rgba(0, 0, 0, 0.35); /* Penumbra */
}
```

---

## 4. Anti-Amateurism Technical Verification Gate (Hard Execution Rules)

Before rendering or shipping code in any engine, verify against these 5 Non-Negotiables:

1. **No Linear Defaults:** Any keyframe with default $33.3\%$ linear ease is rejected. Keyframes must use asymmetric velocities (Minimum **In: 75%–85%**, Out: 0%–15% for explosive impacts).
2. **Motion Blur Active:** Motion blur is mandatory for all high-velocity translations ($\Delta x > 150\text{px}$ in $<300\text{ms}$).
3. **Multi-Pass Glow Only:** Single un-feathered glows look amateurish. Glows must combine specular core ($0\text{px}$) with inner saturated bloom and outer ambient dispersion ($120\text{px}$).
4. **Fluid Edge Choking:** Liquid bodies must combine heavy blur ($\ge 40\text{px}$) with an alpha choking/threshold matrix to create surface tension pinch necks.
5. **Contact Shadow Snapping:** Floating cards must possess both an ambient occlusion seam ($Z=0\text{px}$) and a soft diffuse penumbra.

