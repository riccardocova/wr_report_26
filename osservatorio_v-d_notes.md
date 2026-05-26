# osservatorio_v-d.html — Note di generazione

**File di partenza:** `preview/osservatorio_v-c_fix04.html`
**Data:** 2026-05-26
**Testo di riferimento:** `input - copy and prompts/copy-and-prompt/2026-05-25_testo-landing-approvato+istruzioni-redesign.md`

---

## Modifiche apportate

### Struttura e ordine sezioni
- Rinominazione cap-05 → **SXSW** (era Stories in v-c), cap-06 → **Storie dalla community** (era SXSW in v-c)
- Le label capitolo aggiornate ai valori approvati: "Il contesto", "Un fenomeno trasversale", "Nuovi modi per incontrarsi", "Relazioni in viaggio", "Ricerca qualitativa — SXSW", "Ricerca qualitativa — Community", "Conclusione"

### Hero (Sezione 0)
- Titolo aggiornato: "Nel 2026 conoscere persone nuove è diventato più difficile. Ma la voglia di incontrarsi non è sparita."
- Sottotitolo aggiornato con il testo definitivo sull'Osservatorio
- Label kicker aggiornata: "Come stanno cambiando le relazioni oggi?"

### Sezione 1 — Il contesto
- Secondo stat corretto: **52%** (era 47% in v-c) non è soddisfatto delle relazioni sociali
- Paragrafo OECD¹ e World Happiness Report³ spostato sotto al grid delle ragioni
- Aggiunto dato 41% e 20% sul numero di relazioni profonde dal passato
- Rimosso pullquote fittizio (Marco, 34 — Milano)

### Sezione 2 — Un fenomeno trasversale
- **Mappa paesi sostituita** con dati per dimensione urbana (23%/16%/19%/20%/21%) — il messaggio visivo è che le percentuali sono simili ovunque
- Testo OMS² aggiornato con riferimento al report 2025
- Aggiunto paragrafo sui "third places" con riferimento footnote Scott Galloway⁷
- Aggiunto blocco `support-stats` con **63%** e **58%** (nuovi dati approvati)
- Aggiunto testo ponte sui nuovi spazi di incontro
- **Nuova componente `brand-person-quote`**: Justine Palefsky, CEO Kindred, con foto `quote-brand_kindred_justine-palefsky.jpg`
- Rimosso pullquote fittizio (Lea, 29 — Berlino)

### Sezione 3 — Nuovi modi per incontrarsi
- Bar chart espanso da 4 a **6 voci**: aggiunti "Sport e passioni 29%" e "Eventi 28%"
- Aggiornate le due stat di supporto: **84%** e **72%** (+0,32 vs 2025)
- **Nuovo componente `report-callout`**: dati Eventbrite⁶ "Fourth Spaces" (95% e 84%)
- Rimosso pullquote fittizio (Sofia, 27 — Madrid)

### Sezione 4 — Relazioni in viaggio
- Quarta stat aggiornata: **84%** vede il viaggio come risposta al senso di isolamento (era 39% Skyscanner in v-c)
- **Nuovo `report-callout`**: dati Skyscanner⁴ (39% e 55% Gen Z)
- **Nuovo bar chart** "Perché accade in viaggio" (id=`chart-travel`): 60%, 43%, 30%, 19%, 16%
- **Nuovo `report-callout`**: dati GetYourGuide⁵ (+59% workshop)
- **Nuovo `brand-person-quote`**: Jean-Gabriel Duveau, VP GetYourGuide, con foto `quote-brand_get-your-guide_jean-gabriel-duveau.jpg`
- Aggiunto testo sulle relazioni durature post-viaggio
- **Nuovo pullquote**: Fabio Bin, Co-founder & CMO WeRoad, con riferimento footnote Fortune⁸
- Rimosso pullquote fittizio (Alicia, 31 — Barcellona)

### Sezione 5 — SXSW (ex cap-06)
- Titolo aggiornato: "Che ne pensa un gruppo di americani?"
- Intro aggiornata con il testo definitivo (focus group 15 persone 20-30 anni)
- **3 quote italiane** (approvate) in griglia a 3 colonne (era 4 quote in inglese a 2 colonne)
- Attributions: "SXSW Focus Group · Austin, TX"

### Sezione 6 — Storie dalla community (ex cap-05 Stories)
- **Implementazione flip card** completamente nuova:
  - Fronte: foto circolare (88px, border-radius 50%), nome + emoji bandiera, BIO (troncata a 4 righe via `-webkit-line-clamp`), estratto quote (troncato a 3 righe), label "leggi di più →"
  - Retro: tasto X (top-right), nome, quote completa con `overflow-y: auto; max-height: 320px` (desktop) / `260px` (mobile)
  - Flip via `transform: rotateY(180deg)` con `backface-visibility: hidden`; nessuna libreria JS esterna
  - Quando una card è flippata: `track.style.overflowX = 'hidden'` e `scrollSnapType = 'none'` per bloccare lo scroll orizzontale
  - Touch: `touchmove` e `touchstart` sul retro usano `stopPropagation()` per prevenire conflitti
  - Keyboard: Enter/Space attiva la card, Escape chiude tutte
- **Foto reali**: tutte e 6 le foto da `media/quote-testimonial_*.jpg`
- Estratti generati a partire dalle quote complete approvate
- Aggiunto progress bar nel controllo slider
- Rimossi i placeholder Unsplash

### Sezione 7 — Conclusione
- Titolo aggiornato: "Cosa emerge davvero da questa ricerca"
- Headline: "Le persone non hanno smesso di cercarsi."
- Introdotto testo d'apertura approvato
- **Nuovo `conc-stats`**: lista animata con 9 punti dati chiave (count-up sui numeri inline)
- Frase di chiusura aggiornata con il testo definitivo approvato
- `press@weroad.it` nel colophon confermato

### Note a piè di pagina (sistema nuovo)
- **8 footnotes** implementate come popup inline (no sezione visibile)
- Ogni riferimento nel testo è un `<button class="fn-ref" data-fn="N">` con sottolineatura puntinata
- Un popup condiviso (`#fnPopup`) appare al centro dello schermo con overlay scuro
- Contenuto popup: label (fonte + anno) + testo citazione
- Chiusura: click su ×, click sull'overlay, tasto Escape
- Footnotes presenti: OECD¹, OMS²×3, World Happiness Report³, Skyscanner⁴, GetYourGuide⁵, Eventbrite⁶, Scott Galloway⁷, Fortune/Fabio Bin⁸

### Rimosso
- **Tweaks panel** (⚙): rimossi CSS, HTML e JS del pannello di configurazione in-page
- Tutti i pullquote fittizi con personaggi inventati
- Script `APPLY TWEAKS` e relativo `window.TWEAK_DEFAULTS`
- Script `EUROPE REAL MAP` (non più necessario con la nuova visualizzazione città)
- Script `TWEAKS PANEL` (UI e host protocol)

### Stile preservato integralmente
- CSS tokens: `--paper: #1A1A1A`, `--accent: #FF4758`, `--ink: #F5F2ED`
- Font: Google Sans + Google Sans Mono (via Google Fonts CDN)
- Animazioni IntersectionObserver + scroll listener (doppio sistema, bulletproof)
- Struttura sezioni: chapter label + number + rule + heading
- Grain texture overlay
- Scroll progress bar rossa in cima
- Page meta strip (mix-blend-mode: difference)
- Hero con video loop a 28% opacità
- Sezione 4: fullscreen hero `A-04_the-turn-hero.jpg` con `.c-turn-hero` / `.c-turn-stats`
- Sezione 5: video SXSW a 75% altezza con mask-image fade
- Slider orizzontale con scroll-snap + controlli prev/next

### URI media
Tutti relativi (`media/nome.ext`), nessun URL assoluto. File standalone, nessuna dipendenza esterna eccetto Google Fonts.
