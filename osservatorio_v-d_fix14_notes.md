# osservatorio_v-d_fix14 — Note

**File di partenza:** `osservatorio_v-d_fix13.html` (= commit `fdd0646`, "fix12.3 swipe e scroll")

**Problema:** swipe verticale sulla parte testuale delle card (sezione 06) non scrolla la pagina. Swipe dalla parte immagine funziona correttamente in entrambe le direzioni.

**Causa:** iOS Safari tratta diversamente i tocchi su elementi `<p>` con testo rispetto ai `div` senza testo:
1. **Text-selection pre-emption**: il tocco su testo entra in "modalità selezione" iOS, che cattura i touchmove prima che il browser li passi al gestore JS.
2. **Pan-x pre-commitment**: nei primissimi `touchmove` (prima che il JS determini la direzione), il browser vede il container `overflow-x: auto` e committ silenziosamente a scroll orizzontale.

**Modifiche applicate:**

### 1. CSS — `user-select: none` su `.c-story-front` e `.c-story-back`
```css
user-select: none;
-webkit-user-select: none
```
Impedisce a iOS di entrare in text-selection mode. I tocchi sul testo vengono trattati come tocchi su elementi non-testo (come l'immagine).

### 2. JS — Blocco directional scroll (aggiunto, non era presente in fix12.3)
Aggiunge un listener `touchmove` sul track con `{ passive: false }`.

**Novità rispetto alle versioni precedenti:** `e.preventDefault()` viene chiamato anche quando la direzione è ancora `null` (non determinata), non solo quando `dir === 'v'`. Questo impedisce il pre-commit a pan-x durante i primissimi touchmove.

```
dir === 'v'  → preventDefault + window.scrollBy()
dir === null → preventDefault (blocca pre-commit)
dir === 'h'  → niente (browser gestisce scroll orizzontale nativo)
```

**Cosa NON è stato modificato:**
- Nessun `touch-action` CSS (era la causa della regressione in fix12.5)
- La logica dello slider (prev/next, progress bar, flip card) rimane invariata

**Cosa testare su device:**
- [ ] Swipe verticale dalla parte TESTO → deve scrollare la pagina
- [ ] Swipe orizzontale dalla parte TESTO → deve scorrere le card
- [ ] Swipe verticale dalla parte IMMAGINE → non deve regredir (deve scrollare pagina)
- [ ] Swipe orizzontale dalla parte IMMAGINE → non deve regredir (deve scorrere card)
- [ ] Tap su card → deve aprire il retro (flip)
- [ ] Pulsanti prev/next → devono funzionare
- [ ] Progress bar → deve aggiornarsi
