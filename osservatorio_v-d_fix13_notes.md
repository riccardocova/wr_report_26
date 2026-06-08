# osservatorio_v-d_fix13 — Note

**File di partenza:** `osservatorio_v-d_fix12.html` (commit `2336b07`, versione fix12.4 — pre-regressione)

**Problema:** swipe verticale sulla parte testuale delle card testimonial (sezione 06) non funzionava. Swipe dalla parte immagine funzionava. Swipe orizzontale funzionava da entrambe le aree.

**Causa identificata:**
iOS Safari committ alla direzione di scroll in due momenti distinti:
1. **Text-selection pre-emption**: quando il tocco inizia su un elemento `<p>` con testo, iOS entra in "modalità selezione testo" che interferisce con gli eventi touch prima ancora che il JS li intercetti. Questo non avviene sulle immagini (`div` con background-image).
2. **Early direction commitment**: i primissimi `touchmove` events arrivano al listener prima che il JS abbia determinato la direzione. In quel gap, il browser vede l'elemento con `overflow-x: auto` e committ silenziosamente a pan-x.

**Modifiche applicate:**

### 1. CSS — `user-select: none` su `.c-story-front` e `.c-story-back`
Aggiunto a entrambi i lati della flip card:
```css
user-select: none;
-webkit-user-select: none
```
Impedisce a iOS di entrare in "modalità selezione testo" quando il tocco inizia sui `<p>`. La gesture di touch viene trattata come un tocco su un elemento non-testo (come l'immagine).

### 2. JS — `e.preventDefault()` anche durante la fase "direzione indeterminata"
Prima: `e.preventDefault()` veniva chiamato solo quando `dir === 'v'` (direzione già determinata).

Dopo: `e.preventDefault()` viene chiamato anche quando `dir === null` (soglia non ancora raggiunta). Questo impedisce al browser di committare a pan-x durante i primi eventi touchmove, prima che il JS sappia se l'utente sta andando in verticale o orizzontale.

Quando la direzione si determina come `'h'`, il browser riprende il controllo dello scroll orizzontale nativamente (non viene chiamato preventDefault).

**Cosa testare su device:**
- [ ] Swipe orizzontale dall'area testo → deve scorrere le card
- [ ] Swipe verticale dall'area testo → deve scrollare la pagina
- [ ] Swipe orizzontale dall'area immagine → non deve regredir
- [ ] Swipe verticale dall'area immagine → non deve regredir
- [ ] Tap su card → deve aprire il retro (flip)
- [ ] Pulsanti prev/next → devono funzionare
- [ ] Progress bar → deve aggiornarsi
