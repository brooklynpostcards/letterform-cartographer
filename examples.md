## Worked map — Clarendon lowercase `a`

Territory: one glyph, `ClarendonLTStd.otf`, cited 2026-08-21. Eleven cards live in [`objects/`](objects/) — this file is the catalog, not a copy of them. Terminology audited against the `typography-fundamentals` skill's glossary; two terms drafted from memory ("arch," "tail") were wrong and replaced — see [`reference/decisions.md`](reference/decisions.md).

### Catalog

| Part          | Type            | Status            | Card                                                    |
| ------------- | --------------- | ----------------- | -------------------------------------------------------- |
| Stem          | stroke          | 🟢 live           | [`objects/stem.md`](objects/stem.md)                      |
| Bowl          | stroke          | 🟢 live           | [`objects/bowl.md`](objects/bowl.md)                      |
| Finial        | stroke          | 🟢 live           | [`objects/finial.md`](objects/finial.md)                  |
| Ball terminal | stroke ending   | 🟢 live           | [`objects/ball-terminal.md`](objects/ball-terminal.md)    |
| Spur          | stroke ending   | 🟢 live           | [`objects/spur.md`](objects/spur.md)                      |
| Counter       | negative space  | 🟢 live, derived  | [`objects/counter.md`](objects/counter.md)                |
| Aperture      | negative space  | 🟢 live, derived  | [`objects/aperture.md`](objects/aperture.md)              |
| x-height      | metric          | 🟢 live           | [`objects/x-height.md`](objects/x-height.md)              |
| Baseline      | metric          | 🟢 live           | [`objects/baseline.md`](objects/baseline.md)              |
| Overshoot     | correction      | 🟡 leftover       | [`objects/overshoot.md`](objects/overshoot.md)            |
| Foot serif    | stroke          | 👻 ghost          | [`objects/foot-serif.md`](objects/foot-serif.md)          |

A cold reader stops here unless one part needs opening.

### One walk, in full

*Question: "I want to give this Clarendon `a` a heavier slab foot to match the rest of the face. What does that touch?"*

1. Open the catalog above. "Foot serif" is the obvious door.
2. Open `objects/foot-serif.md`. It says, in the first line of body text: there is no foot serif on this glyph. Status: **ghost**.
3. Stop. The question's premise is wrong — there's no existing foot serif to make heavier. The card also names the two real strokes a reader might have meant instead: [`spur`](objects/spur.md) and [`ball-terminal`](objects/ball-terminal.md), and explains, with a cited coordinate walk, why neither is a serif.

No other card had to be opened to answer this. That's the point of the catalog.

### A second walk, shorter

**Question:** "What's the counter, and can I make it bigger on its own?"

1. Open `objects/counter.md`.
2. **Hits**: nothing directly — it's derived from `bowl` and `stem`.
3. **Does not hit**: the aperture, a separate white shape people usually mean instead.
4. Answer: no, not on its own. Edit `bowl` or `stem`; the counter follows. Stop.

### A third walk, on vocabulary itself

**Question:** "What's the arch called on this a?"

1. There is no `arch.md`. The catalog has no row named "Arch."
2. `reference/naming-collisions.md` names this exact question and points to [`objects/finial.md`](objects/finial.md) — the skill-grounded term for this letter, with the reason "arch" doesn't apply here (it never returns to the baseline, so it isn't one).
3. Stop, with the vocabulary corrected, not just the geometry located.
