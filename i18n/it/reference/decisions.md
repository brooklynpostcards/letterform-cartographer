## Decisioni

Registrato per la forma Decision Record di `icm-md-writer` - in modo che una sessione successiva non ri-argomenti o inverta silenziosamente entrambe le chiamate.

---

**Decision:** Map Clarendon LT Std (`ClarendonLTStd.otf`, Adobe), not Ringold (`Ringold-Clarendon`, Bijou Type).

**Context:** Adobe Fonts returned two “Clarendon” matches. Ringold is a 2020s Bijou Type design by Dan Rhatigan with a style cut named “Clarendon”; Clarendon URW / Clarendon LT Std are digitizations of the original 1845 Fann Street Foundry design.

**Options considered:** Ringold (available, contemporary reinterpretation), Clarendon URW (Adobe Fonts, faithful digitization), Clarendon LT Std (found locally, same lineage as URW's source).

**Rationale:** Clarendon LT Std è stato confermato sulla macchina dell'utente e verificato con una seconda fonte indipendente (SuperClarendon) prima dell'uso, ma non è stato ancora approvato per l'utilizzo su un computer.

**Consequences:** Every card in `objects/` cites `ClarendonLTStd.otf` specifically. A card built from Ringold's outline would not match — the shapes differ (this was tested: Ringold's lowercase a follows the general double-storey pattern but its terminal geometry is not identical).

---

**Decision:** Rename “Arch” → **Finial**, “Tail” → **Spur**.

**Context:** Entrambe le carte sono state redatte partendo da conoscenze tipografiche generali, poi controllate contro la `glossary.md` dell'abilità caricata `typography-fundamentals` — la fonte su cui si suppone che l'intera mappa sia basata.

**Options considered:** Mantenere "Arco" e "Coda" (termini comuni, probabilmente più chiari per un lettore profano) vs. passare ai termini definiti dall'abilità stessa.

**Rationale:** `glossary.md` does not define “Arch” at all. It defines **Finial** — “an ornamental terminal stroke at the top of characters such as *a* and *f*” — explicitly for this letter. It defines **Tail** only for Q, K, R, and g's loop, not for *a*; it defines **Spur** as “the terminal to the stem of a rounded letter,” which is the correct fit. `rules.md` for this territory says a card must cite grounded terminology, not memory — using “Arch” and “Tail” would have violated this map's own rule.

**Consequences:** `reference/naming-collisions.md` documenta entrambi gli swap come la collisione che un lettore probabilmente colpirà per primo, dal momento che “arch” e “tail” sono le parole che la maggior parte delle persone raggiunge per analogia a *n*/*m*/*h* e *g*/*Q* rispettivamente.

---

**Decision:** Rideriva le regioni dello stelo e delle estremità da una scansione punto-in-poligono del contorno reale, sostituendo le caselle di delimitazione posizionate a occhio.

**Context:** Building the live diagram surfaced that `stem`'s hover region (`x: 428, y: 52, w: 145, h: 306`) mostly covered background, not ink — its anchor and clip rectangle had been eyeballed from the earlier text-only coordinate walk rather than checked against the actual filled shape. A systematic scan (`fontTools` outline, ray-casting point-in-polygon, counter treated as a hole) found the stem's real ink at mid-height spans only x=302–440, not the x=428–573 range the original card used — the card had conflated the glyph's overall right bound (556, which belongs to the spur) with the stem's own edge.

**Options considered:** Patch la carta in isolamento vs. ri-scansione dell'ancoraggio e della regione di ogni carta di colpo contro lo stesso metodo.

**Rationale:** Se una regione posizionata a mano era sbagliata, le altre erano costruite nello stesso modo e richiedevano lo stesso controllo, non solo quella che un utente ha notato per caso. Tutti e cinque gli ancoraggi del tratto sono stati ri-verificati da punto-in-poligono; quattro (bowl, finial, terminale a sfera, sperone) erano già su inchiostro reale, ma il rettangolo della regione del finial è stato stretto per corrispondere al suo rapporto d'inchiostro effettivo (~52% contro l'originale dello stelo ~0%). Un rettangolo non può collegare perfettamente un tratto curvo - finial e bowl entrambi atterrano vicino al 50% di copertura dell'inchiostrazione anche se correttamente montati, perché i loro lati concavi necessariamente tirano in qualche sfondo.

**Consequences:** `objects/stem.md` e `objects/finial.md` sono stati riscritti con il frontespizio corretto di `anchor`/`region` e la prosa corretta (la vecchia affermazione della carta che il suo bordo destro ha raggiunto x=556 era sbagliata ed è stata richiamata nella carta stessa piuttosto che risolto in silenzio).

---

**Decision:** Cap `stem`'s region at y≥165 and `spur`'s at y≤165, instead of letting both run through y=60–165.

**Context:** The corrected stem region above still spanned y=60–355, which overlaps `spur`'s region (y=−22–190) across x=332–440 — the exact band where the spur's curl lifts off the stem's base. Hotspots are layered in DOM order, so within that overlap `spur`'s hotspot (added later) always won, making `stem` unreachable by hover in its lower third even though its region rectangle was, on paper, mostly on-ink.

**Options considered:** Riordinare il DOM in modo che lo stelo venga dipinto per ultimo (corregge il sintomo, non la causa — cambia solo quale parte diventa irraggiungibile); ridurre una regione arbitrariamente; dividere l'intervallo y nel punto effettivo in cui l'inchiostro dei due tratti si separa.

**Rationale:** The segment scan (`reference/decisions.md`'s earlier entry) shows the spur's ink exists as an isolated island separate from the stem only below y≈165; above that, only the stem's own segment continues. Splitting the two regions at y=165 removes the overlap entirely rather than papering over it with z-order.

**Consequences:** L'altezza della regione `objects/stem.md` si è ridotta a 185 (y:165–350); l'altezza dell'area `objects/spur.md` si è ridotto a 197 (y:−22–165).

---

**Decision:** Il rendering dell'evidenziazione è passato da un `clip-path` rigido a uno `mask` sfocato (feGaussianBlur, stdDeviation 16) per ogni regione rettangolare / circolare.

**Context:** Una volta che i punti salienti erano effettivamente visibili (vedi precedente voce), il confine stesso era ancora sbagliato in un altro modo: il bordo dritto di una regione spesso non ha alcun significato anatomico - esiste solo per impedire che il punto saliente sanguini in una parte vicina (ad esempio la divisione stelo/sperone a y=165, che si trova a metà della curva su un singolo tratto verticale ininterrotto senza giunzione reale lì). Una clip rigida ha reso quel taglio arbitrario sembrare un rettangolo incollato sopra la lettera, più visibilmente su `spur`, il cui punto saliente aveva una parte superiore orizzontale piatta che tagliava dritto attraverso il ricciolo.

**Options considered:** (1) tracciare a mano i veri sotto-tracciati dai comandi bezier effettivi del font in modo che ogni confine segua l'inchiostro reale — studiato direttamente contro i dati grezzi del tracciato; rifiutato per ora perché diverse parti (la spirale a sfera terminale in particolare) si raddoppiano su se stesse in un modo che non si riduce a tagli di indice di punti puliti senza il rischio reale di introdurre spazi o auto-intersezioni che sono difficili da verificare visivamente. (2) Ellissi invece di linee rette — meglio delle linee rette sulle parti curve, ancora un bordo rigido arbitrario. (3) Maschera morbida invece di clip rigida.

**Rationale:** Una maschera con un rettangolo/cerchio sfocato mantiene ogni bordo di inchiostro *vero* nitide come prima — la maschera è a piena opacità molto prima di raggiungere la silhouette reale — e riduce l'opacità solo vicino al confine artificiale stesso, dove non esiste un vero bordo da preservare. Questo si legge come "l'area generale di questo tratto" piuttosto che "questo esatto rettangolo", che è la cosa onesta da affermare dato che il confine è davvero una chiamata di giudizio, non un fatto misurato. La tecnica di contro-punzonatura della voce precedente non è influenzata: sia il riempimento dell'accento che il punzonatura colorata di sfondo condividono la stessa maschera, quindi il vero bordo del contatore rimane nitide per tutto — confermato dallo zoom visivo diretto, non solo l'ispezione DOM.

**Consequences:** `defs` ora emette un `<filter id="soft-edge">` condiviso più uno `<mask>` per carta di colpo (sostituendo il vecchio `<clipPath>` per carta); `fillPath`/`punch` usano `mask="url(#mask-ID)"` invece di `clip-path` Nessun contenuto della carta cambiato — questa è puramente una tecnica di rendering, non un re-scoping di qualsiasi regione.

---

**Decision:** Sostituire la maschera sfocata (voce precedente) con una clip `ellipse` con bordi rigidi per `bowl`, `finial` e `spur`; `stem` rimane un `rect` letterale.

**Context:** La sfocatura ha risolto il problema dell'"ovvio rettangolo", ma ne ha introdotto uno nuovo: un bagliore morbido e sfocato si legge come impreciso, e entra in conflitto con il resto del linguaggio del diagramma, chiaro e a colori piatti (riempimento Clarendon solido, etichette Akzidenz solide, ritaglio del contatore con bordi duri).

**Options considered:** Un raggio di sfocatura più piccolo (ancora morbido, solo meno); veri sotto-tracciati tracciati a mano dai veri comandi bezier del font (indagati e rifiutati nella voce sopra — la spirale a sfera terminale non si riduce a tagli puliti); una forma a bordi duri più adatta a un tratto curvo che a un rettangolo allineato all'asse.

**Rationale:** A rectangle has flat sides, so any edge that crosses a stroke does so as a dead-straight cut — the artifact that made `spur` look like a box. An ellipse has no flat sides: wherever its boundary crosses the stroke, it does so at an angle, which reads as a rounded, deliberate highlight rather than a pasted-on shape, while staying exactly as hard-edged and “measured” as the rest of the diagram. `stem` is excluded because it's genuinely a straight vertical stroke — a rect is the anatomically correct shape there, not a compromise.

**Consequences:** `objects/bowl.md`, `objects/finial.md`, `objects/spur.md` frontmatter changed `region.shape` from `rect` to `ellipse` (same `x`/`y`/`w`/`h` — now read as an ellipse's bounding box, `cx`/`cy` at its center, `rx`/`ry` at half its width/height). `docs/index.html` gained a shared `regionShapeEl(r)` helper so the clip-path defs, the highlight fill/punch, and the hotspot all build the identical rect/circle/ellipse from one place instead of three separately-maintained branches — the kind of duplication that let the coordinate-space bug (two entries up) go unnoticed as long as it did. The blur filter and per-card masks were removed entirely.

---

**Decision:** Tirare il bordo sinistro di `stem` da x=320 a x=328, restringendo la sua regione da 120 a 112 di larghezza.

**Context:** `stem`'s region and `counter`'s bounds (x=157–323) overlapped by 3 units (320–323). The counter-punch (two entries up) already prevents solid fill from painting over the counter's true hole even there, so this was never a color-accuracy bug — but a 3-unit sliver where a rounded-rect corner nearly grazes a curved hole is exactly the kind of imprecision that reads as visually unsettled up close, and it was flagged as such.

**Rationale:** `stem` e `counter` condividono davvero un bordo nell'anatomia - la linea Hits di `objects/stem.md` lo dice ("il bordo sinistro dello stelo è anche la parete destra del contatore"). La correzione non è quella di negare questa vicinanza, ma solo di smettere di renderla come un quasi-fallimento. Rieseguendo il controllo del rapporto di inchiostro ai bordi tirati (x=328, w=112) abbiamo trovato una copertura dell'inchiostro del 100%, più stretta del 92% della regione originale di 120 - le 3 unità tagliate non erano mai state inchiostri solidi a questa altezza comunque.

**Consequences:** La larghezza della regione `objects/stem.md` è stata modificata da 120 a 112, x 320 → 328. Anchor (380,210) riconfermato on-ink. Nessun cambiamento di prosa necessario — l'intervallo di inchiostro citato dalla scheda (x=324–440 a y=210) era già accurato; solo la regione di rendering, un sottoinsieme deliberatamente conservativo, è stato spostato.
