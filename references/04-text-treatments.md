# 04 Text Treatments, Variable Fonts, Cap-Height Alignment & Kinetic Tracking

Text is the primary carrier of direct conceptual meaning. This document defines typographic decomposition, Variable Font axis interpolations, optical cap-height vertical alignment, non-linear stagger falloffs, kinetic tracking breathing, reading economics, and audio synchronization.

---

## 1. Optical Cap-Height Alignment (Zero Baseline Hop)

When animating font weight (`wght`), width (`wdth`), or font scale, text can vertically jitter if anchored to arbitrary CSS baselines.

- **`vertical_alignment: cap-height-centered` (Mandatory for Hero Reveals):** Anchors vertical center to the font's capital height box, eliminating baseline hopping during dynamic weight interpolations.
- **`vertical_alignment: baseline-locked`:** Used for inline text paragraphs to maintain strict typographic grid alignment.

---

## 2. Variable Font Axis Morphing & Tracking Kinetics

### A. Intrinsic Font Axis Morphs
| Axis | Tag | Range | Narrative Purpose | Easing |
| :--- | :--- | :--- | :--- | :--- |
| **Weight** | `'wght'` | `100 → 900` | Building authority, stress emphasis, crescendo | `ease-out-expo` |
| **Width** | `'wdth'` | `75% → 125%` | Expanding impact, panoramic reveal | `ease-out-expo` |
| **Slant / Italic** | `'slnt'` | `0° → -12°` | Kinetic urgency, speed, forward momentum | `spring-snappy` |
| **Optical Size** | `'opsz'` | `8 → 144` | Dynamic focal shifts between micro-label and hero | `ease-out-cubic` |

### B. Kinetic Tracking Breathing
- In flight, character spacing opens organically: `letter-spacing: +0.06em → +0.08em`.
- On final impact/settle, tracking snaps into a crisp, compressed lock: `letter-spacing: -0.02em`.

---

## 3. Decomposition Levels & Performance Budgets

| Level | Description | Recommended Usage | Performance Budget |
| :--- | :--- | :--- | :--- |
| **Block** | Entire paragraph or header as 1 unit. | Simple fade/slide, reduced-motion. | Unlimited |
| **Line** | Text split into visual wrapped lines. | Cinematic editorial masks, clean reveals. | Up to 8 lines |
| **Word** | Text split by spaces into individual words. | Emphasis stagger, kinetic claims. | Up to 25 words |
| **Character** | Text split into individual glyphs. | Typewriter, decode, high-impact hero titles. | Max 15–20 characters |

---

## 4. Non-Linear Stagger Falloff Curves

Linear stagger delay ($d = i \times s$) feels mechanical. Use curved falloff distributions:

| Falloff Scheme | Calculation Formula | Visual Rhythm |
| :--- | :--- | :--- |
| **`stagger-linear`** | `delay = index * stagger` | Standard uniform list cascades |
| **`stagger-exponential`**| `delay = base * (1.18 ^ index)` | Rapid initial burst settling into a calm trail |
| **`stagger-gaussian`** | `delay = maxDelay * exp(-((index - center)^2) / (2 * sigma^2))` | Symmetrical wave rippling out from focal center |

---

## 5. Text Pattern Library

| Pattern | Decomposition | Key Properties (`from → to`) | Easing Token | Duration Token | Stagger Default |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Mask Reveal (Overflow)** | Line | Parent: `overflow: hidden`<br>Child: `translateY: 110% → 0%`, `opacity: 0 → 1` | `ease-out-expo` | `slow` | `from-start` (80ms) |
| **Mask Reveal (Clip)** | Line / Block | `clip-path: inset(100% 0 0 0) → inset(0)` | `ease-out-expo` | `slow` | `from-start` (60ms) |
| **Variable Weight Pulse** | Word / Line | `font-variation-settings: 'wght' 300 → 800` | `ease-out-expo` | `normal` | `from-start` (40ms) |
| **Tracking Breath Lock** | Word / Line | `letter-spacing: 0.08em → -0.02em`, `opacity: 0 → 1` | `ease-out-expo` | `slow` | `from-start` (50ms) |
| **Slide & Settle** | Word / Line | `translateY: 20px → 0`, `opacity: 0 → 1` | `ease-out-cubic` | `normal` | `from-start` (40ms) |
| **Split & Converge** | Word / Char | `translateX: offset → 0`, `scale: 0.9 → 1`, `opacity: 0 → 1` | `spring-gentle` | `slow` | `from-center` (50ms) |
| **Typewriter Stepped** | Char | `visibility: hidden → visible` | `steps(1)` | `fast` per char | `from-start` (35ms) |
| **Scramble / Decode** | Char | `content: randomChar → targetChar` | `linear` | `normal` | `random` (30ms) |
| **Blur to Focus** | Word / Line | `filter: blur(10px) → blur(0)`, `opacity: 0 → 1` | `ease-out-cubic` | `normal` | `from-start` (50ms) |

---

## 6. Reading Economics & Audio Sync

1. **Reading Speed Budget:** Allocate at least **200–250ms per word** for comfortable human comprehension.
2. **The Dramatic Comma (Settle Hold):** Once the complete headline or claim is revealed, enforce a **minimum 0.5s – 1.0s static hold** before any secondary transition or scene cut occurs.
3. **Never Animate While Reading:** Do not apply continuous wobble, pulse, or drift to body text while the user is meant to read it.
4. **Audio Hit on Hero Word:** Trigger a subtle `sfx-click` or `sfx-whoosh` exactly as the primary emphasis word locks into place.
