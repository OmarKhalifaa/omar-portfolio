# Design System — Omar Khalifa Portfolio

A reference for all design tokens, typography, components, and interaction patterns used in this portfolio.

---

## Fonts

| Role | Family | Weights | Usage |
|------|--------|---------|-------|
| **Display / Headings** | [Syne](https://fonts.google.com/specimen/Syne) | 400, 500, 600, 700, 800 | Hero headline, section headings, logo, card titles |
| **Body / UI** | [DM Sans](https://fonts.google.com/specimen/DM+Sans) | 300, 400, 500 | Body copy, nav links, buttons, meta labels, descriptions |

```html
<link href="https://fonts.googleapis.com/css2?family=Syne:wght@400;500;600;700;800&family=DM+Sans:ital,opsz,wght@0,9..40,300;0,9..40,400;0,9..40,500;1,9..40,300&display=swap" rel="stylesheet">
```

---

## Colour Tokens

### Dark Mode (default)

| Token | Value | Usage |
|-------|-------|-------|
| `--bg` | `#0C0C0B` | Page background |
| `--bg-2` | `#111110` | Card background |
| `--bg-3` | `#181817` | Elevated surfaces, hover states |
| `--bg-4` | `#1F1F1E` | Highest elevation surface |
| `--border` | `rgba(255,255,255,0.07)` | Default borders |
| `--border-2` | `rgba(255,255,255,0.12)` | Stronger borders, focus rings |
| `--text-1` | `#F5F4EE` | Primary text |
| `--text-2` | `#B8B8B1` | Secondary text, descriptions |
| `--text-3` | `#7A7A73` | Muted text, labels, hints |
| `--accent` | `#5DCAA5` | Brand green, highlights, badges |
| `--accent-dim` | `rgba(93,202,165,0.10)` | Accent tints, tag backgrounds |
| `--red` | `#E8524A` | Error / destructive states |
| `--nav-bg` | `rgba(12,12,11,0.85)` | Nav pill background (frosted) |
| `--surface-soft` | `rgba(255,255,255,0.04)` | Subtle surface tint |

### Light Mode (`[data-theme="light"]`)

| Token | Value |
|-------|-------|
| `--bg` | `#F5F3EC` |
| `--bg-2` | `#EFEDE5` |
| `--bg-3` | `#E5E2D8` |
| `--bg-4` | `#DCD9CE` |
| `--text-1` | `#111110` |
| `--text-2` | `#4A4A46` |
| `--text-3` | `#7A7A73` |
| `--accent` | `#1F8F6A` |
| `--red` | `#C4372F` |

---

## Typography Scale

| Element | Font | Size | Weight | Letter Spacing |
|---------|------|------|--------|----------------|
| Hero headline | Syne | `clamp(42px, 6vw, 80px)` | 700 | `-0.04em` |
| Section heading | Syne | `clamp(28px, 3vw, 40px)` | 700 | `-0.02em` |
| Card title | Syne | `18px` | 700 | `-0.02em` |
| Body | DM Sans | `15px` | 400 | — |
| Hero sub | DM Sans | `16px` | 300 | — |
| Nav links | DM Sans | `13px` | 400 | — |
| Tags / labels | DM Sans | `11px` | 500 | `0.03em` |
| Muted hints | DM Sans | `11px` | 400 | `0.06em` uppercase |

---

## Spacing & Layout

| Token | Value |
|-------|-------|
| Max content width | `1920px` (via dynamic padding) |
| Section padding (desktop) | `80px max(40px, calc((100% - 1920px) / 2))` |
| Section padding (mobile) | `72px 24px` |
| Hero padding (desktop) | `56px max(40px, ...) 72px` |
| Hero padding (mobile) | `96px 24px 88px` |
| Cards grid gap | `12px` |
| Card border radius | `18px` |
| Pill border radius | `100px` |

---

## Components

### Nav Pill
- Fixed, centred, frosted glass (`backdrop-filter: blur(14px)`)
- Expands on hover/focus-within to reveal links (desktop)
- Always expanded on mobile; auto-collapses when scrolling down, expands when scrolling up

### Halo Card (`.halo-card`)
- Dark surface card with `border-radius: 18px`
- On hover: radial fill glow follows the cursor (`--mx`, `--my` CSS vars set via JS `mousemove`)
- Border-halo: green radial gradient on border using CSS mask technique
- Lifts `translateY(-3px)` on hover
- Disabled on touch devices (`@media (hover: none)`)

### Buttons

| Variant | Class | Style |
|---------|-------|-------|
| Primary | `.btn-primary` | Filled `--text-1` background, `--bg` text |
| Ghost | `.btn-ghost` | Transparent, `--border` outline, `--text-2` text |

Both: `border-radius: 8px`, `font-size: 13px`, `DM Sans 500`

### Tags / Pills (`.card-tag`)
- `background: var(--accent-dim)`
- `color: var(--accent)`
- `border: 1px solid var(--border)`
- `border-radius: 4px`, `padding: 3px 8px`, `font-size: 11px`

### Available Badge
- Rounded pill with animated green dot (`box-shadow: 0 0 8px var(--accent)` + pulse animation)
- Fade-up entrance animation on load

---

## Motion & Interactions

| Interaction | Behaviour |
|-------------|-----------|
| Scroll reveal | `IntersectionObserver` adds `.visible` class at 10% threshold; elements fade + slide up |
| Card halo | `mousemove` → CSS custom properties `--mx` / `--my` → radial gradients on `::before` / `::after` |
| Hero halo | Same mouse-tracking technique on `#hero::before` with green tint |
| Custom cursor | Dot follows mouse with lerp easing (`0.15` factor via `requestAnimationFrame`) |
| Nav expand | `max-width` transition `1.7s cubic-bezier(0.22, 1, 0.36, 1)` |
| Theme switch | `background` / `color` transition `0.3s ease` on `body` |
| Scroll indicator | Animated mouse SVG — scroll wheel bobs down and fades via `@keyframes scrollWheel` |
| Noise overlay | SVG fractal noise on `body::before`, `opacity: 0.025` dark / `0.04` light |

---

## Card Thumbnail Palettes

| Class | Gradient |
|-------|----------|
| `.t1` | `#111624 → #161c2e` (blue-dark) |
| `.t2` | `#0f1a17 → #141f1c` (green-dark) |
| `.t3` | `#1a1412 → #201a16` (warm-dark) |
| `.t4` | `#181318 → #1e1520` (purple-dark) |

---

## Breakpoints

| Breakpoint | Behaviour |
|------------|-----------|
| `≤ 900px` | Single-column cards, stacked about grid, simplified nav, mobile hero padding |
| `(hover: none)` | Cursor hidden, halo FX disabled, touch-safe interactions only |
