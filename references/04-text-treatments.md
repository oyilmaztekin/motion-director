# 04 Text Treatments & Variable Typography Choreography

Text is the primary carrier of direct conceptual meaning. This document defines typographic decomposition, Variable Font axis interpolations, stagger choreography, reading economics, and audio synchronization.

---

## 1. Variable Font Axis Morphing (Modern Kinetic Typography)

When using Variable Fonts, animate intrinsic type axes instead of generic scaling or stretching:

| Axis | Tag | Range | Narrative Purpose | Easing |
| :--- | :--- | :--- | :--- | :--- |
| **Weight** | `'wght'` | `100 → 900` | Building authority, stress emphasis, crescendo | `ease-out-expo` |
| **Width** | `'wdth'` | `75% → 125%` | Expanding impact, panoramic reveal | `ease-out-expo` |
| **Slant / Italic** | `'slnt'` | `0° → -12°` | Kinetic urgency, speed, forward momentum | `spring-snappy` |
| **Optical Size** | `'opsz'` | `8 → 144` | Dynamic focal shifts between micro-label and hero | `ease-out-cubic` |

---

## 2. Decomposition Levels & Performance Budgets

| Level | Description | Recommended Usage | Performance Budget |
| :--- | :--- | :--- | :--- |
| **Block** | Entire paragraph or header as 1 unit. | Simple fade/slide, reduced-motion. | Unlimited |
| **Line** | Text split into visual wrapped lines. | Cinematic editorial masks, clean reveals. | Up to 8 lines |
| **Word** | Text split by spaces into individual words. | Emphasis stagger, kinetic claims. | Up to 25 words |
| **Character** | Text split into individual glyphs. | Typewriter, decode, high-impact hero titles. | Max 15–20 characters |

---

## 3. Text Pattern Library

| Pattern | Decomposition | Key Properties (`from → to`) | Easing Token | Duration Token | Stagger Default |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Mask Reveal (Overflow)** | Line | Parent: `overflow: hidden`<br>Child: `translateY: 110% → 0%`, `opacity: 0 → 1` | `ease-out-expo` | `slow` | `from-start` (80ms) |
| **Mask Reveal (Clip)** | Line / Block | `clip-path: inset(100% 0 0 0) → inset(0)` | `ease-out-expo` | `slow` | `from-start` (60ms) |
| **Variable Weight Pulse** | Word / Line | `font-variation-settings: 'wght' 300 → 800` | `ease-out-expo` | `normal` | `from-start` (40ms) |
| **Slide & Settle** | Word / Line | `translateY: 20px → 0`, `opacity: 0 → 1` | `ease-out-cubic` | `normal` | `from-start` (40ms) |
| **Split & Converge** | Word / Char | `translateX: offset → 0`, `scale: 0.9 → 1`, `opacity: 0 → 1` | `spring-gentle` | `slow` | `from-center` (50ms) |
| **Typewriter Stepped** | Char | `visibility: hidden → visible` | `steps(1)` | `fast` per char | `from-start` (35ms) |
| **Scramble / Decode** | Char | `content: randomChar → targetChar` | `linear` | `normal` | `random` (30ms) |
| **Blur to Focus** | Word / Line | `filter: blur(10px) → blur(0)`, `opacity: 0 → 1` | `ease-out-cubic` | `normal` | `from-start` (50ms) |

---

## 4. Reading Economics & The Dramatic Comma

1. **Reading Speed Budget:** Allocate at least **200–250ms per word** for comfortable human comprehension.
2. **The Dramatic Comma (Settle Hold):** Once the complete headline or claim is revealed, enforce a **minimum 0.5s – 1.0s static hold** before any secondary transition or scene cut occurs.
3. **Never Animate While Reading:** Do not apply continuous wobble, pulse, or drift to body text while the user is meant to read it.

---

## 5. Orchestration & Audio Accents

1. **Containers First:** Background cards or framing lines must reach ≥60% completion before text entrance begins.
2. **Text Leads Action:** The message lands before the CTA button appears.
3. **Audio Hit on Hero Word:** Trigger a subtle `sfx-click` or `sfx-whoosh` exactly as the primary emphasis word locks into place.
