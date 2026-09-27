# 07 State Machines, Scroll-Scrub & Gesture Interaction Models

Interactive and responsive systems require deterministic state machines and well-defined input driver models.

---

## 1. Input Driver Models

Specify the control driver for every interactive section:

### A. Clock-Driven (`driver: clock`)
- Progresses along a fixed timeline in seconds.
- Standard for video scenes, auto-playing product demos, and micro-feedback stings.

### B. Scroll-Driven Scrubbing (`driver: scroll_scrub`)
- Keyframe progress is bound to viewport scroll percentage (`0.0 → 1.0`).
- **`pin_duration`:** Viewport pinning distance in pixels (e.g., `pin: 1500px`).
- **`scrub_smoothing`:** Inertial lag on scroll release (`0.5s` damping).

### C. Gesture & Velocity-Driven (`driver: velocity_gesture`)
- Direct touch/pointer dragging with momentum fling.
- **`rubber_band_factor`:** Resistance when dragged past boundaries (`0.15`).
- **`fling_decay`:** Exponential deceleration curve upon release.

---

## 2. Core Interactive States

| State | Purpose | Default Physical Character |
| :--- | :--- | :--- |
| **`rest`** | Idle baseline state. | Neutral scale (1.0), zero elevation, calm. |
| **`hover`** | Cursor presence / preview. | Micro elevation, scale lift (1.03), accent glow. |
| **`active` / `pressed`** | Tactile actuation / click. | Instant compression (`scale: 0.96`), shadow collapse. |
| **`focused`** | Keyboard / accessibility navigation. | Focus ring outline, clear high-contrast cue. |
| **`settle` / `released`** | Deceleration back to rest or next view. | Damped spring return (`spring-snappy`). |
| **`disabled`** | Non-interactive locked state. | `opacity: muted`, zero motion response. |

---

## 3. State Machine Specification Template

```yaml
state_machine:
  id: "hero-interactive-card"
  driver: "clock" # clock | scroll_scrub | velocity_gesture
  initial: "rest"
  states:
    rest:
      properties:
        scale: 1.0
        translateY: 0px
        boxShadow: "var(--elevation-card)"
      on:
        POINTER_ENTER: "hover"
        FOCUS: "focused"

    hover:
      properties:
        scale: 1.03
        translateY: -4px
        boxShadow: "var(--elevation-lifted)"
      transition:
        duration: "fast"
        easing: "spring-snappy"
      on:
        POINTER_LEAVE: "rest"
        POINTER_DOWN: "pressed"

    pressed:
      properties:
        scale: 0.96
        translateY: -1px
        boxShadow: "var(--elevation-card)"
      transition:
        duration: "instant"
        easing: "ease-out-cubic"
      on:
        POINTER_UP: "settle"

    settle:
      properties:
        scale: 1.0
        translateY: 0px
      transition:
        duration: "fast"
        easing: "spring-gentle"
      on:
        AUTO_AFTER_SETTLE: "rest"
```
