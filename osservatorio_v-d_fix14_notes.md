# osservatorio_v-d_fix14 — Note

**File di partenza:** `osservatorio_v-d_fix13.html` (= commit `fdd0646`, "fix12.3 swipe e scroll")

**Stato fix13:** swipe V funziona dall'area immagine, non funziona dall'area testo del front della card.

**Problema delle versioni precedenti (fix12.4–fix12.5 e primo tentativo fix14):**
I fix basati su JS con `e.preventDefault()` anticipato (prima che la direzione fosse determinata) rompevano il V-scroll nativo dall'immagine e il V-scroll interno della quote sul retro. Il V-scroll dall'immagine funzionava SENZA JS — bloccarlo con `preventDefault` precoce ne causava la regressione.

**Diagnosi:**
- Immagine: `div` con background-image → iOS non entra in "text-selection mode" → scroll chaining nativo al window ✓
- Testo: `<p>` con contenuto testuale → iOS entra in "text-selection mode" su swipe → intercetta il gesture prima del scroll chaining → V non arriva al window ✗

**Modifica applicata — CSS only, nessun JS:**

```css
.c-story-text-area {
    user-select: none;
    -webkit-user-select: none
}
```

Impedisce a iOS di entrare in text-selection mode quando il tocco inizia sui `<p>` dell'area testo. Se questo è sufficiente, il browser eseguirà scroll chaining V→window esattamente come fa per l'immagine, senza bisogno di alcun handler JS.

**Nessun handler JS aggiunto** — la base fix12.3 non aveva JS per il touch, e questa modifica non ne aggiunge. Questo preserva:
- Il V-scroll nativo dall'immagine (invariato)
- Il V-scroll interno di `.c-story-quote-full` sul retro (invariato)

**Cosa testare su device:**
- [ ] Swipe verticale dalla parte TESTO del front → deve scrollare la pagina
- [ ] Swipe orizzontale dalla parte TESTO del front → deve scorrere le card
- [ ] Swipe verticale dalla parte IMMAGINE → non deve regredir
- [ ] Swipe orizzontale dalla parte IMMAGINE → non deve regredir
- [ ] Scroll della quote completa sul retro → deve funzionare (overflow-y interno)
- [ ] Tap su card → flip funziona
- [ ] Pulsanti prev/next → funzionano
