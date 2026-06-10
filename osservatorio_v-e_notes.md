# osservatorio_v-e — Notes

## Approach
v-e = v-c style system (tokens, fonts, layout primitives) + all content from v-d_fix16.

## Changes from v-c base

### Removed
- Tweaks panel (⚙ FAB, panel HTML, CSS, and JS)
- `TWEAK_DEFAULTS` script block at top of `<head>`
- "APPLY TWEAKS" JS module
- "TWEAKS PANEL" JS module
- Legacy pixel map JS block
- Old v-c slider JS (replaced with v-d flip card + slider JS)
- Old hero-bottom content ("7 capitoli · 12 minuti") → now "5.000 rispondenti · 5 paesi"

### Title & meta updated
- `<title>`: "Osservatorio 2026: come sono cambiate le relazioni sociali? | WeRoad"
- `<meta description>`: updated to match v-d
- Page-meta strip: "Come stanno cambiando le relazioni oggi? _v-e"

### CSS additions (inserted before closing `</style>`)
- Flip card system: `.c-story-inner`, `.c-story-front`, `.c-story-back`, `.c-story-photo`, `.c-story-photo-name`, `.c-story-text-area`, `.c-story-bio`, `.c-story-excerpt`, `.c-story-readmore`, `.c-story-close`, `.c-story-back-name`, `.c-story-back-bio`, `.c-story-quote-full`
- **fix16 iOS overlay**: `.c-story-text-area::after` (transparent z-index:1 div prevents iOS text-selection on swipe); `.c-story-inner.flipped .c-story-text-area::after { display: none }`
- `.brand-person-quote` + sub-elements (person avatar, quote text, attribution)
- `.report-callout` + sub-elements
- `.fn-ref`, `.fn-overlay`, `.fn-popup` (footnote system)
- `.conc-intro`, `.conc-sub-head`, `.conc-stats`, `.conc-close` (v-d conclusion extras)
- `.turn-line-1`, `.turn-line-2` animation (staggered entry for turn headline)
- `.geo__video` (ambient video for s-geo section)
- Dark-section overrides for `.brand-person-quote` and `.report-callout`
- `.c-turn-img` extended height override (parallax: calc(100vh + 520px))
- `.c-turn-stats` gradient override (v-d style: transparent → #1A1A1A)

### CSS modifications
- `.hero__headline` font-size: `clamp(44px, 8vw, 124px)` → `clamp(28px, 3.5vw, 56px)`
- `.h-section` font-size: `clamp(34px, 5.2vw, 72px)` → `clamp(28px, 4vw, 58px)`
- `.sxsw-quotes` grid: `1fr 1fr` → `repeat(3, 1fr)` (v-d has 3 quotes)
- `.c-turn-stat .l` color: `var(--ink-2)` → `var(--on-dark-mute)` (legible on dark bg)

### Section mapping (v-c → v-e)
| ID | v-c label | v-e label | Content source |
|----|-----------|-----------|----------------|
| cap-01 | Il punto di partenza | Il contesto | v-d |
| cap-02 | Geografia della solitudine | Un fenomeno trasversale | v-d (+ ambient video bg) |
| cap-03 | Dove si conoscono le persone | Nuovi modi per incontrarsi | v-d (+ Eventbrite callout) |
| cap-04 | La svolta | Relazioni in viaggio | v-d (alt2 image, 2 brand quotes, 2 charts) |
| cap-05 | Human Stories | SXSW (picture, 3 quotes) | v-d |
| cap-06 | SXSW | Storie dalla community | v-d flip cards (6 stories) |
| cap-07 | Conclusione | Conclusione | v-d (conc-stats list, conc-close) |

### JS additions (all from v-d_fix16)
- REVEAL+COUNT-UP+BAR FILLS: updated to handle multiple `.chart` elements (not just `#chart`)
- HERO ENTRY: same as v-c
- TURN HERO PARALLAX: new (translateY on `.c-turn-img`)
- FLIP CARDS: new (click to flip, close button, ESC, disable snap on flip)
- STORIES SLIDER CONTROLS: updated (uses `cStoriesProgressFill`, not old idx/progress refs)
- FOOTNOTE POPUPS: new (8 footnotes, modal popup with overlay)

### Media assets referenced (new in v-e vs v-c)
- `media/A-02_geography-ambient.webm/.mp4` — ambient video for cap-02
- `media/A-04_the-turn-hero-alt2.jpg` — turn hero image (replaces A-04_the-turn-hero.jpg)
- `media/A-04_the-turn-hero-mobile-alt2.jpg` — mobile version
- `media/A-06_sxsw-hero.jpg` / `A-06_sxsw-hero-mobile.jpg` — SXSW picture bg (replaces video)
- `media/quote-brand_kindred_justine-palefsky.jpg`
- `media/quote-brand_get-your-guide_jean-gabriel-duveau.jpg`
- `media/quote-brand_weroad_fabio-bin.jpg`
- `media/quote-testimonial_anna-harvey.jpg`
- `media/quote-testimonial_alicia-bailac.jpg`
- `media/quote-testimonial_manuel-ortega-sanchez.jpg`
- `media/quote-testimonial_simon-serp.jpg`
- `media/quote-testimonial_eileen-wegner.jpg`
- `media/quote-testimonial_daniela-d-attolico.jpg`
