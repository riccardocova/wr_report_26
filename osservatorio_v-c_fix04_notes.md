# Note su Variante C (Fix 03)

**Data**: 21 Maggio 2026
**File base**: `preview/osservatorio_v-c.html`
**Obiettivo**: Convertire completamente il tema a "Dark Mode", adottare Google Sans per la tipografia, migliorare leggibilità e contrasto dei testi secondari.

## Modifiche effettuate

- **Dark Mode Globale**: Invertite le variabili `--paper` e `--ink` nel CSS. Lo sfondo globale ora è scuro (`#1A1A1A`), i testi principali sono chiari.
- **Tipografia principale**: Sostituiti tutti i font con **Google Sans** e **Google Sans Mono**. Font-weight dei titoli impostato a 700.
- **Testi secondari (Monospace)**: Aumentata la dimensione base dei font monospace (eyebrow, nomi dei partecipanti). È stato aggiunto peso e contrasto, facendoli spiccare su sfondo scuro.
- **Sezione 02 (Geografia)**: Sostituito lo sfondo piatto grigio scuro con il video ambient `A-02_geography-ambient.mp4` a bassa opacità (18%) su fondo nero, per dare più profondità.
- **Sezione 01 (Dati)**: Aggiunto spazio (margin-bottom) sotto al paragrafo introduttivo per distanziarlo dal primo filetto separatore delle statistiche.
- **Sezione 02 (Dati e OMS)**: Nel box di sinistra (Mappa) è stato applicato un effetto glassmorphism moderato per intravedere il video. Il blocco di destra (statistiche OMS) è stato invece liberato da bordi e sfondi, piazzando i numeri direttamente "a vivo" sul video e schiarendo i font di contorno per garantirne la leggibilità.
- **Sezione 06 (Focus Group)**: Aggiornato il gradiente applicato sopra al video di SXSW in modo che sfumi elegantemente nel nuovo sfondo scuro anziché verso un colore chiaro spezzato.
- **Sezione Cover/Hero**: Ridotto leggermente il `font-size` massimo del titolo principale. Aggiunto un gradiente grigio scuro inferiore per far risaltare maggiormente i testi di navigazione (Inizia la lettura, 7 Capitoli) e incrementato lo spazio verticale prima del filetto separatore inferiore.
