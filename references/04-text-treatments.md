# 04 Text Treatments, Variable Fonts, Kerning Guards & Kinetic Tracking

Text is the primary carrier of direct conceptual meaning. This document defines typographic decomposition, Variable Font axis interpolations, optical cap-height vertical alignment, kerning collision guards, non-linear stagger falloffs, kinetic tracking breathing, reading economics, and audio synchronization.

---

## 0. Typographic Hierarchy & Kinetic Physics Scope

Kinetic physics must respect visual hierarchy. Never apply complex micro-physics uniformly across all text blocks.

| Typographic Role | Target Matter | Allowed Kinetics | Forbidden Kinetics | Primary Decomposition |
| :--- | :--- | :--- | :--- | :--- |
| **Hero / Headline / Claim** | `Type` (Primary) | Full kinetic physics: variable axis morph, tracking breath lock, cap-height alignment, optical kerning guard, sub-pixel snap | Constant idle wobble or jitter during read hold | `Word` / `Character` |
| **Sub-Header / Callout** | `Type` / `UI` | Staggered slide, clip reveals, subtle weight accents | Extreme tracking expansion (>0.04em) | `Line` / `Word` |
| **Body Paragraph / Narrative** | `Text Block` | Simple line/block mask reveals, clean vertical slide, soft fade | Tracking breathing, width morphing, character scramble, baseline shifts | `Line` / `Block` |
| **Data Metric / Numeral** | `Data` | Odometer roll, counter interpolation, tabular monospace lock | Non-tabular kerning shifts (causes digit jitter) | `Character` / `Tabular` |
| **Micro-Label / HUD Tag** | `UI` | Stepped typewriter, instant flash cut, decode matrix | Overdamped soft tweens | `Character` / `Block` |

---

## 1. Optical Cap-Height Alignment, Diacritic Safe-Boxes & Sub-Pixel Snapping

### A. Optical Cap-Height Alignment (Zero Baseline Hop)
- **`vertical_alignment: cap-height-centered` (Mandatory for Hero Reveals):** Anchors the vertical transformation origin to the font's capital height box ($CapHeight \approx 0.70 \times FontSize$), eliminating baseline hopping during dynamic font-weight or font-width interpolations.
- **`vertical_alignment: baseline-locked`:** Used strictly for multi-line paragraphs to maintain rigid typographic grid alignment.

### B. Kinetic Kerning Collision Guard
- In ultra-fast character staggers (<40ms per glyph), adjacent critical letter pairs (e.g., `AV`, `To`, `WA`, `LT`) visually collide during rotation or weight morphing.
- **`kerning_guard: dynamic-pair-protection`:** Applies temporary optical kerning expansion (+0.02em) between collision-prone pairs during active flight, snapping to true metric kerning upon settle.

### C. Optical Mask Padding (Diacritic & Descender Safe-Box)
- When utilizing line-split `overflow: hidden` or `clip-path` masks, typographic accents and tails are vulnerable to premature clipping.
- **`mask_optical_padding: { top: 0.20em, bottom: 0.28em }` (Mandatory):**
  - **Top Clearance (0.20em):** Protects capital accents and tall diacritics (`İ`, `Ö`, `Ü`, `Ä`, `Â`, `Ê`, `Å`, `d`, `h`, `t`).
  - **Bottom Clearance (0.28em):** Protects deep descenders and cedillas (`g`, `j`, `p`, `q`, `y`, `ç`, `ş`, `ß`).

### D. Sub-Pixel Baseline Snapping (Anti-Aliasing Guard)
- Floating-point Y-axis transforms (e.g., `translateY(14.342px)`) cause GPU rasterizers to blur letterform stems across fractional physical pixels.
- **`subpixel_snap: display-pixel-rounded`:** During hold frames and the final 10% of deceleration curves, round all spatial offsets to the nearest physical integer pixel ($y = \text{round}(y)$).

---

## 2. Variable Font Axis Morphing & Tracking Kinetics

### A. Intrinsic Font Axis Morphs
| Axis | Tag | Range | Narrative Purpose | Default Easing / Spring | Layout Reflow Impact |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Weight** | `'wght'` | `100 → 900` | Authority, stress emphasis, crescendo | `ease-out-expo` | Expands bounding box |
| **Grade** | `'GRAD'` | `-200 → +150` | Layout-safe weight increase without reflow | `spring-snappy` | **Zero reflow** (Safe) |
| **Width** | `'wdth'` | `75% → 125%` | Expanding impact, panoramic reveal | `ease-out-expo` | Expands horizontally |
| **Slant / Italic** | `'slnt'` | `0° → -12°` | Kinetic urgency, speed, forward momentum | `spring-snappy` | Zero reflow |
| **Optical Size** | `'opsz'` | `8 → 144` | Dynamic focal shifts between micro and hero | `ease-out-cubic` | Subtle reflow |
| **Casual** | `'CASL'` | `0.0 → 1.0` | Formal authority shifting to friendly warmth | `spring-gentle` | Zero reflow |
| **Parametric Stroke**| `'XTRA'` | `400 → 600` | Custom vertical stroke modulation | `ease-out-quart` | Subtle reflow |

### B. Kinetic Tracking Breathing (Hero Statements Only)
- **Flight Phase:** Character spacing opens organically during flight: `letter-spacing: +0.06em → +0.08em`.
- **Settle Phase:** On final impact/settle, tracking snaps into a crisp, compressed lock: `letter-spacing: -0.02em`.
- **Constraint:** Forbidden on body paragraphs and data counters.

---

## 3. Decomposition Levels & Performance Budgets

| Level | Description | Recommended Usage | Performance & DOM Budget |
| :--- | :--- | :--- | :--- |
| **Block** | Entire paragraph or header as 1 unit. | Simple fade/slide, reduced-motion fallback. | Unlimited |
| **Line** | Text split into visual wrapped lines. | Cinematic editorial masks, clean reveals. | Up to 12 lines per viewport |
| **Word** | Text split by spaces into individual words. | Emphasis stagger, kinetic claims, manifestos. | Up to 35 words per scene |
| **Character** | Text split into individual glyphs. | Typewriter, decode, high-impact hero titles. | Max 20 characters per scene |
| **Phoneme / Syllable** | Words split into phonetic beats. | Audio lip-sync, musical syncopation. | Max 10 syllables per burst |

---

## 4. Non-Linear Stagger Falloff Curves

Linear stagger delay ($d = i \times s$) creates rigid robotic cascades. Use curved falloff distributions:

| Falloff Scheme | Calculation Formula | Visual Rhythm & Kinetic Feel |
| :--- | :--- | :--- |
| **`stagger-linear`** | $\text{delay} = i \times s$ | Uniform list cascades, neutral technical feeds. |
| **`stagger-exponential`**| $\text{delay} = s_{\text{base}} \times (1.18^i)$ | Rapid initial explosive burst settling into a calm trail. |
| **`stagger-gaussian`** | $\text{delay} = d_{\max} \times \exp\left(-\frac{(i - c)^2}{2\sigma^2}\right)$ | Symmetrical wave rippling outward from focal center $c$. |
| **`stagger-sine-wave`** | $\text{delay} = s_{\text{base}} \times \sin\left(\frac{i}{\text{count}} \times \pi\right)$ | Smooth undulating rolling wave across character sequence. |
| **`stagger-polyrhythmic`**| $\text{delay} = (i_{\text{word}} \times s_{\text{word}}) + (i_{\text{char}} \times s_{\text{char}})$ | Nested dual-tier cadence (words cascade at 50ms, chars within at 12ms). |

---

## 5. Master Text Pattern Library

| Pattern | Decomposition | Key Properties (`from → to`) | Easing / Spring Token | Duration Token | Default Stagger |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Mask Reveal (Overflow)** | Line | Parent: `overflow: hidden`<br>Child: `translateY: 110% → 0%`, `opacity: 0 → 1` | `ease-out-expo` | `slow` (450ms) | `from-start` (70ms) |
| **Mask Reveal (Clip)** | Line / Block | `clip-path: inset(100% 0 0 0) → inset(0)` | `ease-out-expo` | `slow` (400ms) | `from-start` (60ms) |
| **Variable Weight Pulse** | Word / Line | `font-variation-settings: 'wght' 300 → 800` | `ease-out-expo` | `normal` (300ms) | `from-start` (40ms) |
| **Tracking Breath Lock** | Word / Line | `letter-spacing: 0.08em → -0.02em`, `opacity: 0 → 1` | `ease-out-expo` | `slow` (500ms) | `from-start` (50ms) |
| **Slide & Settle** | Word / Line | `translateY: 24px → 0`, `opacity: 0 → 1` | `ease-out-cubic` | `normal` (350ms) | `from-start` (40ms) |
| **Split & Converge** | Word / Char | `translateX: offset → 0`, `scale: 0.9 → 1`, `opacity: 0 → 1` | `spring-gentle` | `slow` (550ms) | `from-center` (50ms) |
| **Typewriter Stepped** | Char | `visibility: hidden → visible` | `steps(1)` | `fast` (30ms/char)| `from-start` (30ms) |
| **Scramble / Decode** | Char | `content: randomChar → targetChar` | `linear` | `normal` (350ms) | `random` (25ms) |
| **Blur to Focus** | Word / Line | `filter: blur(12px) → blur(0)`, `opacity: 0 → 1` | `ease-out-cubic` | `normal` (350ms) | `from-start` (50ms) |
| **Rolling Numeral Odometer**| Char (Numeral)| `translateY: (targetDigit * -10%) → final`, `opacity: 1` | `spring-snappy` | `normal` (450ms) | `from-end` (60ms) |
| **Highlighter Marker Sweep**| Word / Line | `stroke-dashoffset: 100% → 0%` (SVG background draw) | `ease-out-quart` | `normal` (350ms) | `from-start` (80ms) |
| **Venetian Glyph Shutter** | Char / Line | Split even/odd slices: `translateY: ±100% → 0%` | `ease-out-expo` | `normal` (300ms) | `from-start` (30ms) |
| **Chromatic Split Impact** | Word | `text-shadow: ±4px 0 (Red/Cyan) → 0 0 transparent` | `spring-snappy` | `fast` (150ms) | At impact point |
| **Isometric 2.5D Extrusion**| Word / Line | `rotateX: 45° → 0°`, `rotateY: -20° → 0°`, `translateZ: 0` | `spring-gentle` | `slow` (600ms) | `from-center` (60ms) |

---

## 6. Reading Economics & Audio-Typographic Synchrony

### A. Mathematical Reading Speed & Hold Formula
To prevent rushed cuts, calculate the minimum scene hold duration based on word count $N$:

$$t_{\text{hold}} = \max\left(0.60\text{s}, \frac{N_{\text{words}}}{220} \times 60\text{s}\right) + t_{\text{settle}}$$

- **Reading Budget:** 220 words per minute ($272\text{ms}$ per word).
- **The Dramatic Comma ($t_{\text{settle}}$):** Always add an unconditional **$0.60\text{s} – 1.00\text{s}$ static rest** after the last character locks before initiating any exit transition.
- **Never Animate While Reading:** Continuous oscillation, drift, or pulsing on active body copy is strictly forbidden.

### B. Audio-Phonetic Synchronization
- **Hero Word Transient Lock:** Fire a crisp transient click or whoosh accent (`stem-sfx-hero`) at the exact timestamp ($t_{\text{impact}}$) where the primary emphasis word reaches 100% opacity and settles.
- **Speech Rhythm Matching:** Synchronize word reveal staggers to voiceover phoneme peaks ($\pm 16\text{ms}$ / 1 video frame tolerance).

---

## 7. Multilingual, RTL & CJK Spatial Grid Mechanics

### A. Right-to-Left (RTL) Locales (Arabic, Hebrew, Persian, Urdu)
- **Vector Inversion:** Dominant text flow mirrors: `current_vector: RIGHT` (flowing rightward).
- **Mask Inversion:** `clip-reveal-left` mirrors to `clip-reveal-right` (`clip-path: inset(0 0 0 100%) → inset(0)`).
- **Stagger Inversion:** Glyphs and words cascade from right to left (`stagger: from-end`).
- **Transform Origin:** Horizontal origins mirror: `origin-left-center` becomes `origin-right-center`.

### B. CJK Locales (Chinese, Japanese, Korean)
- **Square Em-Box Alignment:** CJK glyphs inhabit uniform square bounding boxes. Variable tracking breathing is **disabled** (`letter-spacing: 0`) to preserve ideographic balance.
- **Vertical Text Writing Modes (`writing-mode: vertical-rl`):**
  - The Current flows vertically downward (`+Y`).
  - Stagger sequences execute top-to-bottom, right-to-left.
- **Stroke-Order Vector Write-On:** Preferred reveal for high-impact single CJK characters is animated stroke-order vector path draw (`vector.path-draw`).

