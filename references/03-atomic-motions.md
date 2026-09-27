# 03 Atomic Motion Library

This document specifies the complete atomic motion unit catalog. Complex animations are constructed by sequencing and layering these fundamental atoms.

---

## 1. Composition Rules for Atoms

- **Single Anchor Law:** Only ONE primary atom in a scene carries maximum energy.
- **Anticipation & Volume Conservation:** Atoms marked `[Anticipation]` execute a 50–100ms micro-recoil with volume preservation ($\text{scaleX} \times \text{scaleY} \approx 1.0$).
- **Viscous Hysteresis:** Spring oscillations dissipate asymmetrically (60% → 20% → 3% → lock).
- **Momentum Transfer & Elastic Restitution:** High-mass impacts transfer energy to adjacent low-mass elements, causing a proportional secondary recoil ($m_1 v_1 = m_2 v_2$).
- **Settle Integration:** Atoms marked `[Settle]` execute a 100–200ms damped deceleration into rest.
- **G2 Curvature Continuity:** Trajectories follow natural gravitational curves (`arc-convex` or `arc-concave`) with continuous acceleration derivative across bezier joins.
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
| `arc-fly-in` [Anticipation] | Enters along a G2-smooth convex path | `x, y: path(arc-convex, G2)`, `opacity: 0 → 1` | `slow` | `ease-out-expo` | `fade-in` | Med |
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
| `physics.hysteresis-settle` | Viscous asymmetric oscillation dampening | `dissipation: [0.60, 0.20, 0.03, 0]` | `normal` | `spring-gentle` | Low |

---

## 4. Particle & Emitter Dynamics

| Atom Name | Description | Key Physics Properties | Default Duration | Easing | Cost |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `particles.radial-burst` | 360° celebratory or click burst | `count: 16-24`, `spread: 360deg`, `gravity: 0.4`, `decay: 0.9` | `fast` | `ease-out-expo` | Med |
| `particles.directional-flow`| Particles flowing along bezier vector | `velocity: 250px/s`, `emission_rate: 12/s`, `spread: 15deg` | Continuous | `linear` | Med |
| `particles.ambient-bokeh` | Subtle floating luminous discs | `count: 8-12`, `scale: 4-12px`, `opacity: 0.15 → 0.4` | `glacial` | `ease-in-out-cubic` | Low |

---

## 5. Optical, Vector Trails & Specular Light Atoms

| Atom Name | Description | Key Optical Properties | Default Duration | Easing | Cost |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `effects.light-sweep` | 45° metallic sheen across surface | `background-position: -200% → 200%`, `angle: 135deg` | `normal` | `ease-out-expo` | Med |
| `effects.vector-trail` | Decaying multi-frame ghosting silhouette | `trail_count: 3`, `decay: 0.35`, `delay: 16ms` | `fast` | `ease-out-expo` | High |
| `effects.glow-flare` | High-intensity luminous ignition | `filter: drop-shadow(0 0 24px accent)`, `opacity: 0 → 1 → 0` | `fast` | `spring-snappy` | High |
| `effects.frosted-glass-refract` | Translucent refraction with chromatic dispersion | `backdrop-filter: blur(16px)`, `refractive_index: 1.52`, `split_offset: micro` | `normal` | `ease-out-cubic` | High |
| `effects.noise-shimmer` | Organic tactile surface grain modulation | `opacity: 0.02 → 0.05 → 0.02`, `frequency: 24fps` | Continuous | `linear` | Low |

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

## 10. Cinematic Transition & Montage Taxonomy (24 Master Transitions)

### A. Spatial & 3D Camera Transitions
| Atom Name | Description | Key Spatial Properties (`from → to`) | Default Duration | Easing |
| :--- | :--- | :--- | :--- | :--- |
| **`transition.whip-pan`** | High-velocity linear streak pan matching trajectory | `camera.x: 0 → -100vw`, `motion_blur: shutter-360` ($\theta_{\text{exit}}=\theta_{\text{entry}}$) | `fast` | `ease-in-expo` + `ease-out-expo` |
| **`transition.scale-plunge`** | Dives through a negative space opening/letter | `camera.z: 0 → +1500px`, `scale: 1.0 → 20.0`, `opacity: 1 → 0` | `slow` | `ease-in-expo` |
| **`transition.crash-zoom-out`**| Snap pullback from micro detail to macro world | `camera.z: -1200px → 0px`, `scale: 0.05 → 1.0` | `fast` | `spring-snappy` |
| **`transition.orbit-axial-flip`**| 3D camera rotates around axis to reveal reverse scene | `rotateY: 0° → 180°`, `transform_origin: center` | `normal` | `ease-in-out-cubic` |
| **`transition.parallax-slice`**| Depth planes slide at differential velocities | $v_{\text{fg}} = 1.8v_0$, $v_{\text{mid}} = 1.0v_0$, $v_{\text{bg}} = 0.2v_0$ in split directions | `normal` | `ease-out-expo` |

### B. Montage & Conceptual Match Transitions
| Atom Name | Description | Key Properties (`from → to`) | Default Duration | Easing |
| :--- | :--- | :--- | :--- | :--- |
| **`transition.match-cut-geometric`**| Shape silhouette and scale alignment across cut | `shapeA.circle → shapeB.pieChart`, `scaleA = scaleB` | `instant` / `fast` | `ease-out-cubic` |
| **`transition.match-cut-vector`** | Exit velocity vector matches entry velocity vector | $\vec{v}_{\text{exit}}(A) = \vec{v}_{\text{entry}}(B)$ along identical trajectory | `fast` | `cut-the-curve` |
| **`transition.match-cut-chromatic`**| Full-screen accent color becomes ground of next scene | `accent_fill: 100vw → next_scene.ground` | `fast` | `ease-out-expo` |
| **`transition.smash-cut`** | Zero-hold high-velocity cut on peak climax impact | Cut at peak velocity ($\vec{v}_{\text{max}}$), zero settle | `instant` | `linear` |
| **`transition.jump-cut-staccato`**| Rhythmic spatial hops along same camera axis | `camera.z: step1 → step2 → step3`, no angle change | `fast` per hop | `steps(1)` |

### C. Optics, Lens & Shutter Transitions
| Atom Name | Description | Key Optical Properties | Default Duration | Easing |
| :--- | :--- | :--- | :--- | :--- |
| **`transition.lens-flare-burn`** | Anamorphic streak / over-exposure wash | `brightness: 1.0 → 3.5 → 1.0`, `blend-screen` | `fast` | `ease-out-expo` |
| **`transition.rack-focus-defocus`**| Scene A pulls to bokeh, Scene B pulls sharp | `sceneA.blur: 0 → 16px` + `sceneB.blur: 16px → 0` | `normal` | `ease-in-out-cubic` |
| **`transition.chromatic-shatter`**| RGB prism split during high-speed transition | `split_offset: 0px → 12px → 0px` on RGB channels | `fast` | `spring-snappy` |
| **`transition.light-leak-sweep`** | Organic film burn wash sweeps across frame | `background: light-leak-gradient`, `blend-screen` | `normal` | `ease-out-expo` |

### D. Diegetic Occlusion & Portals
| Atom Name | Description | Key Mechanical Properties | Default Duration | Easing |
| :--- | :--- | :--- | :--- | :--- |
| **`transition.occlusion-wipe`** | Passing foreground object swipes camera revealing scene B | `translateForegroundX: -100vw → 100vw`, `clip-path` | `slow` | `ease-in-out-cubic` |
| **`transition.mask-portal-expand`**| Geometric shape expands from center to fill canvas | `clip-path: circle(0% at center) → circle(150%)` | `normal` | `ease-out-expo` |
| **`transition.split-curtain-unfold`**| Central seam opens like architectural shutters | `clip-path: split-horizontal(50% → 0%)` | `normal` | `ease-out-expo` |
| **`transition.cut-the-curve`** | Master velocity match mid-transit across cut | `x: 0 → -100vw` (Exit) + `x: 100vw → 0` (Entry) | `normal` | `ease-in-expo` + `ease-out-expo` |

### E. Material, Fluid & Morph Transitions
| Atom Name | Description | Key Physics Properties | Default Duration | Easing |
| :--- | :--- | :--- | :--- | :--- |
| **`transition.morph-dock`** | Persistent asset morphs topology into new UI container | `d: pathA → pathB`, `posA → posB`, `topology: matched` | `slow` | `spring-gentle` |
| **`transition.viscous-liquid-wipe`**| Gooey fluid wave sweeps across canvas | `gooey_threshold: alpha(0.85)`, `viscosity: 0.8` | `slow` | `spring-gentle` |
| **`transition.particle-dissolve-rebuild`**| Object disintegrates into particles and reconstructs | `particles.emit → particles.gather(targetShape)` | `slow` | `ease-in-out-cubic` |
| **`transition.paper-fold-origami`**| 2.5D geometric plane folds along diagonal vector | `rotate3d: (1, 1, 0, 180deg)`, `origin: diagonal` | `normal` | `spring-snappy` |

### F. Graphic & Typographic Transitions (Swiss / Brutalist)
| Atom Name | Description | Key Graphic Properties | Default Duration | Easing |
| :--- | :--- | :--- | :--- | :--- |
| **`transition.swiss-grid-slice`**| Columns/rows shift along typography grid lines | `translateY(col_odd): +100vh`, `translateY(col_even): -100vh` | `fast` | `ease-out-expo` |
| **`transition.invert-flash`** | 1-frame ink/ground color inversion | `color: invert(ground ↔ ink)` for 1 frame | `instant` | `steps(1)` |
| **`transition.kinetic-type-push`**| Massive header bulldozes previous scene off-screen | `translateX(heroText): 100vw → 0`, `sceneA: -100vw` | `normal` | `ease-out-expo` |

---

## 11. Vector Lines, Path Drawing & Path-Follow Atoms

| Atom Name | Description | Key Properties (`from → to`) | Default Duration | Easing | Cost |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **`vector.path-draw`** | Organic SVG stroke line write-on | `stroke-dashoffset: 100% → 0%`, `stroke-linecap: round` | `slow` | `ease-in-out-cubic` | Med |
| **`vector.path-follow`**| Element traverses along custom bezier curve | `offset-path: path(...)`, `offset-distance: 0% → 100%`, `auto_rotate: true` | `slow` | `ease-out-expo` | Med |
| **`vector.trim-offset`** | Trim start & end offset (AE Shape style) | `trim_start: 0% → 80%`, `trim_end: 20% → 100%`, `trim_offset: 0° → 360°` | `normal` | `ease-out-cubic` | Med |
| **`vector.minimal-line-wipe`**| Architectural hairline slicing across frame | `scaleX: 0 → 1`, `transform_origin: left`, `stroke_width: 1px` | `fast` | `ease-out-expo` | Low |

---

## 12. Organic Fluid Dynamics & Liquid Morph Atoms

| Atom Name | Description | Key Physics Properties | Default Duration | Easing | Cost |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **`liquid.blob-morph`** | Viscous droplet morphing with organic tension | `d: path(blobA) → path(blobB)`, `viscosity: 0.82` | `slow` | `spring-gentle` | High |
| **`liquid.surface-tension-merge`**| Two approaching elements merge via gooey bridge | `gooey_threshold: alpha(0.85)`, `bridge_radius: 24px` | `normal` | `spring-snappy` | High |
| **`liquid.droplet-splash`** | Tear-off droplet detaching and landing with recoil | `gravity: 0.5`, `elastic_recoil: 0.4`, `decay: 0.85` | `fast` | `physics.elastic-restitution` | High |
