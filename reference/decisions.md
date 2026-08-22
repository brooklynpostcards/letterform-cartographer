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
