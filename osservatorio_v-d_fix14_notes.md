# osservatorio_v-d_fix14 — Note

**File di partenza:** `osservatorio_v-d_fix13.html` (= commit `fdd0646`, "fix12.3 swipe e scroll")

**Diagnosi finale:**
Analizzando lo slider di weroad.it (section `TRIP_LIST_PROMO`) — che funziona correttamente — la differenza strutturale con il nostro slider è che le loro card non hanno `overflow: hidden` su elementi intermedi. La struttura è solo:
```
overflow-x:auto (scroll container)
  └── card (no overflow)
      └── contenuto (immagine + testo)
```

Nel nostro slider invece `.c-story-front` ha `overflow: hidden`, che iOS Safari tratta come uno scroll container intermedio. Questo cambia come iOS gestisce il touch gesture sul testo: invece di far risalire il V-scroll fino alla pagina (scroll chaining), lo "cattura" nel contesto di `.c-story-front` e non lo propaga correttamente.

**Modifica applicata — CSS only, una sola proprietà:**

Separato `.c-story-front` da `.c-story-back` nella regola CSS e aggiunto override:

```css
.c-story-front {
    overflow: visible;
    clip-path: inset(0)
}
```

- `overflow: visible` — rimuove `.c-story-front` dagli scroll container di iOS
- `clip-path: inset(0)` — clip visuale identica a `overflow: hidden` (taglia il contenuto ai bordi del box), ma **non crea un scroll container** nel modello di iOS Safari

`.c-story-back` mantiene `overflow: hidden` perché contiene `.c-story-quote-full` con `overflow-y: auto` (scroll della citazione completa).

**Nessun JS aggiunto.** Nessun `touch-action`. Nessun `user-select`. Solo questa modifica CSS strutturale.

**Cosa testare su device:**
- [ ] Swipe verticale dalla parte TESTO del front → deve scrollare la pagina
- [ ] Swipe orizzontale dalla parte TESTO del front → deve scorrere le card
- [ ] Swipe verticale dalla parte IMMAGINE → non deve regredir (deve scrollare pagina)
- [ ] Swipe orizzontale dalla parte IMMAGINE → non deve regredir (deve scorrere card)
- [ ] Scroll della quote completa sul retro → deve funzionare
- [ ] Tap su card → flip animazione funziona (verificare che clip-path non rompa la 3D rotation)
- [ ] Pulsanti prev/next → funzionano
- [ ] Progress bar → si aggiorna
