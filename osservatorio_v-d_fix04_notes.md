# osservatorio_v-d_fix04.html — Note di generazione

**File di partenza:** `preview/osservatorio_v-d_fix03.html`
**Data:** 2026-05-26

---

## Modifiche apportate

### Sezione 04 — continuità visiva cover → stats

#### Immagine hero estesa nella sezione dati
- `.c-turn-img` spostato fuori da `.c-turn-hero`: ora è figlio diretto di `.s-turn` (la section), posizionato `position: absolute; top: 0`.
- `height` portata a `calc(100vh + 220px)`: l'immagine si estende fisicamente 220px dentro la zona `.c-turn-stats`, così i primi numeri appaiono visivamente sovrapposti all'immagine.
- `.c-turn-hero` rimosso `overflow: hidden` (non più necessario), aggiunto `z-index: 1` per stare sopra all'immagine nel contesto `.s-turn`.

#### Gradiente hero aggiornato
- `.c-turn-img::before` non arriva più a `rgba(26,26,26,1)` — si ferma a `.88`. La dissolvenza finale è gestita da `.c-turn-stats`.

#### Gradiente continuità su `.c-turn-stats`
- `background: linear-gradient(180deg, rgba(26,26,26,0) 0px, rgba(26,26,26,1) 220px)`: i primi 220px della sezione dati sono trasparenti, rivelando l'immagine sottostante. Da 220px in poi è paper solido.

### Titolo sezione — colori
- `<em>In viaggio</em>` → rosso (`var(--accent)` via `.turn-headline em`)
- `succede qualcosa...` → bianco (testo default, rimosso il precedente `<em>` su "qualcosa")

### Animazione titolo staggered (due righe)
- Titolo diviso in due `<span class="turn-line-1">` e `<span class="turn-line-2">` con `display: block`.
- Il parent `.turn-headline.reveal` annulla il comportamento del sistema reveal generico (`opacity:1; transform:none; transition:none`) — le righe gestiscono autonomamente la propria animazione.
- `.turn-line-1` ("In viaggio"): entra con `translateY(22px) → 0`, delay 200ms, durata 0.9s.
- `.turn-line-2` ("succede qualcosa..."): delay 700ms, durata 1.2s — 500ms di stacco visibile dalla prima riga.
- Entrambe si attivano quando il JS aggiunge `.in` al parent `.turn-headline.reveal`.
