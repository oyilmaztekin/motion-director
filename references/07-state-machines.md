# 07 State Machines, Scroll-Scrub & Gesture Interaction Models

Interactive, UI, and responsive systems require deterministic finite state machines, gesture-velocity handoffs, scroll-scrub triggers, and tactile haptic feedback.

---

## 1. Input Driver Models & Dynamic Velocity Handoff

Every interactive storyboard element or scene must declare its primary input driver:

### A. Clock-Driven (`driver: clock`)
- Progresses along an absolute or relative timeline in seconds.
- Standard for video scenes, autoplaying brand manifestos, automated product tours, and logo stings.

### B. Scroll-Driven Scrubbing (`driver: scroll_scrub`)
- Keyframe progress is strictly bound to viewport scroll progress ($\text{progress} \in [0.0, 1.0]$).
- **`pin_duration`:** Viewport pinning distance in physical pixels (e.g., `pin: 1500px`).
- **`scrub_smoothing`:** Inertial lag and damping on scroll release (e.g., `smoothing: 0.45s`).
- **`snap_points`:** Magnetic resting thresholds (e.g., `snap: [0.0, 0.33, 0.66, 1.0]`).
- **`direction_hysteresis`:** Direction-change trigger deadzone ($\Delta y \ge 12\text{px}$) to prevent jitter on scroll reversal.

### C. Gesture & Velocity-Driven (`driver: velocity_gesture`)
- Direct pointer/touch tracking with real-time physics simulation.
- **`rubber_band_factor`:** Exponential drag resistance past container boundaries ($k_{\text{rubber}} = 0.15$).
- **`fling_decay`:** Ballistic deceleration upon pointer release based on launch velocity:
  $$\vec{v}_{\text{fling}} = \frac{\Delta \vec{x}}{\Delta t}, \quad \vec{a}_{\text{friction}} = -\mu \cdot g \cdot \hat{v} \quad (\mu = 0.92)$$
- **`interruption_handling: velocity-inherit` (Mandatory):** When a user taps or catches an object mid-animation, the interactive engine inherits the active instantaneous velocity $\vec{v}_{\text{active}}$ as the initial gesture velocity, eliminating visual jump cuts or snap-to-target stutter.

---

## 2. Hit-Target Invariance & Fitts's Law Cushion

- **`hit_cushion_guard: 44px-minimum` (Mandatory):**
  - Interactive elements must preserve a minimum $44 \times 44\text{px}$ touch target bounding box across all visual states.
  - During tactile compression states (`scale: 0.94`), the active hit-area dynamically expands by $+6\text{px}$ invisible padding to prevent accidental pointer drop-offs.

---

## 3. Tactile Haptic Feedback Architecture

For mobile and spatial tactile interactions, state transitions bind to standard haptic vibration tokens:

| Haptic Token | Waveform / Intensity | Physical Metaphor | Bound Interaction |
| :--- | :--- | :--- | :--- |
| **`haptic: selection-tick`** | Light transient (10ms) | Mechanical watch gear click | Stepper increment, carousel card snap, tab switch |
| **`haptic: impact-light`** | Crisp impulse (25ms) | Light acrylic tap | Button hover lock, menu open |
| **`haptic: impact-medium`**| Solid impulse (45ms) | Magnetic dock snap | Card drop into container, toggle switch engage |
| **`haptic: impact-heavy`** | Deep resonant pulse (80ms)| Weighted mechanical latch | Climax confirmation, purchase swipe completion |
| **`haptic: success-pulse`** | Double harmonic chirp | Dual melodic ping | Form submission success, metric goal unlock |
| **`haptic: error-buzz`** | Triplet jagged buzz (3x30ms)| Rapid friction grind | Form validation error, boundary limit hit |

---

## 4. Master 7-State Interactive Lifecycle Matrix

```text
       [DISABLED] <── (disabled = true) ──┐
                                          │
 [REST] ── (pointer_enter) ──> [HOVER] ───┴─ (pointer_down) ──> [PRESSED]
   ▲                             │                                  │
   │                             └──────── (drag_start) ────────────┤
   │                                                                ▼
   │                                                           [DRAGGING]
   │                                                                │
   │                                                          (pointer_up)
   │                                                                │
   │                                                                ▼
   └──────── (rest_settle) ─── [SETTLE] <── (boundary_hit) ─── [FLING_FLIGHT]
```

| State | Purpose | Default Physical Character | Typical Easing / Spring | Haptic Binding |
| :--- | :--- | :--- | :--- | :--- |
| **`rest`** | Idle baseline state. | Scale 1.0, zero elevation, neutral shadow. | `linear` | None |
| **`hover`** | Cursor presence / preview. | Scale 1.03, elevation lift (-4px), border glow. | `spring-snappy` | `haptic: impact-light` |
| **`pressed`** | Tactile actuation / click. | Scale 0.96, translateY +1px, shadow pinch. | `ease-out-cubic` (instant) | `haptic: impact-medium` |
| **`dragging`** | Direct 1:1 pointer tracking. | Follows cursor with lag ($\Delta t = 16\text{ms}$), tilt angle proportional to drag speed. | Direct transform | None |
| **`fling_flight`**| Ballistic momentum decay. | Decelerates with friction $\mu = 0.92$, momentum transfer. | Dynamic physics decay | None |
| **`settle`** | Damped spring return to slot. | Underdamped bounce settling ($\zeta = 0.70$, $k = 180$). | `spring-snappy` | `haptic: selection-tick` |
| **`disabled`** | Non-interactive locked state.| Opacity muted (0.4), grayscale saturation 0%. | `ease-out-cubic` | `haptic: error-buzz` (on tap) |

---

## 5. Master State Machine YAML Specification Template

```yaml
state_machine:
  id: "hero-interactive-card"
  driver: "velocity_gesture" # clock | scroll_scrub | velocity_gesture
  initial: "rest"
  interruption_handling: "velocity-inherit"
  hit_cushion_guard: "44px-minimum"
  
  states:
    rest:
      properties:
        scale: 1.0
        translateY: "0px"
        boxShadow: "0px 2px 4px rgba(0,0,0,0.12)"
      on:
        POINTER_ENTER: "hover"
        FOCUS: "focused"
        POINTER_DOWN: "pressed"

    hover:
      properties:
        scale: 1.03
        translateY: "-4px"
        boxShadow: "0px 12px 24px rgba(0,0,0,0.18)"
      transition:
        duration: "fast"
        easing: "spring-snappy"
      haptic: "haptic: impact-light"
      on:
        POINTER_LEAVE: "rest"
        POINTER_DOWN: "pressed"

    pressed:
      properties:
        scale: 0.96
        translateY: "1px"
        boxShadow: "0px 1px 2px rgba(0,0,0,0.40)"
      transition:
        duration: "instant"
        easing: "ease-out-cubic"
      haptic: "haptic: impact-medium"
      on:
        POINTER_UP: "settle"
        DRAG_START: "dragging"

    dragging:
      physics:
        rubber_band: 0.15
        tilt_factor: 0.08 # deg per px/s
      on:
        POINTER_UP: "fling_flight"

    fling_flight:
      physics:
        friction_mu: 0.92
        terminal_velocity_threshold: "0.05px/ms"
      on:
        REST_REACHED: "settle"

    settle:
      properties:
        scale: 1.0
        translateY: "0px"
        boxShadow: "0px 2px 4px rgba(0,0,0,0.12)"
      transition:
        duration: "normal"
        easing: "spring-snappy"
      haptic: "haptic: selection-tick"
      on:
        AUTO_AFTER_SETTLE: "rest"

    disabled:
      properties:
        opacity: 0.4
        filter: "grayscale(100%)"
        scale: 1.0
      on:
        POINTER_DOWN: "rejected_tap"
      rejected_tap:
        animation: "shake-x"
        haptic: "haptic: error-buzz"
```

