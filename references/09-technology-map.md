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
| **`spring-snappy`** | CSS Spring / JS Spring | `CustomBounce` / Elastic | Expression Spring (freq: 3, decay: 8) | Rive Spring transition (`mass: 1, stiffness: 200, damping: 20`) |

---

## 2. Downstream Environment Guidelines

### A. Web (GSAP / Framer Motion / CSS)
- Pure `from → to` property pairs map directly to timeline tweens (`gsap.fromTo(...)` or `motion.div animate={{...}}`).
- Named spatial tokens (`--spatial-normal`) map to CSS custom properties.

### B. Video & Motion Graphics (After Effects / Premiere / Remotion)
- Scene beats map to composition markers and keyframe spans.
- Holds and Negative Time map directly to freeze spans between keyframe clusters.

### C. 2D Interactive (Rive / Lottie)
- The storyboard's `state_machine` maps directly to Rive State Machine Layers, Transitions, and Boolean/Trigger Inputs.
