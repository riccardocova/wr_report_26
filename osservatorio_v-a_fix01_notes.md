# osservatorio_v-a_fix01 — Note modifiche

**File base:** `preview/osservatorio_v-a.html`  
**Data:** maggio 2026

---

## Modifiche apportate

### Sostituzione font system → Google Sans (brand WeRoad)

| Ruolo | Prima | Dopo |
|---|---|---|
| Display / Headline | Space Grotesk | Google Sans |
| Body / Testo | Inter | Google Sans |
| Mono / Eyebrow / Labels | JetBrains Mono | Google Sans Mono |

**Import aggiornato:**
```html
<link href="https://fonts.googleapis.com/css2?family=Google+Sans:wght@400;500;700&family=Google+Sans+Mono:wght@400;500;700&display=swap" rel="stylesheet" />
```

**CSS variables aggiornate:**
```css
--font-display: "Google Sans", "Helvetica Neue", Helvetica, Arial, sans-serif;
--font-body:    "Google Sans", "Helvetica Neue", Helvetica, Arial, sans-serif;
--font-mono:    "Google Sans Mono", ui-monospace, Menlo, Consolas, monospace;
```

### Adattamento font-weight

Google Sans non include il peso 300. Tutti gli usi di `font-weight: 300` portati a `font-weight: 400`.

### Stile heading — peso aumentato (stile weroad.com)

Aggiunto blocco CSS override per titoli e numeri grandi, allineato all'uso di Google Sans sul sito WeRoad:

```css
font-weight: 700;
font-variation-settings: "GRAD" 90, "opsz" 18;
```

Elementi interessati: `.display`, `.concl-title`, `.stat-num`, `.reason__num`, `.geo-big`, `.geo-who__num`, `.turn-stat__num`, `.apps-foot__num`, `.reasons__title`, `.sxsw-quote__text`

Eccezione: `.stat-num.outlined` usa `font-weight: 500` e `"GRAD" 40` per mantenere leggibilità con `-webkit-text-stroke`.

---

## Invariato

- Struttura HTML, layout, colori, animazioni
- Tutti i path risorse (relativi, nessun URL assoluto introdotto)
- Placeholder media e ritratti Unsplash
- Tweaks panel
