# 03 Atomic Motion Library

This document specifies the complete atomic motion unit catalog. Complex animations are constructed by sequencing and layering these fundamental atoms.

---

## 1. Composition Rules for Atoms

- **Single Anchor Law:** Only ONE primary atom in a scene carries maximum energy.
- **Anticipation & Volume Conservation:** Atoms marked `[Anticipation]` execute a 50–100ms micro-recoil with volume preservation ($\text{scaleX} \times \text{scaleY} \approx 1.0$).
- **Momentum Transfer & Elastic Restitution:** High-mass impacts transfer energy to adjacent low-mass elements, causing a proportional secondary recoil ($m_1 v_1 = m_2 v_2$).
- **Settle Integration:** Atoms marked `[Settle]` execute a 100–200ms damped deceleration into rest.
- **Spatial Trajectory:** Diagonal and multi-axis transitions follow `arc-convex` or `arc-concave` paths by default.
- **Transform Origin Declaration:** Every scaling/rotating atom must declare its origin (`origin-center`, `origin-bottom-center`, etc.).
- **Vector Morph Topology:** Morph atoms declare path topology (`matched_vertices` or `geometric_unfold`) to prevent self-intersections.
- **Max Atoms Per Element:** No single element may combine more than 3 simultaneous atoms.
- **Entrance & Exit Exclusivity:** An element cannot execute an entrance atom and an exit atom simultaneously.

---

## 2. Entrance Atoms (Elements arriving on screen)

| Atom Name | Description | Key Properties (`from → to`) | Default Duration | Default Easing | Reduced Motion Fallback | Cost |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `fade-in` | Simple opacity reveal | `opacity: 0 → 1` | `normal` | `ease-out-cubic` | `fade-in` (fast) | Low |
| `slide-in-up` [Settle] | Upward slide with organic settle | `translateY: var(--spatial-normal) → 0`, `opacity: 0 → 1` | `normal` | `ease-out-expo` | `fade-in` | Low |
| `slide-in-down` | Downward slide into position | `translateY: calc(-1 * var(--spatial-normal)) → 0`, `opacity: 0 → 1` | `normal` | `ease-out-expo` | `fade-in` | Low |
| `slide-in-left` | Leftward slide along the Current | `translateX: var(--spatial-large) → 0`, `opacity: 0 → 1` | `normal` | `ease-out-expo` | `fade-in` | Low |
| `scale-up` [Anticipation] | Scales up with volume preservation | `scale: (0.85, 0.85) → (1.0, 1.0)`, `opacity: 0 → 1` | `normal` | `spring-gentle` | `fade-in` | Low |
| `arc-fly-in` [Anticipation] | Enters along a convex trajectory | `x, y: path(arc-convex)`, `opacity: 0 → 1` | `slow` | `ease-out-expo` | `fade-in` | Med |
| `clip-reveal-up` | Cinematic reveal from clip mask | `clip-path: inset(100% 0 0 0) → inset(0)` | `slow` | `ease-out-expo` | `fade-in` | Med |
| `clip-reveal-left` | Reveal along the Current axis | `clip-path: inset(0 100% 0 0) → inset(0)` | `slow` | `ease-out-expo` | `fade-in` | Med |
| `split-reveal-h` | Unfurls from horizontal center | `clip-path: inset(0 50% 0 50%) → inset(0)` | `slow` | `ease-out-expo` | `fade-in` | Med |
| `blur-in` | Optical focus pull | `filter: blur(12px) → blur(0)`, `opacity: 0 → 1` | `normal` | `ease-out-cubic` | `fade-in` | High |
| `draw-in` | SVG path stroke drawing | `stroke-dashoffset: 100% → 0` | `slow` | `ease-in-out-cubic` | Instant show | Med |
| `counter-up` | Numeric data value roll | `textContent: 0 → targetNumber` | `slow` | `ease-out-expo` | Instant final value | Low |
| `typewriter-in` | Stepped character arrival | `width: 0 → 100%` / Char loop | `slow` | `steps(n)` | Instant show | Low |

---

## 3. Physics & Momentum Transfer Atoms

| Atom Name | Description | Key Physics Properties | Default Duration | Easing | Cost |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `physics.momentum-transfer` | Heavy hero impact launches adjacent micro-elements | `recoilY: -8px → 0px`, `mass_ratio: 0.2` | `fast` | `spring-snappy` | Low |
| `physics.elastic-restitution`| Surface rebound based on elasticity ($e = 0.75$) | `translateY: impact → recoil → rest` | `fast` | `spring-bouncy` | Low |

---

## 4. Particle & Emitter Dynamics

| Atom Name | Description | Key Physics Properties | Default Duration | Easing | Cost |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `particles.radial-burst` | 360° celebratory or click burst | `count: 16-24`, `spread: 360deg`, `gravity: 0.4`, `decay: 0.9` | `fast` | `ease-out-expo` | Med |
| `particles.directional-flow`| Particles flowing along bezier vector | `velocity: 250px/s`, `emission_rate: 12/s`, `spread: 15deg` | Continuous | `linear` | Med |
| `particles.ambient-bokeh` | Subtle floating luminous discs | `count: 8-12`, `scale: 4-12px`, `opacity: 0.15 → 0.4` | `glacial` | `ease-in-out-cubic` | Low |

---

## 5. Optical & Specular Light Atoms

| Atom Name | Description | Key Optical Properties | Default Duration | Easing | Cost |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `effects.light-sweep` | 45° metallic sheen across surface | `background-position: -200% → 200%`, `angle: 135deg` | `normal` | `ease-out-expo` | Med |
| `effects.glow-flare` | High-intensity luminous ignition | `filter: drop-shadow(0 0 24px accent)`, `opacity: 0 → 1 → 0` | `fast` | `spring-snappy` | High |

---

## 6. Typographic & Variable Font Atoms

| Atom Name | Description | Key Properties (`from → to`) | Default Duration | Default Easing | Cost |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `type.weight-morph` | Smooth optical weight transition | `font-variation-settings: 'wght' 200 → 800` | `normal` | `ease-out-expo` | Low |
| `type.width-stretch` | Dynamic kinetic width reveal | `font-variation-settings: 'wdth' 75 → 125` | `slow` | `ease-out-expo` | Low |
| `type.slant-snap` | Expressive italic emphasis | `font-variation-settings: 'slnt' 0 → -12` | `fast` | `spring-snappy` | Low |
| `type.tracking-breath` | Expands tracking in-flight, tightens on lock | `letter-spacing: +0.06em → -0.02em` | `normal` | `ease-out-expo` | Low |

---

## 7. Camera & Spatial 3D Atoms

| Atom Name | Description | Key Spatial Properties | Default Duration | Default Easing | Cost |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `camera.pan-x` | Horizontal camera track across space | `camera.x: 0 → targetX` | `slow` | `ease-out-expo` | Med |
| `camera.dolly-in` | Push-in toward focal anchor (Z-forward) | `camera.z: 0 → targetZ`, `scale: 1.0 → 1.35` | `slow` | `ease-out-quart` | Med |
| `camera.dolly-out` | Pull-out establishing wider scene | `camera.z: targetZ → 0`, `scale: 1.35 → 1.0` | `slow` | `ease-out-quart` | Med |
| `camera.rack-focus` | Depth shift between planes | `foreground.blur: 0 → 10px`, `midground.blur: 10px → 0` | `normal` | `ease-in-out-cubic` | High |

---

## 8. Emphasis & Squash Atoms

| Atom Name | Description | Key Properties | Default Duration | Default Easing | Reduced Motion Fallback | Cost |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `squash-impact` | Volume-conserved landing impact | `scaleY: 0.78, scaleX: 1.28 → (1.0, 1.0)` | `fast` | `spring-snappy` | None | Low |
| `scale-pop` [Anticipation] | Tactile punch with settle | `scale: 1.0 → 1.08 → 1.0` | `fast` | `spring-snappy` | Static highlight | Low |
| `ring-expand` | Radial ripple emanating outward | `scale: 1.0 → 1.4`, `opacity: 0.8 → 0` | `normal` | `ease-out-cubic` | None | Med |
| `underline-draw` | Accent line draws under hero word | `scaleX: 0 → 1`, `transformOrigin: left` | `normal` | `ease-out-expo` | Instant show | Low |
| `color-flash` | Transient signal color ignition | `color: ground → signal → ink` | `fast` | `ease-out-cubic` | Instant color snap | Low |
| `nudge` [Anticipation] | Micro directional shift | `translateX: 0 → -4px → 8px → 0` | `fast` | `spring-snappy` | None | Low |

---

## 9. Exit Atoms (Elements leaving the scene)

| Atom Name | Description | Key Properties | Default Duration | Default Easing | Reduced Motion Fallback | Cost |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `fade-out` | Clean disappearance | `opacity: 1 → 0` | `fast` | `ease-in-quad` | `fade-out` (fast) | Low |
| `slide-out-left` [Anticipation] | Accelerates out in Current direction | `translateX: 0 → calc(-1 * var(--spatial-large))`, `opacity: 1 → 0` | `fast` | `ease-in-expo` | `fade-out` | Low |
| `scale-down-out` | Shrinks away into background | `scale: 1.0 → 0.85`, `opacity: 1 → 0` | `fast` | `ease-in-quad` | `fade-out` | Low |
| `clip-hide-up` | Collapses upward behind mask | `clip-path: inset(0) → inset(0 0 100% 0)` | `normal` | `ease-in-quad` | Hide instantly | Med |
| `dissolve-blur` | Blurs out rapidly | `filter: blur(0) → blur(16px)`, `opacity: 1 → 0` | `fast` | `ease-in-quad` | `fade-out` | High |

---

## 10. Transition & Vector Morph Atoms

| Atom Name | Description | Key Properties | Default Duration | Default Easing | Continuity Role |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `cut-the-curve` | Exit & entry matched mid-velocity | `x: 0 → -100vw` (Exit) + `x: 100vw → 0` (Entry) | `normal` | `ease-in-expo` + `ease-out-expo` | Master Seam Standard |
| `morph-shape` | Shape A vertices interpolate to Shape B | `d: pathA → pathB`, `topology: matched_vertices` | `slow` | `ease-in-out-cubic` | Shared Element Carrier |
| `zoom-through` | Massive scale expansion revealing next beat | `scale: 1.0 → 8.0`, `opacity: 1 → 0` | `slow` | `ease-in-expo` | Deep Dive Vector |
| `carrier-dock` | Element flies across cut into new UI slot | `x, y, scale: posA → posB` | `slow` | `spring-gentle` | Direct Eye Carrier |
