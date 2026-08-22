## Decisions

Logged per `icm-md-writer`'s Decision Record shape — so a later session doesn't re-argue or silently reverse either call.

---

**Decision:** Map Clarendon LT Std (`ClarendonLTStd.otf`, Adobe), not Ringold (`Ringold-Clarendon`, Bijou Type).

**Context:** Adobe Fonts returned two "Clarendon" matches. Ringold is a 2020s Bijou Type design by Dan Rhatigan with a style cut named "Clarendon"; Clarendon URW / Clarendon LT Std are digitizations of the original 1845 Fann Street Foundry design.

**Options considered:** Ringold (available, contemporary reinterpretation), Clarendon URW (Adobe Fonts, faithful digitization), Clarendon LT Std (found locally, same lineage as URW's source).

**Rationale:** The brief was "the classic slab serif" — the historical original, not a contemporary typeface that borrowed its name for one cut. Clarendon LT Std was confirmed on the user's own machine and verified against a second independent source (SuperClarendon) before use.

**Consequences:** Every card in `objects/` cites `ClarendonLTStd.otf` specifically. A card built from Ringold's outline would not match — the shapes differ (this was tested: Ringold's lowercase a follows the general double-storey pattern but its terminal geometry is not identical).

---

**Decision:** Rename "Arch" → **Finial**, "Tail" → **Spur**.

**Context:** Both cards were drafted first from general typographic knowledge, then audited against the loaded `typography-fundamentals` skill's `glossary.md` — the source this whole map is supposed to be grounded in.

**Options considered:** Keep "Arch" and "Tail" (common terms, arguably clearer to a lay reader) vs. switch to the skill's own defined terms.

**Rationale:** `glossary.md` does not define "Arch" at all. It defines **Finial** — "an ornamental terminal stroke at the top of characters such as *a* and *f*" — explicitly for this letter. It defines **Tail** only for Q, K, R, and g's loop, not for *a*; it defines **Spur** as "the terminal to the stem of a rounded letter," which is the correct fit. `rules.md` for this territory says a card must cite grounded terminology, not memory — using "Arch" and "Tail" would have violated this map's own rule.

**Consequences:** `reference/naming-collisions.md` documents both swaps as the collision a reader is likely to hit first, since "arch" and "tail" are the words most people reach for by analogy to *n*/*m*/*h* and *g*/*Q* respectively.

---

**Decision:** Re-derive the stem and finial regions from a point-in-polygon scan of the real outline, replacing bounding boxes that were placed by eye.

**Context:** Building the live diagram surfaced that `stem`'s hover region (`x: 428, y: 52, w: 145, h: 306`) mostly covered background, not ink — its anchor and clip rectangle had been eyeballed from the earlier text-only coordinate walk rather than checked against the actual filled shape. A systematic scan (`fontTools` outline, ray-casting point-in-polygon, counter treated as a hole) found the stem's real ink at mid-height spans only x=302–440, not the x=428–573 range the original card used — the card had conflated the glyph's overall right bound (556, which belongs to the spur) with the stem's own edge.

**Options considered:** Patch the one card in isolation vs. re-scan every stroke card's anchor and region against the same method.

**Rationale:** If one hand-placed region was wrong, the others were built the same way and warranted the same check, not just the one a user happened to notice. All five stroke anchors were re-verified by point-in-polygon; four (bowl, finial, ball terminal, spur) already sat on real ink, but finial's region rectangle was tightened to match its actual ink ratio (~52% vs. stem's original ~0%). A rectangle can't perfectly bound a curved stroke — finial and bowl both land near 50% ink coverage even correctly fitted, because their concave sides necessarily pull in some background. That's expected for a rect clip on a curved letterform, not a defect.

**Consequences:** `objects/stem.md` and `objects/finial.md` were rewritten with corrected `anchor`/`region` frontmatter and corrected prose (the old stem card's claim that its right edge reached x=556 was wrong and is called out in the card itself rather than silently fixed).

---

**Decision:** Cap `stem`'s region at y≥165 and `spur`'s at y≤165, instead of letting both run through y=60–165.

**Context:** The corrected stem region above still spanned y=60–355, which overlaps `spur`'s region (y=−22–190) across x=332–440 — the exact band where the spur's curl lifts off the stem's base. Hotspots are layered in DOM order, so within that overlap `spur`'s hotspot (added later) always won, making `stem` unreachable by hover in its lower third even though its region rectangle was, on paper, mostly on-ink.

**Options considered:** Reorder the DOM so stem paints last (fixes the symptom, not the cause — just flips which part becomes unreachable); shrink one region arbitrarily; split the y-range at the actual point the two strokes' ink separates.

**Rationale:** The segment scan (`reference/decisions.md`'s earlier entry) shows the spur's ink exists as an isolated island separate from the stem only below y≈165; above that, only the stem's own segment continues. Splitting the two regions at y=165 removes the overlap entirely rather than papering over it with z-order.

**Consequences:** `objects/stem.md` region height shrank to 185 (y:165–350); `objects/spur.md` region height shrank to 187 (y:−22–165). Both anchors re-verified on-ink after the change.

---

**Decision:** Highlight rendering switched from a hard `clip-path` to a blurred `mask` (feGaussianBlur, stdDeviation 16) for every rect/circle region.

**Context:** Once the highlights were actually visible (previous entry), the boundary itself was still wrong in a different way: a region's straight edge frequently has no anatomical meaning — it exists only to stop the highlight from bleeding into a neighbouring part (e.g. the stem/spur split at y=165, which sits mid-curve on a single unbroken vertical stroke with no real joint there). A hard clip made that arbitrary cut look like a rectangle had been pasted over the letter, most visibly on `spur`, whose highlight had a flat horizontal top slicing straight across the curl.

**Options considered:** (1) hand-trace true sub-paths from the font's actual bezier commands so every boundary follows real ink — investigated directly against the raw path data; rejected for now because several parts (the ball-terminal spiral in particular) double back on themselves in a way that doesn't reduce to clean point-index cuts without real risk of introducing gaps or self-intersections that are hard to verify visually. (2) Ellipses instead of rects — better than rects on curved parts, still an arbitrary hard edge. (3) Soft mask instead of hard clip.

**Rationale:** A mask with a blurred rect/circle keeps every *true* ink edge exactly as sharp as before — the mask is at full opacity well before it reaches the real silhouette — and only feathers opacity near the artificial boundary itself, where no real edge exists to preserve. This reads as "the general area of this stroke" rather than "this exact rectangle," which is the honest thing to claim given the boundary really is a judgment call, not a measured fact. The counter-punch technique from the previous entry is unaffected: both the accent fill and the bg-colored punch share the same mask, so the counter's own true edge stays crisp throughout — confirmed by direct visual zoom, not just DOM inspection.

**Consequences:** `defs` now emits one shared `<filter id="soft-edge">` plus one `<mask>` per stroke card (replacing the old `<clipPath>` per card); `fillPath`/`punch` use `mask="url(#mask-ID)"` instead of `clip-path`. No card content changed — this is purely a rendering technique, not a re-scoping of any region.
