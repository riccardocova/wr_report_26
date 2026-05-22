# osservatorio_v-c_fix01 — Note modifiche

**File base:** `preview/osservatorio_v-c.html`  
**Data:** maggio 2026

---

## Modifiche apportate

### Sostituzione font system → Google Sans (brand WeRoad)

| Ruolo | Prima | Dopo |
|---|---|---|
| Display / Headline (`--f-display`) | Syne (default) | Google Sans |
| Body (`--f-body`) | Source Serif 4 | Google Sans |
| Mono (`--f-mono`) | JetBrains Mono | Google Sans Mono |

Font rimossi dall'import: Syne, Source Serif 4, Fraunces, Instrument Serif, JetBrains Mono.

**Import aggiornato:**
```html
<link href="https://fonts.googleapis.com/css2?family=Google+Sans:wght@400;500;700&family=Google+Sans+Mono:wght@400;500;700&display=swap" rel="stylesheet">
```

### Stile heading — peso aumentato (stile weroad.com)

Aggiunto blocco CSS override per titoli e numeri grandi:

```css
font-weight: 700;
font-variation-settings: "GRAD" 90, "opsz" 18;
```

Elementi interessati: `.hero__headline`, `.turn-headline`, `.sxsw-headline`, `.conc-headline`, `.stat-num`, `.turn-stat .n`, `.c-turn-stat .n`

### Tweaks panel — rimosso font-switcher headline

Il pannello tweaks aveva un segmento con 3 opzioni per il font headline (Syne / Fraunces / Instrument Serif). Con la sostituzione Google Sans queste opzioni non hanno più senso — rimosse:
- Blocco HTML `<div class="tw-seg" data-key="headlineFont">` con i 3 bottoni
- Chiave `headlineFont` dallo stato iniziale JSON (`TWEAK_DEFAULTS`)
- Riga JS `root.dataset.headline = state.headlineFont` nella funzione `apply()`
- Override CSS `html[data-headline="fraunces"]` e `html[data-headline="instrument"]`

Il resto del tweaks panel è invariato (grain, paper/dark mode, accent color, section numbers, sxsw variant).

---

## Invariato

- Struttura HTML e layout completo
- Colori, animazioni, logica JS
- Tutti i path risorse (relativi, nessun URL assoluto introdotto)
- Placeholder ritratti Unsplash
- Resto del tweaks panel (grain, dark mode, accent, section numbers)
