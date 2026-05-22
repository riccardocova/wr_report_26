# osservatorio_v-c_fix02 — Note modifiche

**File base:** `preview/osservatorio_v-c_fix01.html`  
**Data:** maggio 2026

---

## Modifiche apportate

### 1. Dark mode ovunque

Tutte le sezioni con sfondo chiaro sono state convertite a sfondo scuro `#1A1A1A` (stessa palette della sezione 07 Conclusione). Tecnica: blocco CSS override aggiunto alla fine del `<style>`, senza toccare le variabili globali (così le sezioni già scure — hero, s-turn, s-conclusion — rimangono invariate).

**Sezioni convertite da chiaro a scuro:**

| Sezione | Era | Ora |
|---|---|---|
| 01 · Data Escalation (`s-data`) | `#F5F2ED` | `#1A1A1A` |
| 02 · Geography (`s-geo`) | `#ECE7DE` | `#1A1A1A` |
| 03 · Apps vs Travel (`s-apps`) | `#F5F2ED` | `#1A1A1A` |
| 05 · Stories (`s-stories`) | `#F5F2ED` | `#1A1A1A` |
| 06 · SXSW / Focus Group (`s-sxsw`) | `#ECE7DE` | `#1A1A1A` |

**Sezioni invariate (già scure):** hero, 04 La svolta (`s-turn`), 07 Conclusione (`s-conclusion`).

**Colori testo aggiornati nelle sezioni convertite:**
- Testo primario → `var(--on-dark)` = `#F5F2ED` (bianco caldo)
- Testo secondario / muted → `var(--on-dark-mute)` = `#8c8a86` (grigio)
- Accent → `#FF4758` (invariato)
- Bordi/filetti → `var(--rule-dark)` = `rgba(245,242,237,.18)`
- Card/box interni (geo-map, who-stats, reason) → `#1e1e1e` / `#222222`
- Barre chart → `rgba(245,242,237,.10)` al posto di paper-3

### 2. Fix video SXSW (sezione 06)

Il video background sfuma tramite CSS mask-image. Cambiando il background di `.s-sxsw` da `var(--paper-2)` a `var(--ink)`, il video sfuma automaticamente verso il grigio scuro — nessuna modifica alla mask stessa necessaria.

### 3. Testi mono più grandi e leggibili

Aumentate dimensioni e ridotta opacity su tutti i testi monospace secondari:

| Elemento | Prima | Dopo |
|---|---|---|
| `.chapter` (es: "06 FOCUS GROUP") | 12px, opacity 0.6 | 14px, opacity 0.85 |
| `.eyebrow` | 12px | 14px |
| `.hero__issue` | 12px | 13px |
| `.sxsw-meta` | 12px | 14px |
| `.sxsw-quote .attr` (partecipanti) | 11px | 13px |
| `.pullquote .attr` | 12px | 13px |
| `.story__num` | 11px | 13px |
| `.bar-delta`, `.chart-source` | 11px | 12px |
| `.geo-map .map-meta`, `.geo-insight` | 10–11px | 12px |
| `.who-stats .who-lbl` | 12px | 13px |
| `.turn-stat .l small` | 11px | 12px |
| `.h-section` | 11px | 13px |

---

## Invariato

- Struttura HTML e layout completo
- Sezioni già scure: hero, s-turn, s-conclusion
- Font Google Sans / Google Sans Mono (da fix01)
- Heading override (GRAD 90, opsz 18, weight 700) (da fix01)
- Tutti i path risorse (relativi, nessun URL assoluto)
- Placeholder ritratti Unsplash
- Tweaks panel (grain, dark mode toggle, accent color, section numbers, sxsw variant)
