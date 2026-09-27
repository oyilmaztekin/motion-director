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
- **Vectors & Path Following:** Map `vector.path-draw` to GSAP `DrawSVGPlugin` (`drawSVG: "0% 100%"`) or CSS `stroke-dashoffset`. Map `vector.path-follow` to CSS `offset-path: path(...)` or GSAP `MotionPathPlugin`.
- **Liquid Morphs:** Map `liquid.blob-morph` to SVG `<feGaussianBlur>` + `<feColorMatrix>` gooey filter pipeline.
- **Color Interpolation:** Use CSS `color-mix(in oklch, ...)` or interpolate lightness/chroma channels independently.
- **Accessibility:** Wrap animations in `@media (prefers-reduced-motion: reduce)` fallback blocks or use Framer Motion's `useReducedMotion()`.

### B. Video & Motion Graphics (After Effects / Premiere / Remotion)
- **Timeline Markers:** Scene beats map directly to composition markers (`Intro_Start`, `Data_Reveal`, `Climax_Burst`, `Final_Settle`).
- **Path & Shape Vectors:** Map `vector.trim-offset` directly to Shape Layer `Trim Paths` (`Start`, `End`, `Offset`). Map `vector.path-follow` to Layer `Auto-Orient along Path`.
- **Liquid Dynamics:** Map `liquid.blob-morph` to `CC Simple Choker` + `Fast Box Blur` adjustment layer stack.
- **Hold Spans:** Negative time translates to freeze spans between keyframe clusters.
- **Optics & Depth:** Focal lengths (`35mm`, `85mm`) map directly to After Effects 3D Camera layer properties.

### C. 2D Interactive (Rive / Lottie)
- **State Machine Layers:** The storyboard's `state_machine` maps directly to Rive State Machine Layers, Transitions, and Inputs (`trig_start`, `trig_climax`, `state_settled`).
- **Vector Paths:** Animate vector vertices and path trim directly on Rive shape paths with bones/constraints.
- **Hit-Area Protection:** Use transparent collision geometry to ensure interactive bounds conform to the Fitts's Law 44x44px standard.
