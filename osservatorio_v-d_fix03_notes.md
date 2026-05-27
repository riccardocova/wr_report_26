# osservatorio_v-d_fix03.html — Note di generazione

**File di partenza:** `preview/osservatorio_v-d_fix02.html`
**Data:** 2026-05-26

---

## Modifiche apportate

### Sezione 04 — Relazioni in viaggio: enfasi "punto di svolta"

#### Continuità visiva cover → stats
- **Gradiente hero aggiornato**: `.c-turn-img::before` passa da `rgba(26,26,26,.82) 100%` a `rgba(26,26,26,1) 100%` con curva più morbida a 4 stop (0% → 50% → 80% → 100%). La cover ora sfuma completamente nel colore paper, eliminando la frattura visiva con la sezione dati.
- **Linea rossa rimossa**: eliminato `border-top: 3px solid var(--accent)` da `.c-turn-stats`. Cover e griglia dati ora si percepiscono come un'unica unità visiva continua.

#### Effetto parallax sull'immagine hero
- `.c-turn-img` ridimensionato a `height: 115%` (era `100%`) per permettere il movimento senza esporre i bordi dell'immagine.
- Aggiunto JS IIFE `TURN HERO PARALLAX`: al scroll, l'immagine trasla verticalmente da `0` a `-9%` mentre la sezione attraversa il viewport. Effetto di profondità che enfatizza il momento di ingresso nella sezione.
- Rispetta `prefers-reduced-motion`.

#### Animazione headline più teatrale
- `.turn-headline.reveal` overridato con transizione più lenta (`1.6s` vs `0.9s`), easing `cubic-bezier(.16,1,.3,1)` (spring-like), e partenza con `scale(.94)` invece del solo `translateY`. L'ingresso del titolo "In viaggio succede *qualcosa*..." è più impattante rispetto agli altri capitoli.
