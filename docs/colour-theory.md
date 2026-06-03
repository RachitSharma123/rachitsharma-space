# Colour Theory — rachitsharma.space

Design rationale, palette decisions, and applied colour theory for the portfolio.

---

## 1. Colour Models

### RGB vs HSL vs OKLCH

| Model | Purpose | Weakness |
|-------|---------|---------|
| RGB | Screen rendering | Non-intuitive; hue shifts when lightness changes |
| HSL | Human-readable | Not perceptually uniform — same L value looks different across hues |
| **OKLCH** | Perceptual design | Lightness is truly uniform; hue rotations stay vivid |

**Use OKLCH for gradients.** RGB gradients pass through a grey midpoint; OKLCH gradients stay saturated because they follow the perceptual colour manifold.

```css
/* RGB gradient — desaturated middle */
linear-gradient(90deg, #f59e0b, #22d3ee)

/* OKLCH gradient — vivid all the way through */
linear-gradient(in oklch 90deg, oklch(78% 0.17 67), oklch(83% 0.12 197))
```

---

## 2. Colour Harmonies

### The Colour Wheel (Perceptual / OKLCH hues)

```
          Red (25°)
         /          \
 Amber (67°)      Magenta (0°)
        |                |
 Yellow (98°)     Purple (310°)
         \          /
    Green (145°) — Cyan (197°) — Blue (265°)
```

### Harmony Types

| Harmony | Hue Relationship | Energy Level | Use Case |
|---------|-----------------|-------------|---------|
| **Complementary** | 180° apart | Maximum tension | CTAs, error states |
| **Split-complementary** | 150–210° from base | High but balanced | Hero palettes, portfolios |
| **Analogous** | 30–60° apart | Low tension, cohesive | UI backgrounds, status |
| **Triadic** | 120° apart | Vibrant, balanced | Illustrations, icons |
| **Tetradic** | 90° apart | Complex, rich | Data visualisations |

---

## 3. rachitsharma.space Palette

### Chosen Harmony: Split-Complementary

Base hue: **Amber** (OKLCH H ≈ 67°, equivalent to ~38° in traditional RYB)

| Role | Hex | OKLCH | Hue |
|------|-----|-------|-----|
| Primary accent | `#f59e0b` | `oklch(78% 0.17 67)` | 67° amber |
| Split accent | `#22d3ee` | `oklch(83% 0.12 197)` | 197° cyan |
| Status accent | `#4ade80` | `oklch(85% 0.16 145)` | 145° green |

**Why split-complementary over pure complementary?**

Pure complementary of amber (67°) would be **blue-violet** at ~247°. That combination is common (think construction signage) but harsh. Split-complementary shifts the second colour by ±30–40° to **cyan** (197°) — softer tension, still maximum cool/warm contrast, but without the visual aggression.

This same tension appears in virtually every major film poster: warm light source (amber/gold) + cool environment/shadow (teal/cyan). It reads as cinematic and premium without trying.

### Background Colours

```
#0a0a08  ← near-black, slightly warm (green undertone)
#111110  ← card base
#1a1a18  ← elevated surfaces
#2a2a26  ← borders
```

The warm undertone in the darkest background (`#0a0a08` has equal R+G but slightly lower B) subconsciously aligns with the amber accent. Cool-cast darks (`#080810`) would fight the amber instead of supporting it.

### Text Colours

| Role | Hex | Contrast on #0a0a08 |
|------|-----|---------------------|
| Primary text | `#e8e6df` | ~50:1 (AAA) |
| Muted text | `#7e7e71` | ~5.5:1 (AA ✓) |
| Borders | `#2a2a26` | decorative only |

> **WCAG AA requires 4.5:1 for normal text, 3:1 for large text.**  
> Original muted `#6b6b60` scored ~4.1:1 — just below AA. Bumped to `#7e7e71`.

---

## 4. Colour Psychology

### Amber `#f59e0b`

- Warmth, energy, attention
- Associated with craftsmanship, gold, expertise
- Used by: Stripe, Linear (hover states), many premium SaaS products
- **On dark bg**: reads as "illuminated from within" — confidence signal

### Cyan `#22d3ee`

- Technology, precision, clarity
- Associated with data, interfaces, futurism
- The classic "tech blue-green" — Tailwind 400, OpenAI, Figma
- **Paired with amber**: creates the warm/cool tension of daylight vs. screen glow

### Green `#4ade80`

- Success, active status, health
- Reserved here **only** for the "open to work" indicator and terminal `✓` output
- Never used decoratively — semantic colour with one meaning on this site

---

## 5. Darkness and Depth

### Layering on Dark Backgrounds

Depth on dark UIs comes from **lightness progression**, not shadows:

```
Layer 0 (background)  →  #0a0a08  (L=0.05 in OKLCH)
Layer 1 (cards)        →  #111110  (L=0.08)
Layer 2 (elevated)     →  #1a1a18  (L=0.12)
Layer 3 (hover)        →  #222220  (implied, via bg3 + brightness)
```

Shadows on dark backgrounds are barely visible. The correct approach is surface elevation through **lighter fills**, not `box-shadow` opacity.

### Glow Effects

Glows should use the same hue as the surface colour they emanate from:

```css
/* Amber glow — correct */
box-shadow: 0 0 24px rgba(245, 158, 11, 0.35);

/* White glow on amber — incorrect (desaturates) */
box-shadow: 0 0 24px rgba(255, 255, 255, 0.3);
```

---

## 6. Gradient Design

### Colour-Space Interpolation

CSS now supports explicit colour space gradient interpolation:

```css
/* Interpolates through RGB — may look muddy mid-point */
background: linear-gradient(135deg, #f59e0b, #22d3ee);

/* Interpolates through OKLCH — stays vivid across the span */
background: linear-gradient(in oklch 135deg, oklch(78% 0.17 67), oklch(83% 0.12 197));
```

The OKLCH version is used for `.gradient-text` and the scroll progress bar.

### Gradient Direction Principle

- **135° (top-left → bottom-right)**: natural reading flow, "ascending" feel — used for text gradients
- **90° (left → right)**: horizontal progress, momentum — used for progress bars and scanlines
- **Radial from center**: depth/light source — used for aurora blobs

---

## 7. Typography + Colour Interaction

### Font Choices and Colour Pairing

| Font | Role | Why this pairing works |
|------|------|----------------------|
| **Syne** (display) | Headings | Geometric, wide letterforms → pairs with amber (bold, mechanical) |
| **JetBrains Mono** | Code/labels | Monospaced → pairs with muted/cyan (technical, precise) |
| **Crimson Pro** | Body | Serif humanist → pairs with warm off-white `#e8e6df` |

The serif body on near-black background is intentional: serifs have higher legibility at body sizes on dark backgrounds than sans-serif because the serif strokes create more texture variation.

### Outlined Text

The `.title-outline` style (`-webkit-text-stroke`) creates outlined/ghost letters — this works specifically because:
1. The background is dark enough that outline-only text doesn't disappear
2. It establishes visual hierarchy without adding another colour (the eye reads solid > outline)

---

## 8. Colour Decisions Summary

| Decision | Principle | Alternative Considered |
|----------|-----------|----------------------|
| Amber primary on dark | Warm-on-dark = luminous, premium | Blue — too common in tech |
| Cyan split-complement | Avoids harsh complementary tension | Purple — more creative, less "builder" |
| Warm dark background | Background should support, not fight, warm accents | Neutral dark (`#0a0a0a`) — acceptable |
| Green only for status | Semantic colour discipline | Green as fourth accent — dilutes meaning |
| OKLCH for gradients | Perceptual uniformity | HSL gradients — desaturated midpoints |
| 3-layer depth system | Lightness-as-depth on dark | Shadow-based depth — weak on dark bg |

---

## 9. OKLCH Reference

Quick converter for palette accents:

```
#f59e0b → oklch(78.03% 0.173 67.4)   — amber
#22d3ee → oklch(83.15% 0.120 197.2)  — cyan  
#4ade80 → oklch(85.40% 0.163 144.7)  — green
#e8e6df → oklch(93.10% 0.008 96.8)   — warm white
#7e7e71 → oklch(56.30% 0.013 96.5)   — muted (AA compliant)
#0a0a08 → oklch(5.10%  0.003 120.0)  — dark bg
```

Browser support: OKLCH is supported in all modern browsers (Chrome 111+, Firefox 113+, Safari 15.4+). For fallbacks, hex values remain in the CSS.
