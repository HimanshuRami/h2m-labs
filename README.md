# Handoff: H2M Labs — Company Landing Page

## Overview
A single-page marketing/landing site for **H2M Labs** (h2mlabs.in) — a bootstrapped,
one-person SaaS product studio based in India. The site exists to (1) present the
studio and its products and (2) serve as a **payment-trust anchor**: when a customer
sees "H2M Labs" on a card statement (from a product like WatchMySubs), they can visit
h2mlabs.in and immediately confirm it's a legitimate, registered operator.

It is a single scrollable page: sticky navbar → hero → about → products → payment
trust → founder → contact → footer.

## About the Design Files
The file in this bundle (`index.html`) is a **design reference created in HTML** — a
working prototype that shows the intended look, copy, and behavior. It is *not*
required to be shipped verbatim.

That said, this design was authored as a deliberately dependency-light static site
(semantic HTML + Tailwind + vanilla JS), so **shipping it largely as-is is a valid and
encouraged path**. The task is to take it to **production-grade static output**: replace
the Tailwind CDN with a real local Tailwind build, self-host fonts, add favicon/OG/SEO
assets, run an a11y pass, and deploy. Do **not** introduce React, a build framework, or
a CMS — keep it vanilla HTML/CSS/JS. If you do recreate it in another environment,
preserve the design and copy exactly.

## Fidelity
**High-fidelity (hifi).** Final colors, typography, spacing, copy, and interactions are
all decided. Recreate pixel-for-pixel. All exact values are listed under **Design
Tokens** below.

---

## Production Task Checklist
1. **Repo setup** — git init, sensible `.gitignore`, `README.md` (what it is, run
   locally, deploy steps).
2. **Keep it static & fast** — no React/framework/CMS. Replace the Tailwind **CDN**
   with a local **Tailwind CLI** build that purges unused classes and outputs one
   minified stylesheet. Visual result must be identical. **Self-host the Inter font**
   (woff2) instead of Google Fonts.
3. **Production polish** — favicon set (svg + ico + apple-touch-icon) + `site.webmanifest`;
   a `1200×630` `og-image.png` matching the dark/blue brand wired into OG + Twitter card
   meta; `robots.txt` + `sitemap.xml` for h2mlabs.in; accessibility pass (contrast, alt
   text, focus states, aria labels on the hamburger + links).
4. **Fill placeholders** — ask the owner for values; do **not** invent them:
   - `[Founder Name]` (founder section)
   - Founder avatar initials (currently `FN`)
   - LinkedIn URL (currently `#`)
   - X/Twitter URL (currently `#`)
   - Privacy Policy + Terms of Service pages (currently `#`)
5. **Deploy** — configure for Netlify or Vercel; commit the config; document steps.

---

## Screens / Views

There is one view (the scrolling page). Sections below, in DOM order.

### 1. Navbar (`<nav id="nav">`)
- **Purpose:** Persistent navigation + primary CTA.
- **Layout:** Fixed top, full width, z-50. Inner row: `max-width: 1120px`, horizontal
  padding `20px` (mobile) / `24px` (sm+), height `64px`, `flex` space-between, vertically
  centered.
- **Components:**
  - **Logo (left):** 32×32 rounded-lg (`8px`) tile, `border` hairline, `bg #151821`,
    containing a small "H" lab mark SVG (two vertical strokes + crossbar, stroke `#4F7EFF`,
    width 2.2). Beside it the wordmark "H2M Labs", 15px, weight 600, white, `tracking-tight`.
  - **Center links (desktop ≥768px):** "Products", "About", "Contact" — 14px,
    `color rgba(255,255,255,0.65)`, hover → white, `transition: color`. Gap `32px`.
  - **CTA (right, desktop):** "Our Products →" — accent gradient button (see token
    `.btn-accent`), rounded-lg, padding `16px/8px`, 14px weight 500, white.
  - **Hamburger (mobile <768px):** 36×36 rounded-lg bordered tile; toggles between a
    3-line "open" icon and an "X" close icon.
- **Behavior:** On `window.scrollY > 12`, add `.scrolled` → frosted background
  `rgba(13,15,20,0.72)`, `backdrop-filter: blur(14px) saturate(140%)`, hairline bottom
  border. Transition `0.35s`.

### 2. Hero
- **Purpose:** One-line value prop + two CTAs.
- **Layout:** Centered column, `max-width: 768px (max-w-3xl)`, top padding `144px`
  (mobile) / `176px` (sm), bottom `80–112px`. Text centered. Wrapper has class
  `.hero-wrap` (position relative) and a child `.spotlight` overlay.
- **Components (top→bottom):**
  - **Pill badge:** rounded-full, hairline border, `bg rgba(21,24,33,0.7)`, padding
    `14px/6px`, 12px weight 500, `rgba(255,255,255,0.7)`. Contains a pulsing accent dot
    (`.pulse-dot`, 6px, `bg #4F7EFF`) + text "One person · Building in the open from India".
  - **H1 (`.hero-h1`):** 40px (mobile) / 60px (sm) `text-6xl`, weight 800,
    `tracking-tight`, white, `text-balance`, line-height 1.07. Copy:
    **"Software you'll actually want to keep paying for."** Each word is wrapped in a
    `<span class="word">` with staggered `transition-delay` for a word-by-word reveal.
  - **Sub-headline `<p>`:** 16px (mobile) / 18px (sm), line-height relaxed,
    `rgba(255,255,255,0.6)`, `max-width: 36rem`, centered, `text-pretty`. Copy:
    "H2M Labs is a tiny, independent studio in India. One developer, a small shelf of
    products, and a stubborn belief that good software doesn't take a hundred people to build."
  - **CTA row:** stacks vertically on mobile, row on sm+, gap `12px`.
    - Primary: "See what we've built →" — `.btn-accent`, rounded-lg, padding `20px/12px`,
      14px weight 600. Links to `#products`.
    - Secondary: "The story behind it" — bordered, `bg rgba(21,24,33,0.6)`, hover
      `bg #1B1F2A` + brighter border. Links to `#about`.
- **Behavior:** `.spotlight` is a radial gradient that follows the cursor (CSS vars
  `--mx`/`--my` set via JS `pointermove`), fading in on hover of `.hero-wrap`.

### 3. About (`<section id="about">`)
- **Purpose:** Studio story + value stats.
- **Layout:** `max-width 1120px`, vertical padding `80–112px`, `scroll-mt-20` (offset
  for sticky nav). Two columns on `lg` (`grid lg:grid-cols-2`, gap 48–64px), stacked
  below. **Left** = text, **right** = stat cards.
- **Left column:**
  - Eyebrow "About" — 12px weight 600, uppercase, `letter-spacing 0.18em`,
    `color rgba(79,126,255,0.9)`.
  - H2 "So what is H2M Labs?" — 30px (mobile) / 36px (sm), weight 700, white, tracking-tight.
  - Three `<p>` body paragraphs, `rgba(255,255,255,0.6)`, `space-y 20px`, `text-pretty`.
    Copy (verbatim):
    1. "Honestly? It's one developer who got tired of software that tries to do everything, and started building the simpler version instead."
    2. "Every product begins the same way — a problem I kept bumping into, no tool I actually liked, so I made one. No committees, no features nobody asked for. Just small tools that do one job well."
    3. "Everything ships under a single name — **H2M Labs** — so when you spot it on a statement, you know exactly who built the thing and where to find them." (the name is white/weight-500 emphasis).
- **Right column:** 2×2 grid (`sm:grid-cols-2`, gap 16px) of stat cards. Each card:
  `.card .glow-card`, rounded-xl (`12px`), hairline border, `bg #151821`, padding `20px`,
  `overflow-hidden`. Big number 24px weight 700 white; label below 14px
  `rgba(255,255,255,0.5)`.
  1. "1+ live products" / "Out in the world, getting used"
  2. "One studio, many tools" / "All under H2M Labs"
  3. "Made in India" / "Used pretty much everywhere"
  4. "Bootstrapped" / "No investors, no pressure"

### 4. Products (`<section id="products">`)
- **Purpose:** The product shelf.
- **Layout:** `max-width 1120px`, vertical padding `80–112px`, `scroll-mt-20`. Heading
  block (`max-width 42rem`) then a 2-col grid on `md` (gap 20px), 1-col on mobile.
- **Heading block:** eyebrow "Products"; H2 "What we've shipped"; sub-paragraph "Each one
  stands on its own, does one thing well, and is built and backed by H2M Labs."
- **Card 1 — WatchMySubs (Live):** `<article>` `.card .glow-card .live-card`, rounded-2xl
  (`16px`), hairline border, `bg #151821`, padding `28px`, flex column.
  - Top row: **Live badge** — rounded-full, emerald border/bg
    (`border rgba(52,211,153,0.25)`, `bg rgba(52,211,153,0.1)`, text `#6ee7b7`), with a
    pulsing emerald dot (`.pulse-dot`). Right: "watchmysubs.com" 12px `rgba(255,255,255,0.4)`.
  - Title "WatchMySubs" 20px weight 600 white. Category "Subscription Management" 14px
    `rgba(79,126,255,0.9)`.
  - Description (verbatim): "Subscriptions are sneaky. WatchMySubs keeps every one in a
    single place, tells you what's about to renew, and nudges you before you get charged
    for that thing you forgot you signed up for." — 14px `rgba(255,255,255,0.6)`, flex-1.
  - CTA link "Take a look →" → `https://watchmysubs.com` (target=_blank, rel=noopener).
    Arrow nudges right on group-hover.
  - **Animated gradient border** via `.live-card::before` (see token below).
- **Card 2 — Coming Soon:** `.card .glow-card`, **dashed** hairline border,
  `bg rgba(21,24,33,0.6)`, padding `28px`. Amber badge (`border rgba(251,191,36,0.25)`,
  `bg rgba(251,191,36,0.1)`, text `#fcd34d`) "Coming Soon". Title "Something new"
  `rgba(255,255,255,0.85)`; category "In the workshop". Description: "There's another one
  taking shape right now — solving a problem I happen to be annoyed by, which is usually
  how these start. It'll be worth the wait." Footer text "Almost there"
  `rgba(255,255,255,0.3)`. **No CTA link.**

### 5. Payment Trust
- **Purpose:** Reassure about the billing descriptor. Visually distinct lighter panel.
- **Layout:** `max-width 1120px`, vertical padding `80–112px`. Inside: a single rounded-3xl
  (`24px`) panel, hairline border, `bg rgba(27,31,42,0.7)` (`surface-2`), padding `32px`
  (sm `48px`), `position relative; overflow hidden`. A decorative blurred accent blob sits
  top-right (`bg rgba(79,126,255,0.1)`, `blur-3xl`).
- **Components:**
  - Shield-check icon tile (44×44 rounded-xl bordered, `bg #151821`, accent stroke).
  - H2 "Wait — why does my statement say "H2M Labs"?" 24px (mobile) / 30px (sm) weight 700.
  - Two body paragraphs (verbatim):
    1. "Good question, and nothing's wrong. If you're paying for one of our products — like WatchMySubs — **"H2M Labs"** is the name that shows up on your bank statement or invoice."
    2. "That's just us. H2M Labs is the registered business behind every product here, and we run all payments through a single account so your billing stays simple and predictable."
  - **3 trust bullets** (`sm:grid-cols-3`, gap 16px), each a `.glow-card` rounded-xl
    bordered tile, `bg rgba(21,24,33,0.7)`, padding `20px`. Emoji + small text:
    - 🔒 "Payments run through established, secure gateways — we never see your card details."
    - 🏢 "H2M Labs is the legal entity operating every product on this site."
    - 📧 "Still not sure? Email hello@h2mlabs.in and a real person replies." (email is an
      accent `mailto:` link).

### 6. Founder
- **Purpose:** Personal, warm bio.
- **Layout:** Centered, `max-width 42rem`, vertical padding `80–112px`. Eyebrow "Founder";
  H2 "The person behind all this". Below: a single rounded-2xl card, hairline border,
  `bg #151821`, padding `32px` (sm `40px`), centered column.
- **Components:**
  - **Avatar:** 80×80 rounded-full, gradient `from rgba(79,126,255,0.3) to rgba(99,102,241,0.2)`,
    hairline border, centered initials "FN" (24px weight 700, `rgba(255,255,255,0.8)`).
    → Replace with real founder photo or initials.
  - Name "[Founder Name]" 18px weight 600 white. → **placeholder, fill in.**
  - Role "Founder, H2M Labs" 14px `rgba(79,126,255,0.9)`.
  - Bio (verbatim): "Hey — I'm the one building everything here. I'm a developer in India
    who got fed up with apps that try to do too much, so I started making the lean versions
    instead. I use every product I ship, every single day. When something annoys me, it
    gets fixed fast — because I'm the one being annoyed."
  - Link "Say hi on LinkedIn →" → `#` (**fill in LinkedIn URL**).

### 7. Contact (`<section id="contact">`)
- **Purpose:** One clear way to reach out (no form).
- **Layout:** Centered, `max-width 42rem`, vertical padding `80–112px`, `scroll-mt-20`.
- **Components:** Eyebrow "Contact"; H2 "Come say hello"; paragraph "Got a question about
  a product? A partnership idea? Spotted a bug, or just feel like chatting? Whatever it is,
  it lands in my inbox — and I read every one." Then a large pill `.btn-accent` button
  (rounded-full, padding `28px/14px`) with a mail icon + "hello@h2mlabs.in" → `mailto:`.
  Below it a muted text link "Or catch me on X / Twitter →" → `#` (**fill in**).

### 8. Footer (`<footer>`)
- **Purpose:** Sitemap + legal + colophon.
- **Layout:** `border-top` hairline. Inner `max-width 1120px`, padding `56px` vertical.
  Top grid: on `md`, columns `1.4fr 1fr 1fr 1fr`; stacked on mobile (gap 40px).
  - **Col 1:** logo tile + wordmark, then tagline "Building Software That Works For You."
    (14px `rgba(255,255,255,0.45)`, max-width ~20rem).
  - **Col 2 "Products":** WatchMySubs → `https://watchmysubs.com`.
  - **Col 3 "Company":** About (`#about`), Contact (`#contact`).
  - **Col 4 "Legal":** Privacy Policy (`#`), Terms of Service (`#`) — **build these pages.**
  - Column headers: 12px weight 600 uppercase `letter-spacing 0.16em` `rgba(255,255,255,0.4)`.
    Links: 14px `rgba(255,255,255,0.6)` → white on hover.
- **Bottom bar:** top hairline border, flex space-between (stacked on mobile), 12px
  `rgba(255,255,255,0.4)`: "© 2025 H2M Labs. All rights reserved." | (sm+ only)
  "Building software that works for you." | "Built in India 🇮🇳".

---

## Interactions & Behavior
- **Sticky frosted navbar:** JS toggles `.scrolled` on `<nav>` at `scrollY > 12`. Frost =
  `backdrop-filter: blur(14px) saturate(140%)` + translucent bg + hairline border. 0.35s.
- **Mobile menu:** Hamburger toggles `#mobileMenu` (`.hidden-menu` → opacity 0 +
  `scaleY(.96) translateY(-6px)` + `pointer-events:none`). Swaps open/close icons, sets
  `aria-expanded` + `aria-label`. Each menu link closes the menu on click. 0.25s transition.
- **Smooth scroll:** `html { scroll-behavior: smooth }`; all nav targets are `#id` anchors;
  scroll targets use `scroll-mt-20` so the sticky nav doesn't overlap headings.
- **Word-by-word headline:** `.hero-h1 .word` start at `opacity 0; translateY(16px)`;
  `.hero-h1.in .word` animates to visible. Per-word `transition-delay` (0.04s → 0.34s)
  staggers them. `.in` is added by the reveal observer.
- **Scroll reveal:** Elements with `.reveal` start hidden (`opacity 0; translateY(18px)`)
  and get `.in` via IntersectionObserver (threshold 0.12, rootMargin bottom -8%). **Safety
  fallbacks:** on load, anything already in viewport is revealed immediately, and a
  `setTimeout(revealAll, 1200)` guarantees nothing stays hidden; if `IntersectionObserver`
  is unavailable, everything reveals at once. Preserve these fallbacks.
- **Hero cursor spotlight:** `pointermove` on `.hero-wrap` sets `--mx`/`--my`; `.spotlight`
  radial gradient (420px) follows and fades in on hover.
- **Card pointer glow:** `pointermove` on each `.glow-card` sets `--cx`/`--cy`; a
  `::after` radial gradient (240px, accent) follows the cursor and fades in on hover.
- **Animated gradient border** (`.live-card`): a `::before` conic-gradient masked to a
  1px ring, rotated via the registered `@property --ba` angle, `spinBorder 6s linear infinite`.
- **Pulse dots** (`.pulse-dot`): an inherited-color `::after` ring scales `1 → 3.2` and
  fades, `pulseRing 2.4s ease-out infinite`.
- **Background:** fixed grid layer (`.bg-field`) slowly drifts (`drift 26s linear`), a dot
  matrix (`.bg-dots`), and a breathing accent glow (`.bg-glow`, `breathe 9s`). All are
  `position:fixed; z-index:0; pointer-events:none` with radial masks.
- **Reduced motion:** `@media (prefers-reduced-motion: reduce)` disables all the above
  animations, reveals everything, and sets `scroll-behavior: auto`. Preserve this.

## State Management
No app state. Two transient UI booleans only:
- Navbar `scrolled` (derived from scroll position).
- Mobile menu `open` (toggled by hamburger; reset on link click).

No data fetching. Static content only.

## Design Tokens

**Colors**
| Token | Value | Use |
|---|---|---|
| `ink` | `#0D0F14` | Page background |
| `surface` | `#151821` | Cards, tiles, nav logo |
| `surface-2` | `#1B1F2A` | Payment-trust panel, secondary btn hover |
| `hair` | `rgba(255,255,255,0.08)` | All hairline borders / dividers |
| `accent` | `#4F7EFF` | Primary accent (buttons, links, glow, mark) |
| `accent-2` | `#6366F1` | Secondary accent (gradients) |
| Text primary | `#FFFFFF` | Headings |
| Text body | `rgba(255,255,255,0.6)` | Paragraphs |
| Text muted | `rgba(255,255,255,0.4–0.5)` | Labels, footer |
| Emerald (Live) | border `rgba(52,211,153,0.25)`, bg `rgba(52,211,153,0.1)`, text `#6ee7b7`, dot `#34d399` |
| Amber (Soon) | border `rgba(251,191,36,0.25)`, bg `rgba(251,191,36,0.1)`, text `#fcd34d`, dot `#fbbf24` |

**Typography** — Inter (400/500/600/700/800), `-webkit-font-smoothing: antialiased`,
`font-feature-settings: "cv02","cv03","cv04","cv11"`.
| Role | Size (mobile → sm+) | Weight |
|---|---|---|
| H1 hero | 40px → 60px | 800 |
| H2 section | 30px → 36px (trust 24→30) | 700 |
| H3 card title | 20px | 600 |
| Body | 16px → 18px (hero), 14px (cards/footer) | 400 |
| Eyebrow | 12px, uppercase, `letter-spacing 0.18em` | 600 |

**Spacing** — Tailwind default scale. Section vertical rhythm `80px` (mobile) → `112px`
(sm). Content max-width `1120px`. Page horizontal padding `20px` → `24px`.

**Radius** — lg `8px` (buttons, small tiles), xl `12px` (stat/bullet cards),
2xl `16px` (product cards), 3xl `24px` (trust panel), full (pills, avatar, dots).

**Shadows / effects**
- `.btn-accent`: `linear-gradient(180deg,#5C88FF,#4F7EFF)` +
  `inset 0 1px 0 rgba(255,255,255,0.22)` + `0 8px 24px -8px rgba(79,126,255,0.65)`;
  hover `brightness(1.07)` + `translateY(-1px)`.
- `.card` hover: `translateY(-4px)`, border → `rgba(79,126,255,0.45)`,
  `box-shadow: 0 24px 50px -24px rgba(79,126,255,0.45), 0 0 0 1px rgba(79,126,255,0.1)`.
- Frosted nav: `backdrop-filter: blur(14px) saturate(140%)`.

**Animation timings** — reveal 0.7s; word stagger 0.04–0.34s; nav 0.35s; menu 0.25s;
spinBorder 6s; pulseRing 2.4s; breathe 9s; drift 26s.

## Assets
- **Logo / favicon mark:** inline SVG "H" (two vertical strokes + crossbar, `#4F7EFF`).
  Currently used both as the nav/footer logo and as a data-URI favicon. → Generate a
  proper favicon set + OG image from this mark.
- **Founder avatar:** placeholder gradient circle with "FN" initials. → Replace with real
  photo/initials.
- **Icons:** small inline SVGs (hamburger, shield-check, mail, envelope). No icon library.
- **Emoji:** 🔒 🏢 📧 🇮🇳 used inline in trust bullets + footer.
- **No stock photography** — by design. Keep it geometric/abstract.
- **Font:** Inter, currently via Google Fonts CDN → self-host.

## Files
- `index.html` — the complete single-file design (HTML + Tailwind CDN config + inline
  `<style>` for custom animations + inline `<script>` for nav/menu/reveal/pointer effects).
  Everything described above lives in this one file.
