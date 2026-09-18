# Design Schema — Explore Learn Make (ELM)

> Single source of truth for colors, type, and logo usage across sites/apps, so it's not re-decided per project.
>
> **Last Updated:** 2026-08-22

---

## Color Palette

Two modes, sharing one naming convention so the tokens map directly across both — same idea, different values. Naming follows standard practice: `background`/`text` for the base, `primary`/`secondary` for brand identity, `accent` for interactive elements (with a `-hover` state), `tertiary` for low-emphasis decorative accents (tags, asides).

Theme: forest-and-metal in light mode (grounded, natural — the elm tree and its bark) — an alien bioluminescent forest at night in dark mode. Not "the same forest after dark" anymore; dark mode is its own register, leaning into neon/cyberpunk. The light-mode interactive color still ages from copper to verdigris on hover, echoing real metal oxidation.

### Light

| Token | Name | Hex | Usage |
| --- | --- | --- | --- |
| `background` | Cream | `#F5EEE0` | Page background |
| `text` | Ink | `#211C16` | Body text |
| `primary` | Forest | `#34503A` | Primary brand color — headings, primary UI elements |
| `secondary` | Bark | `#6B4A32` | Supporting brand color — secondary text, outlines, dividers |
| `accent` | Copper | `#C17F3E` | Interactive elements (buttons, links) — default state. Pair with `text` (ink) on top, not white/cream. |
| `accent-hover` | Verdigris Patina | `#8CB6A9` | Interactive elements — hover state. Give hovered elements a thin `text`-colored border regardless of fill, since Patina alone is low-contrast against Cream. |
| `tertiary` | Leaf Dark | `#3F6644` | Tags, asides, low-emphasis accents |

### Dark

| Token | Name | Hex | Usage |
| --- | --- | --- | --- |
| `background` | Midnight Violet | `#13111C` | Page background |
| `text` | Off-white | `#EDEFEC` | Body text |
| `primary` | Coral | `#FF8C75` | Primary brand color — "alien bioluminescent foliage." Headings, primary UI elements. |
| `secondary` | Ash Violet | `#9685A3` | Supporting brand color — "metallic tree trunk." Secondary text, outlines, dividers. |
| `accent` | Bio Cyan | `#3FB6D6` | Interactive elements (buttons, links) — glow/highlight color |
| `accent-detail` | Magenta | `#FF3D8A` | Not a fill color — borders, hover glow, gradient "brush stroke" fades only |
| `tertiary` | Holo Lavender-Ice | `#C9D6F2` | Tags, asides — sits between Bio Cyan and Magenta on the color wheel for a holographic feel |

**Accessibility check:** every pairing above has been verified against WCAG AA (4.5:1 body text, 3:1 large text/UI) — not eyeballed, and this mode's colors also went through actual protanopia/deuteranopia simulation, not just contrast math. Two real findings that shaped the final picks: (1) the original dark-mode accent was a teal-green (Verdigris) — normal vision separated it from Coral easily (186.8 apart on a 0–441 scale), but under protanopia simulation that gap collapsed to 52.7, because red and green sit on exactly the axis that form of colorblindness can't distinguish. Swapping the accent to blue-leaning Bio Cyan fixed it (103–115 apart under simulation) without losing the "glow" feeling — blue-vs-red isn't on the confused axis. (2) A darker/muted verdigris variant was tested separately and rejected for only clearing 4.0:1 contrast (large/UI only, not body text) — confirms a muted patina green can genuinely fall short against near-black, not just a feeling. General lesson: when adding a new color here, check it both for contrast (vs background) and for distance from every existing color under colorblind simulation, not just how it looks to normal vision — a color that reads as obviously distinct can still collapse into a neighbor under simulation. [WebAIM's contrast checker](https://webaim.org/resources/contrastchecker/) covers contrast; there's no simple equivalent link for colorblind simulation, ask for it to be re-run if a new color is added.

### Functional (Success / Warning / Error)

| Token | Mode | Hex | Contrast vs background | Notes |
| --- | --- | --- | --- | --- |
| `success` | Light | `#34503A` (= `primary`/Forest) | 7.7:1 | Reused rather than adding a 3rd green — no dedicated green cleared 4.5:1 while staying visually distinct from Forest/Leaf Dark. Doubles nicely as "growth." |
| `warning` | Light | `#8A4200` (Rust) | 6.4:1 | New color, kept clearly separated from Copper |
| `error` | Light | `#B3261E` | 5.7:1 | New color, red was unclaimed in this mode |
| `success` | Dark | `#4ADE80` | 10.7:1 | Green is unclaimed now that the accent moved to Bio Cyan |
| `warning` | Dark | `#F7C948` | 11.9:1 | Pushed clearly away from Coral |
| `error` | Dark | `#FF3B3B` | 5.3:1 | Threaded between Coral and Magenta — the tightest fit of the six |

**Hard rule, not a suggestion:** WCAG 1.4.1 prohibits color as the _only_ way to convey information. Every success/warning/error state must ship with an icon (✓ / ⚠ / ✕ or equivalent) and a text label at all times — never a color change alone (not just a fallback for bad cases; applies uniformly to every state in both modes). This isn't optional styling — a colorblind visitor literally cannot tell light mode's Success and Error apart by color alone; simulation showed the two collapsing to nearly the same tone under both protanopia and deuteranopia. Dark mode's pair separates better under simulation, but the icon+label rule still applies there — consistency matters more than relying on a pair that "happens to" work.

Implementation note: alert/banner backgrounds should use a light tint of the functional color (roughly 10–15% opacity over the surface) with the full-strength color reserved for the icon, border, and heading text — avoids ever needing light text on a saturated fill.

---

## Typography

Two families: **Atkinson Hyperlegible Next** for everything readable, **Fira Code** for anything code-related. Sizes are still open — fill in the Size column once a scale is picked.

**Atkinson Hyperlegible Next** — variable font (weight axis confirmed 200–800 on Google Fonts), designed by the Braille Institute specifically for legibility — distinct shapes for easily-confused characters (`1`/`l`/`I`, `0`/`O`), which fits the accessibility bar the rest of this doc is held to. `Fira Code` is a monospace font for programmers with optional ligatures for sequences like `->` and `<=`, weights 300–700 via Google Fonts.

Google Fonts embed (self-contained if self-hosted later, but this is the simple path to start):

```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Atkinson+Hyperlegible+Next:wght@200..800&family=Fira+Code:wght@400..700&display=swap" rel="stylesheet">
```

| Role | Font Family | Weight | Size | Notes |
| --- | --- | --- | --- | --- |
| Heading 1 | Atkinson Hyperlegible Next | 700 (suggested) | | |
| Heading 2 | Atkinson Hyperlegible Next | 700 (suggested) | | |
| Heading 3 | Atkinson Hyperlegible Next | 600 (suggested) | | |
| Body | Atkinson Hyperlegible Next | 400 | | |
| Small / Label | Atkinson Hyperlegible Next | 500 (suggested — a touch heavier helps small text stay legible) | | |
| Code | Fira Code | 400 | | Code blocks, inline `code`, anything technical |

---

## Logo Usage

_Reference for what's already in `Assets/Branding/` and when to use each — this part's already decided, just documenting it._

| Version | Files | Use when |
| --- | --- | --- |
| Full mark, black (with text) | `ELM-logo-black.svg`, `ELM-logo-black-1500.png` | On light backgrounds, anywhere there's room for the full wordmark — headers, footers, print |
| Full mark, white (with text) | `ELM-logo-white.svg`, `ELM-logo-white-1500.png` | On dark backgrounds |
| Icon only, black | `ELM-logo-black-notext.svg`, `-16/32/180-notext.png` | Small placements where the wordmark won't be legible — favicon, small nav mark, app icon |
| Icon only, white | `ELM-logo-white-notext.svg`, `-16/32/180-notext.png` | Same as above, on dark backgrounds |
| Favicon | `favicon.ico` (16/32/48 embedded), plus the individual 16 & 32px PNGs | Browser tab icon — see note below |
| Apple touch icon | `ELM-logo-black-180.png` / `-180-notext.png` | `<link rel="apple-touch-icon">`, 180×180 |
| Social share | `ELM-logo-social-share-black.png`, `-white.png` | Open Graph / Twitter card preview image |

**Suggested rule of thumb** (edit if you land on something different): use the icon-only mark at anything smaller than roughly 32px tall — the wordmark stops being readable below that. Full mark everywhere it fits.

**Minimum clear space:** _not yet defined — a common approach is "clear space equal to the height of the icon mark on all sides," but decide what looks right for this logo and note it here._

---

## Spacing Scale (optional)

_Only fill this in if you want a consistent spacing system across projects — e.g. a set of margin/padding values everything pulls from instead of arbitrary pixel values per project._

| Token | Value | Typical use |
| --- | --- | --- |
| xs | | |
| sm | | |
| md | | |
| lg | | |
| xl | | |

---

## Open Questions

- [ ] Type size scale — families and weights are set, sizes (H1/H2/H3/body/small) still need values
- [ ] Interactive states beyond hover — keyboard focus-visible (important for accessibility, not just mouse users) and disabled states aren't defined for either mode yet
- [ ] Minimum clear space for logo
