# Kembali Basah — Design Guidelines

Companion to [brand-profile.md](brand-profile.md). Tokens live in [`src/styles/tokens.css`](../src/styles/tokens.css) and are the source of truth; this document explains how to use them.

## 1. Principles

1. **Water settles, fire sharpens.** Water is slow, smooth and low-contrast. Fire is small, sharp and bright. Never mix them in one motion.
2. **Data is the imagery.** Real satellite points are the hero. No stock photography.
3. **Quiet confidence.** Generous space, restrained colour, one accent per view.
4. **Indonesian first.** Layouts are designed for the Indonesian copy and checked in English.
5. **Colour is never the only signal.** Fire and recovery must differ by shape and text as well as hue.

## 2. Colour

### Roles

| Role | Token | Hex | Use |
|---|---|---|---|
| Peat | `--kb-peat-950` … `300` | `#1a130e` … `#b39c86` | Text, dark surfaces |
| Paper | `--kb-paper-50` … `200` | `#fbf7ef` … `#e5dac4` | Light surfaces |
| Tannin | `--kb-tannin-700` … `300` | `#8a4f18` … `#e2b47c` | **Water**, links, focus |
| Moss | `--kb-moss-800` … `100` | `#2f4423` … `#e2ead2` | **Recovery**, primary action |
| Ember | `--kb-ember-600` … `300` | `#c93d0b` … `#ff9b63` | **Fire only** |

**Ember means fire. Moss means rewetted or recovering.** Neither is ever used as decoration. If a screen has no fire data, it has no ember.

### Contrast (computed, WCAG 2.x)

| Pair | Ratio | Result |
|---|---|---|
| peat-950 on paper-50 (body) | 17.19 | AAA |
| peat-700 on paper-50 (secondary) | 10.63 | AAA |
| peat-500 on paper-50 (captions) | 5.42 | AA |
| tannin-700 on paper-50 (links) | 6.12 | AA |
| moss-700 on paper-50 | 7.29 | AAA |
| ember-600 on paper-50 (fire text) | 4.73 | AA |
| paper-50 on peat-950 (dark body) | 17.19 | AAA |
| peat-300 on peat-950 (dark captions) | 7.01 | AAA |
| tannin-300 on peat-950 | 9.67 | AAA |
| moss-300 on peat-950 | 9.31 | AAA |
| ember-500 on peat-950 (data points) | 5.38 | AA |
| paper-50 on moss-700 (button) | 7.29 | AAA |
| ember-500 vs moss-300 (against each other) | **1.73** | **fails: needs a shape cue** |

`tannin-600` on paper-50 is 4.54, which passes only for large or bold text. Use `tannin-700` for body links.

### The fire / recovery rule
Because ember and moss are not distinguishable from each other by contrast alone:

- **Fire** is a **filled dot with a glow**.
- **Rewetted** is a **ring (hollow dot)** with no glow.
- Legends, tooltips and the table view name the state in words.

## 3. Typography

| Role | Family | Why |
|---|---|---|
| Display | **Fraunces** (variable, optical size) | Warm, characterful serif with an editorial voice |
| Body / UI | **Public Sans** | Clear, neutral, built for public information; good Indonesian support |
| Data | **IBM Plex Mono** | Tabular figures for numbers, coordinates and timestamps |

Load with `next/font/google`, subset to Latin, `display: swap`.

| Step | Size | Use |
|---|---|---|
| `--kb-text-4xl` | 44 → 96px (fluid) | Home hero only |
| `--kb-text-3xl` | 36 → 64px | Page titles |
| `--kb-text-2xl` | 28 → 44px | Section titles |
| `--kb-text-xl` | 22 → 30px | Lead paragraphs, card titles |
| `--kb-text-lg` | 19 → 22px | Large body |
| `--kb-text-base` | 17px | Body |
| `--kb-text-sm` | 15px | UI labels |
| `--kb-text-xs` | 13px | Captions, data labels (never smaller) |

- Body line-height 1.6, headings 1.1 to 1.2, measure `66ch`.
- No text below 13px. Uppercase labels use letter-spacing 0.08em and `text-xs` or larger.
- Numbers in data contexts use `font-variant-numeric: tabular-nums`.

## 4. Logo

- **Mark** (`public/brand/logo-mark.svg`): a drop, a wavy water-table line inside it, and one ember above the line. It uses `currentColor` for the strokes and `--kb-ember` for the dot.
- **Lockup:** mark + "Kembali Basah" set in Fraunces, medium weight. Mark height equals the cap height of the wordmark × 1.6.
- **Clear space:** half the mark's width on every side. **Minimum size:** 24px tall for the mark alone.
- **Colour use:** peat on paper, paper on peat. The ember dot stays ember in both. On a single-colour print the dot may take the same colour as the strokes.
- **Don't:** recolour the dot to moss, add shadows or gradients, rotate, or put the mark over busy imagery.

## 5. Layout and space

- 4px base scale (`--kb-space-1` … `9`).
- Content max width `72rem`; gutters 16px on phones, 32px from 768px up.
- 12-column grid from 1024px, single column below. Text blocks never span more than `66ch`.
- Sections breathe: `--kb-space-8` to `--kb-space-9` between major sections on desktop.
- Radii: 6 (inputs, chips), 12 (cards), 20 (feature panels), pill (buttons, tags).
- Elevation is almost flat: a 1px border and a surface change, with a soft shadow only on floating layers.

## 6. Imagery

- **Primary:** the satellite point field.
- **Secondary:** contour lines (topographic) and peat strata cross-sections as line illustration, drawn in `peat-300` / `tannin-300` at low opacity.
- **Photography:** only if licensed and credited; duotone (peat to paper) if used.
- Every informative graphic has a text alternative or an adjacent table.

## 7. Motion

| | Water (calm) | Fire (sharp) |
|---|---|---|
| Easing | `--kb-ease-water` | `--kb-ease-fire` |
| Duration | 300 to 700ms | 150ms |
| Used for | Page transitions, the Rewet slider, reveals | Hotspot pulse, hover on fire data |

- Nothing loops forever except the hotspot pulse, and it pauses off screen.
- `prefers-reduced-motion: reduce` removes all movement. State changes become instant and the Rewet slider shows both states with a static comparison.
- No parallax, no scroll-jacking.

## 8. Components (first set)

| Component | Notes |
|---|---|
| Button | Primary = moss; secondary = outline; min height 44px; label always visible |
| Link | `tannin-700`, underlined; visible focus ring |
| Language switch | ID / EN; `lang` attribute updated on `<html>`; remembered |
| Stat | Mono figure + label + source line; illustrative figures carry an "Example" tag |
| Hotspot legend | Dot (fire) and ring (rewetted) with words |
| Map card | Canvas with a keyboard-reachable table alternative |
| Rewet slider | Native `<input type="range">`, labelled, with a text readout of the state |
| Story section | Single column, `66ch`, full-bleed figure |
| Concept notice | Persistent, calm banner: "Proyek konsep / Concept project" |
| Donate card (demo) | Clearly marked demo; never collects payment details |

## 9. Accessibility (WCAG 2.2 AA is the floor)

- Contrast per the table above; re-check any new colour pair.
- **Targets:** at least 24×24 CSS px (WCAG 2.5.8), 44px preferred on touch.
- **Focus:** 3px ring using `--kb-focus`, offset 2px, never removed.
- **Keyboard:** every interaction is reachable and operable by keyboard, including the map (via the table) and the Rewet slider.
- **Language:** `<html lang>` is correct, and inline passages in the other language carry their own `lang`.
- **Motion:** reduced-motion respected everywhere.
- **Forms:** visible labels, errors in text, no placeholder-only labels.
- **Skip link** to main content on every page.

## 10. Performance budget

| Metric | Budget |
|---|---|
| JS on the home page (compressed) | ≤ 150 KB |
| LCP (mobile, simulated) | ≤ 2.5 s |
| CLS | ≤ 0.05 |
| Total blocking time (mobile, simulated) | ≤ 200 ms |
| Fonts | ≤ 3 families, variable where possible, subset |
| Heavy interactive pieces | Loaded on demand, never on the critical path |

CI runs Lighthouse against these budgets and fails the build on regression.

## 11. Internationalisation

- Indonesian is the default locale (`/`), English at `/en`.
- All copy lives in dictionaries, none in components or images.
- Layouts tolerate ~15% longer strings.
- Dates and numbers use `Intl` with the active locale (Indonesian uses `.` for thousands and `,` for decimals).

## 12. Content states that must always be designed

Loading, empty, error, offline, "data is stale" (older than 24h), and "concept / example" labelling.
