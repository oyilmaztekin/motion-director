# 08 Cross-Platform Adaptation, Aspect Ratios & Accessibility (A11y)

Motion design must remain accessible, performant, and responsive across diverse viewports, social platforms, and user preferences.

---

## 1. Multi-Aspect Ratio & Safe Zone Standards

Modern motion design requires multi-format planning:

| Format | Aspect Ratio | Target Canvas | Safe Zone Rules |
| :--- | :--- | :--- | :--- |
| **Widescreen** | `16:9` (`1920x1080`) | Desktop Web, YouTube, Keynotes | 10% outer margin for text and focal anchors. |
| **Vertical** | `9:16` (`1080x1920`) | Reels, TikTok, Shorts, Mobile Stories | Avoid top 12% (header) and bottom 22% (captions/UI buttons). |
| **Square / Feed** | `1:1` (`1080x1080`) | Social Feeds, Instagram Post | Centered framing with 8% outer margin. |
| **Social Portrait**| `4:5` (`1080x1350`) | In-feed Mobile Video | 10% top/bottom margin. |

**Safe Zone Rule:** The focal anchor and core typographic message must remain strictly inside the Safe Zone across all target aspect ratios.

---

## 2. Mandatory Reduced Motion Compliance (WCAG 2.2 AAA)

**Rule:** Every single animated layer in `motion-director` MUST declare a `reduced_motion` fallback specification.

### Fallback Matrix:
| Standard Motion Atom | Reduced Motion Fallback | Rationale |
| :--- | :--- | :--- |
| `slide-in-*` / `parallax` | `fade-in` (`fast`) | Eliminates vestibular trigger from spatial movement. |
| `scale-up` / `zoom-through`| `fade-in` (`instant` / `fast`) | Eliminates motion sickness from depth zoom. |
| `rotate-in` / `page-flip` | `fade-in` (`fast`) | Eliminates disorientation from 3D tumbling. |
| `glow-pulse` / `shake-x` | Static border / highlight | Eliminates seizure/distraction triggers. |
| `typewriter-in` / `counter`| Instant final text/number | Eliminates visual flicker. |

---

## 3. Desktop vs Mobile Responsive Rules

1. **Spatial Scale Reduction:**
   - Desktop `translateY: 32px` → Mobile `translateY: 12px`.
   - Large hero travels on mobile cause overflow and visual distortion.
2. **Hover Substitution:**
   - On touch devices, `hover` state transitions are omitted or converted to direct tap feedback (`pressed`).
3. **Reduced Stagger Count:**
   - Cap staggered items on mobile to a maximum of **6 elements** (vs 12 on desktop) to prevent sluggish loading.

---

## 4. Performance, Compositor Isolation & GPU Budgets

- **Hardware Acceleration (Composite-Only):** Only animate composite-friendly properties (`transform: translate3d/scale/rotate`, `opacity`, `filter: blur` sparingly, and `clip-path`).
- **Layout Thrashing Guard:** Never animate geometry-reflowing properties (`top`, `left`, `width`, `height`, `margin`, `padding`) during high-frame-rate sequences.
- **Compositor Lifecycle Isolation:** Promote active layers via `will-change: transform, opacity` at animation ignition, and remove promotion on final settle hold to release GPU memory.
- **Max Concurrent Tweens:** Limit simultaneous active layer animations to **≤ 6** on desktop and **≤ 3** on mobile to guarantee silky 60fps / 120fps ProMotion execution.

---

## 5. Delta-Time Normalization ($\Delta t$) & Variable Refresh Rate (VRR)

To ensure animations play at identical real-world velocity across 60Hz, 120Hz (Apple ProMotion), and 240Hz displays:
- **Tick-Rate Independence:** Physics simulations (springs, particles, friction decay) must scale updates by the elapsed delta time ($\Delta t = t_{\text{current}} - t_{\text{previous}}$) rather than a fixed frame increment ($1/60\text{s}$).
- **Spring Time-Step Clamping:** Clamp maximum $\Delta t \le 33.3\text{ms}$ during tab backgrounding to prevent explosive physics tunneling upon window refocus.
