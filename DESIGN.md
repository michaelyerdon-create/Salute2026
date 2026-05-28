# Salute Gala 2026 — Design System

## Fonts

| Role | Family | Weights |
|---|---|---|
| Display / Headings | **Zodiak** (Fontshare) | 400, 700 |
| Body / UI | **Source Sans 3** (Google Fonts) | 300, 400, 600, 700 |

Load order matters: Zodiak via `https://api.fontshare.com/v2/css?f[]=zodiak@700,400,1&display=swap`, Source Sans 3 via Google Fonts.

---

## Color Palette

### Brand Colors (primary — use these)

| Token | Hex | Use |
|---|---|---|
| `--dark-navy` | `#13235B` | Primary text, borders, headings on light |
| `--dark-forest` | `#0E2A1F` | Quote card background |
| `--cream` | `#F3EDE5` | Light section backgrounds (About, Leadership, Sponsorship) |
| `--pale-orange` | `#FCE6C5` | Warm section backgrounds (FAQ, Fundraise, Funds) |
| `--ywca-orange` | `#F33A1A` | CTAs, eyebrows, accents, prices, checks |

### Text Tokens

| Token | Value | Use |
|---|---|---|
| `--on-dark` | `rgba(255,255,255,0.88)` | Body text on dark backgrounds |
| `--on-dark-muted` | `rgba(255,255,255,0.5)` | Secondary text on dark |
| `--on-light` | `#13235B` | Body text on light backgrounds |
| `--on-light-muted` | `rgba(19,35,91,0.6)` | Secondary text on light |

### Legacy Tokens (used in nav, hero, buttons — do not remove)

| Token | Hex |
|---|---|
| `--persimmon` | `#F33A1A` (alias of `--ywca-orange`) |
| `--lavender` | `#CFC0FA` |
| `--lavender-mid` | `#A690CE` |
| `--plum` | `#8B72BE` |
| `--plum-dark` | `#6B5494` |
| `--navy` | `#1C2B52` |
| `--navy-dark` | `#131B35` |
| `--navy-deeper` | `#0D1225` |

---

## Section Backgrounds

| Section | Background |
|---|---|
| Hero | Dark gradient (navy→plum), pattern overlay |
| About | `--cream` |
| Honorees | `--dark-navy` |
| Sponsorship | `--cream` |
| Tickets | `--cream` |
| Legacy (Past Galas) | `--dark-navy` |
| Mission | `--dark-navy` |
| FAQ | `--pale-orange` |
| Fundraise | `--pale-orange` |
| What Salute Funds | `--pale-orange` |
| Final CTA | Dark gradient (same as hero) |
| Footer | `--navy-deeper` (`#0D1225`) |

Dark sections (Honorees, Legacy, Mission, CTA) share a repeating SVG pattern overlay at `opacity: 0.01`, `mix-blend-mode: screen` from `./brand.assets/LockupPatternViolet.svg`.

---

## Layout

```css
--content-max: 1200px;
--gutter: clamp(1.5rem, 5vw, 4rem);
--section-pad: clamp(3rem, 5vw, 4.5rem);
```

- `.container`: `max-width: 1200px; margin: 0 auto; padding: 0 var(--gutter);`
- `.section-pad`: `padding: var(--section-pad) 0;`
- Mobile breakpoint: `860px` (main), `640px` (grids)

---

## Typography Scale

### Eyebrow (shared component)
```css
font-size: 0.6875rem; font-weight: 700; letter-spacing: 0.4em; text-transform: uppercase;
color: var(--persimmon); /* --ywca-orange */
/* Decorative lines via ::before and ::after: width 2rem, height 1.5px */
```

### Section Headings (Zodiak)
- Large: `clamp(1.49rem, 2.55vw, 2.34rem)` — About, Sponsorship, Tickets, Legacy, Leadership
- CTA title: `clamp(1.7rem, 3.4vw, 2.98rem)`
- Honorees title: `clamp(1.25rem, 2.1vw, 2rem)`
- All headings: `font-weight: 700; letter-spacing: -0.01em; line-height: 1.0–1.15`

### Body
- Standard: `1rem; line-height: 1.45;`
- Mission body: `1rem; line-height: 1.8;`
- Small caps / labels: `0.58–0.72rem; font-weight: 700; letter-spacing: 0.2–0.4em; text-transform: uppercase;`

### Stat Numbers (About section)
```css
font-family: 'Zodiak', serif; font-size: clamp(1.49rem, 2.55vw, 2.13rem);
font-weight: 700; color: var(--dark-navy); letter-spacing: -0.02em;
```

---

## Buttons

### Primary — Persimmon/Orange
```css
.btn-persimmon { background: var(--persimmon); color: white; }
/* hover: darken 20%, translateY(-2px), box-shadow: 0 10px 30px rgba(250,70,22,0.35) */
```

### Ghost — Light (on dark backgrounds)
```css
.btn-ghost-light { background: transparent; color: white; border: 1px solid rgba(255,255,255,0.45); }
/* hover: border→lavender, color→lavender, translateY(-2px) */
```

### Shared `.btn` base
```css
padding: 1rem 2.5rem; font-size: 0.7rem; font-weight: 700;
letter-spacing: 0.25em; text-transform: uppercase;
transition: all 0.25s cubic-bezier(0.25, 0, 0, 1);
```

---

## Navigation

- Fixed, `z-index: 1000`
- Transparent on load → `rgba(13,18,37,0.92)` + `backdrop-filter: blur(16px)` on scroll (`.scrolled` class)
- Logo: YWCA logo, `height: 32px`, `filter: brightness(0) invert(1)`, `opacity: 0.9`
- Nav links: `0.7rem; font-weight: 600; letter-spacing: 0.18em; text-transform: uppercase; color: rgba(255,255,255,0.7)`
- CTA button: `.nav-cta` — persimmon background, `padding: 0.55rem 1.25rem; font-size: 0.65rem`
- Mobile menu: full-screen overlay with staggered link animations, same dark gradient as hero
- Hamburger: animated to × (3 spans, CSS transitions)
- Mobile breakpoint: `860px`

---

## Hero

- Full viewport height, dark gradient + radial overlays + pattern + glow layer
- Gradient: `#0d1225 → #141d50 → #291448 → #3a0e30` (diagonal)
- Staggered load animations with `@keyframes fadeUp` (translateY 20px → 0, opacity 0→1)
- All elements use `animation: fadeUp Xs Ys forwards` with delays from 0.2s–1.2s
- Scroll indicator: pulse animation on vertical line

---

## Cards & Surfaces

### Honoree Cards (on dark-navy)
```css
background: white; border: 1px solid rgba(19,35,91,0.1); padding: 2.25rem 2.5rem;
/* Top accent: 3px linear-gradient(90deg, --ywca-orange → orange/35%) */
/* hover: translateY(-5px), box-shadow: 0 24px 60px rgba(19,35,91,0.15) */
```

### FAQ Contact Card
```css
background: white; padding: 1.75rem; border-left: 3px solid var(--dark-navy);
```

### Mission Quote Card
```css
background: var(--dark-forest); padding: 3rem; overflow: hidden;
/* Decorative " via ::before — Zodiak, 10rem, rgba(255,255,255,0.06) */
```

---

## Accordions

### FAQ Accordion
- Trigger: `width: 100%; display: flex; justify-content: space-between; padding: 1.5rem 0;`
- Icon: 26px circle, border `rgba(19,35,91,0.25)`, rotates 45° when open, fills `--dark-navy`
- Panel: `max-height: 0 → auto` via JS, `transition: max-height 0.4s cubic-bezier(0.25,0,0,1)`
- Body text: `0.95rem; line-height: 1.45; color: var(--text-mid)`

### Sponsorship Tier Accordion (mobile only, `max-width: 860px`)
- `display: none` on desktop, `display: flex; flex-direction: column; gap: 0.6rem` on mobile
- Panel animation: `grid-template-rows: 0fr → 1fr` (single `<ul>` child with `overflow: hidden`)
- Header: tier name (Zodiak 1rem) + price (orange, Zodiak 0.95rem) + icon
- Card border: `rgba(27,33,80,0.45)` → `#fa3f20` when open/hover
- "Become a [Tier] Sponsor" link: last `<li>` inside the `<ul>`, orange, 0.65rem, `letter-spacing: 0.18em`

### Leadership Accordion (mobile only)
- Groups separated by `border-bottom: 1px solid rgba(19,35,91,0.1)`
- Desktop `border-top` overridden with `border-top: none !important` on mobile

---

## Reveal Animations

```css
.reveal { opacity: 0; transform: translateY(28px); transition: opacity 0.75s cubic-bezier(0.25,0,0,1), transform 0.75s; }
.reveal.visible { opacity: 1; transform: translateY(0); }
.reveal-delay-1 { transition-delay: 0.1s; }
.reveal-delay-2 { transition-delay: 0.2s; }
.reveal-delay-3 { transition-delay: 0.3s; }
.reveal-delay-4 { transition-delay: 0.4s; }
```
Triggered by IntersectionObserver — never animate `transition-all`.

---

## Photo Sliders

- `scroll-snap-type: x mandatory`, `scrollbar-width: none`
- Prev/next buttons: 32px circles, `rgba(13,18,37,0.5)`, hidden until hover on the container
- Dots: 6px circles, active dot is `#ccc4fc` (lavender) at scale 1.4
- Touch devices: buttons hidden via `@media (hover: none)`

---

## Qgiv Modal Integration

All support/donate/ticket buttons use class `qgiv-trigger`. A hidden button with id `qgiv-load-modal-91416` and class `qgiv-load-modal` acts as the actual Qgiv embed trigger. JS click handler:

```js
document.querySelectorAll('.qgiv-trigger').forEach(el =>
  el.addEventListener('click', e => {
    e.preventDefault();
    document.getElementById('qgiv-load-modal-91416').click();
  })
);
```

Qgiv embed script loads from `https://secure.qgiv.com/resources/core/js/embed.js`. **Do not use `var QGIV = ...`** — this overwrites the global Qgiv object. Use a different variable name.

---

## Brand Assets

Located in `./brand.assets/`:

| File | Use |
|---|---|
| `SaluteGalaLogoTransparent.svg` | Hero logo (white/transparent) |
| `LockupPatternViolet.svg` | Repeating background texture on dark sections |
| `YWCA LOGO NO TAGLINE.png` | Nav + footer logo |

---

## Key Anti-Patterns (never do these)

- No `transition-all` — always specify property (`transform`, `opacity`)
- No default Tailwind palette (indigo-500, blue-600, etc.)
- No `var QGIV = ...` in script — reserved by Qgiv embed.js
- No flat `shadow-md` — use layered color-tinted shadows
- Accordions: "Become a Sponsor" link must be a `<li>` inside the `<ul>` (the grid child), not a sibling element — or it won't collapse with the panel animation
