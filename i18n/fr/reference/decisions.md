## Décisions

Enregistré par la forme d'enregistrement de décision de `icm-md-writer` - donc une session ultérieure ne re-argumente pas ou n'annule silencieusement aucun appel.

---

**Decision:** Map Clarendon LT Std (`ClarendonLTStd.otf`, Adobe), not Ringold (`Ringold-Clarendon`, Bijou Type).

**Context:** Adobe Fonts returned two “Clarendon” matches. Ringold is a 2020s Bijou Type design by Dan Rhatigan with a style cut named “Clarendon”; Clarendon URW / Clarendon LT Std are digitizations of the original 1845 Fann Street Foundry design.

**Options considered:** Ringold (available, contemporary reinterpretation), Clarendon URW (Adobe Fonts, faithful digitization), Clarendon LT Std (found locally, same lineage as URW's source).

**Rationale:** La police Clarendon LT Std a été confirmée sur la propre machine de l'utilisateur et vérifiée par rapport à une deuxième source indépendante (SuperClarendon) avant son utilisation, et les résultats ont été publiés dans le journal de l'Académie des sciences.

**Consequences:** Every card in `objects/` cites `ClarendonLTStd.otf` specifically. A card built from Ringold's outline would not match — the shapes differ (this was tested: Ringold's lowercase a follows the general double-storey pattern but its terminal geometry is not identical).

---

**Decision:** Rename “Arch” → **Finial**, “Tail” → **Spur**.

**Context:** Les deux cartes ont d'abord été rédigées à partir de connaissances typographiques générales, puis vérifiées par rapport à la `glossary.md` de la compétence `typography-fundamentals` chargée - la source sur laquelle toute cette carte est censée être fondée.

**Options considered:** Gardez "Arc" et "Queue" (termes communs, sans doute plus clairs pour un lecteur non spécialisé) vs. passez aux termes définis par la compétence.

**Rationale:** `glossary.md` ne définit pas du tout “Arc”. Il définit **Finial** — “un trait terminal ornemental au sommet de caractères tels que *a* et *f*” — explicitement pour cette lettre. Il définit uniquement **Tail** pour la boucle de Q, K, R, et g, pas pour *a*; il définit un **Spur** comme “le terminal de la tige d'une lettre arrondie”, ce qui est le bon ajustement. `rules.md` pour ce territoire dit qu'une carte doit citer la terminologie fondée, pas la mémoire — en utilisant “Arc” et “Queue” aurait violé la règle de cette carte.

**Consequences:** `reference/naming-collisions.md` documente les deux échanges comme la collision qu’un lecteur est susceptible de rencontrer en premier, puisque « arc » et « queue » sont les mots que la plupart des gens utilisent par analogie avec *n*/*m*/*h* et *g*/*Q* respectivement.

---

**Decision:** Redérivez les régions de la tige et des extrémités à partir d'un balayage point-dans-polygone du contour réel, en remplaçant les boîtes de délimitation qui ont été placées à l'œil.

**Context:** Building the live diagram surfaced that `stem`'s hover region (`x: 428, y: 52, w: 145, h: 306`) mostly covered background, not ink — its anchor and clip rectangle had been eyeballed from the earlier text-only coordinate walk rather than checked against the actual filled shape. A systematic scan (`fontTools` outline, ray-casting point-in-polygon, counter treated as a hole) found the stem's real ink at mid-height spans only x=302–440, not the x=428–573 range the original card used — the card had conflated the glyph's overall right bound (556, which belongs to the spur) with the stem's own edge.

**Options considered:** Patch la carte en isolation vs re-scanner l'ancre et la région de chaque carte de trait contre la même méthode.

**Rationale:** Si une région placée à la main était incorrecte, les autres étaient construites de la même manière et justifiaient le même contrôle, pas seulement celle qu'un utilisateur a remarqué par hasard. Les cinq ancrages de trait ont été re-vérifiés par point-dans-polygone; quatre (bowl, finial, terminal à bille, spur) étaient déjà sur de l'encre réelle, mais le rectangle de la région du finial a été serré pour correspondre à son ratio d'encre réel (~52% vs. ~0% original de la tige). Un rectangle ne peut pas parfaitement lier un trait courbe — le finial et le bowl atterrissent tous deux près de 50% de couverture d'encres même correctement ajustés, parce que leurs côtés concaves tirent nécessairement dans un certain arrière-plan.

**Consequences:** `objects/stem.md` et `objects/finial.md` ont été réécrits avec le frontmatter `anchor`/`region` corrigé et la prose corrigée (l'affirmation de l'ancienne carte de base que son bord droit atteignait x=556 était fausse et est appelée dans la carte elle-même plutôt que de se fixer silencieusement).

---

**Decision:** Cap `stem`'s region at y≥165 and `spur`'s at y≤165, instead of letting both run through y=60–165.

**Context:** The corrected stem region above still spanned y=60–355, which overlaps `spur`'s region (y=−22–190) across x=332–440 — the exact band where the spur's curl lifts off the stem's base. Hotspots are layered in DOM order, so within that overlap `spur`'s hotspot (added later) always won, making `stem` unreachable by hover in its lower third even though its region rectangle was, on paper, mostly on-ink.

**Options considered:** Réorganiser le DOM de sorte que les peintures de la tige soient les dernières (corrige le symptôme, pas la cause — inverse simplement quelle partie devient inaccessible); rétrécir une région arbitrairement; diviser la plage y au point réel où l'encre des deux traits se sépare.

**Rationale:** Le scan du segment (entrée antérieure de `reference/decisions.md`) montre que l'encre de l'éperon existe comme une île isolée séparée de la tige seulement en dessous de y≈165; au-dessus de cela, seul le propre segment de la Tige continue.Diviser les deux régions à y=165 supprime le chevauchement entièrement plutôt que de le recouvrir avec l'ordre z.

**Consequences:** La hauteur de la région `objects/stem.md` a été réduite à 185 (y:165–350) ; la hauteur des régions `objects/spur.md` ont été réduites à 177 (y:−22–165).

---

**Decision:** Le rendu des surbrillances est passé d'un `clip-path` dur à un `mask` flou (feGaussianBlur, stdDeviation 16) pour chaque région rectangulaire/cercle.

**Context:** Une fois que les points forts étaient visibles (entrée précédente), la limite elle-même était toujours erronée d'une autre manière : le bord droit d'une région n'a souvent aucune signification anatomique — il n'existe que pour empêcher le point fort de saigner dans une partie voisine (par exemple, la scission tige/éperon à y=165, qui se trouve au milieu de la courbe sur un seul trait vertical ininterrompu sans véritable joint là-bas). Un clip dur a fait que cette coupe arbitraire ressemblait à un rectangle collé sur la lettre, le plus visiblement sur `spur`, dont le point fort avait une tranche horizontale plate en haut à travers la boucle.

**Options considered:** (1) tracer à la main de vrais sous-chemins à partir des commandes de Bézier de la police afin que chaque bordure suive l'encre réelle — étudié directement par rapport aux données brutes du chemin ; rejeté pour l'instant parce que plusieurs parties (la spirale à bille en particulier) se doublent sur elles-mêmes d'une manière qui ne se réduit pas à des coupes propres à l'index point sans risque réel d'introduire des espaces ou des auto-intersections difficiles à vérifier visuellement. (2) Ellipses au lieu de rectangulaires — mieux que des rectangulaire sur les parties courbes, toujours un bord dur arbitraire. (3) Masque souple au lieu de clip dur.

**Rationale:** Un masque avec un rectangle/cercle flou garde chaque bord d'encre *vrai* aussi net qu'avant — le masque est à pleine opacité bien avant d'atteindre la silhouette réelle — et ne réduit l'opacité que près de la limite artificielle elle-même, où il n'existe pas de bord réel à préserver. Cela se lit comme « la zone générale de ce trait » plutôt que « ce rectangle exact », ce qui est la chose honnête à dire étant donné que la limite est vraiment un appel au jugement, pas un fait mesuré. La technique de contre-perforation de l'entrée précédente n'est pas affectée : le remplissage d'accent et le poinçon de couleur de fond partagent le même masque, de sorte que le bord vrai du compteur reste net tout au long — confirmé par un zoom visuel direct, pas seulement une inspection DOM.

**Consequences:** `defs` now emits one shared `<filter id="soft-edge">` plus one `<mask>` per stroke card (replacing the old `<clipPath>` per card); `fillPath`/`punch` use `mask="url(#mask-ID)"` instead of `clip-path`. No card content changed — this is purely a rendering technique, not a re-scoping of any region.

---

**Decision:** Remplacez le masque flou (entrée précédente) par un clip `ellipse` aux bords durs pour `bowl`, `finial` et `spur` ; `stem` reste un `rect` littéral.

**Context:** Le flou a corrigé le problème du « rectangle évident », mais en a introduit un nouveau — une lueur douce et floue se lit comme imprécise, et entre en conflit avec le reste du langage clair et plat du diagramme (remplissage Clarendon solide, étiquettes Akzidenz solides, contre-découpe aux bords durs).

**Options considered:** Un rayon de flou plus petit (toujours doux, juste moins); des sous-chemins tracés à la main à partir des vraies commandes de bézier de la police (enquêté et rejeté dans l'entrée ci-dessus — la spirale à billes ne se réduit pas à des coupes propres); une forme à bords durs mieux adaptée à un trait courbé qu'à un rectangle aligné sur l'axe.

**Rationale:** Un rectangle a des côtés plats, donc tout bord qui traverse un trait le fait comme une coupe droite — l'artefact qui a fait `spur` ressembler à une boîte. Une ellipse n'a pas de côtés plats : partout où sa limite traverse le trait, elle le fait à un angle, ce qui se lit comme une mise en évidence arrondie et délibérée plutôt qu'une forme collée, tout en restant exactement aussi rigide et « mesurée » que le reste du diagramme.`stem` est exclu parce qu'il s'agit véritablement d'un trait vertical droit — un rectangulaire est la forme anatomiquement correcte ici, pas un compromis.

**Consequences:** `objects/bowl.md`, `objects/finial.md`, `objects/spur.md` frontmatter changed `region.shape` from `rect` to `ellipse` (same `x`/`y`/`w`/`h` — now read as an ellipse's bounding box, `cx`/`cy` at its center, `rx`/`ry` at half its width/height). `docs/index.html` gained a shared `regionShapeEl(r)` helper so the clip-path defs, the highlight fill/punch, and the hotspot all build the identical rect/circle/ellipse from one place instead of three separately-maintained branches — the kind of duplication that let the coordinate-space bug (two entries up) go unnoticed as long as it did. The blur filter and per-card masks were removed entirely.

---

**Decision:** Pull `stem`'s left edge in from x=320 to x=328, narrowing its region from 120 to 112 wide.

**Context:** `stem`'s region and `counter`'s bounds (x=157–323) overlapped by 3 units (320–323). The counter-punch (two entries up) already prevents solid fill from painting over the counter's true hole even there, so this was never a color-accuracy bug — but a 3-unit sliver where a rounded-rect corner nearly grazes a curved hole is exactly the kind of imprecision that reads as visually unsettled up close, and it was flagged as such.

**Rationale:** `stem` et `counter` partagent réellement une bordure dans l'anatomie — la ligne Hits de `objects/stem.md` le dit (« le bord gauche de la tige est aussi la paroi droite du compteur »). Le correctif n'est pas de nier cette adjacence, mais seulement d'arrêter de le rendre comme un quasi-échec. En re-exécutant le contrôle du rapport d'encre aux limites tirées (x=328, w=112), j'ai trouvé une couverture d'encres de 100%, plus serrée que les 92% de la région originale de 120 — les 3 unités coupées n'étaient jamais des encres de tige solides à cette hauteur de toute façon.

**Consequences:** La largeur de la région `objects/stem.md` a été changée de 120 à 112, x 320 → 328. Anchor (380,210) a été reconfirmé sur l'encre. Aucun changement de prose n'était nécessaire — la plage d'encre citée par la carte (x=324–440 à y=210) était déjà exacte ; seule la région de rendu, un sous-ensemble délibérément conservateur, a été déplacée.
