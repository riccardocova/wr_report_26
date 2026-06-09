# osservatorio_v-d_fix15 — Note

**File di partenza:** commit `fdd0646` ("fix12.3 swipe e scroll") — base pulita

**Approccio:** completamente diverso da tutte le versioni precedenti.

## Perché i fix precedenti non funzionavano

Tutti i tentativi precedenti cercavano di intercettare il touch verticale DOPO che iOS aveva già deciso di ignorarlo, lavorando a livello JS con `e.preventDefault()` + `window.scrollBy()`. Il problema è a monte: iOS Safari decide la direzione del gesture a livello di sistema prima che il JS entri in gioco, e la decisione dipende dal tipo di elemento toccato (testo vs immagine).

## Nuovo approccio: `touch-action: pan-y`

### CSS
```css
.c-stories-track {
    touch-action: pan-y
}
```

Questa dichiarazione dice al browser **a livello CSS, prima di qualsiasi JS**: "lo scroll verticale è sempre permesso da qualsiasi elemento in questo container". Il browser gestisce il V-scroll nativo indipendentemente dal tipo di elemento toccato — testo o immagine, non importa.

Con `pan-y`, il browser NON gestisce più lo scroll orizzontale (pan-x è escluso). Quindi lo scroll tra le card viene gestito completamente dal JS.

### JS — handler H-scroll manuale con snap

`touchstart` (passive):
- Registra posizione iniziale
- Calcola card corrente (`snapCard`)
- Disabilita `scroll-snap` durante il drag

`touchmove` (passive: **false** — necessario solo per `e.preventDefault()` sull'asse H):
- Se direzione = H: `e.preventDefault()` (previene che la componente V minore durante uno swipe H scrolli la pagina), poi imposta `track.scrollLeft` manualmente
- Se direzione = V: **non fa niente** — il browser gestisce via `touch-action: pan-y`

`touchend`:
- Se H-drag: calcola card target (soglia 20% larghezza card), chiama `scrollTo` con `offsetLeft` della card target, ripristina `scroll-snap`
- Altrimenti: ripristina `scroll-snap`

## Cosa è preservato
- Flip card: tap funziona, logica `has-flip` / `scrollSnapType = 'none'` del flip card handler non è toccata
- Pulsanti prev/next: continuano a funzionare via `scrollBy` nativo
- Progress bar: aggiornata via evento `scroll` (invariata)
- Scroll quote sul retro (overflow-y interno): non toccato

## Cosa testare
- [ ] Swipe verticale da TESTO → scrolla la pagina
- [ ] Swipe verticale da IMMAGINE → scrolla la pagina (non deve regredir)
- [ ] Swipe orizzontale da TESTO → scorre le card
- [ ] Swipe orizzontale da IMMAGINE → scorre le card
- [ ] Snap delle card al rilascio dello swipe
- [ ] Tap su card → flip funziona
- [ ] Pulsanti prev/next → funzionano
- [ ] Scroll della quote sul retro → funziona
- [ ] Progress bar → si aggiorna
