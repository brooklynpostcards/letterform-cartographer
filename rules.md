## What counts as a noun

An **anatomical part**: a named range of the glyph's outline, or a named font-wide reference line the outline is measured against. Eleven exist in this territory — nine live, one leftover, one ghost.

Two kinds of noun:

- **Stroke parts** (stem, bowl, finial, ball terminal, spur) — a contiguous stretch of the outer contour.
- **Derived shapes** (counter, aperture) — white space bounded by stroke parts, with no contour of their own.
- **Metrics** (x-height, baseline, overshoot) — horizontal reference lines from the font's own tables, not the glyph's contour at all.

## What counts as movement

Editing a stroke part changes the outline range it names, and anything that range structurally borders. A stem sharing an edge with the counter means widening the stem narrows the counter — that is a real hit, cite it. A stem sharing nothing with the x-height means changing the stem never touches it — that is a real miss, cite it too.

Metrics move differently: they hit *every glyph in the font*, never just this one. That asymmetry — one glyph's stroke change stays local, one font-wide metric change goes global — is the single most important thing a card in this territory can get right.

## Live / Leftover / Ghost, defined for this territory

- **Live** — the part corresponds to a real range of the actual outline, citable by point index and coordinate.
- **Leftover** — the part is real and present, but its reason for existing is a correction from an earlier design tradition, not a feature of this glyph on its own. The overshoot: still doing its job, still worth explaining, not something to "fix."
- **Ghost** — the part has a name a reader will reach for, and nothing behind it in this specific glyph. This territory's ghost, the foot serif, exists precisely because the typeface's own category (slab serif) sets an expectation this letter doesn't meet.

## Hits / Does not hit

Every card ends with exactly two lines. **Hits** names the real structural neighbor. **Does not hit** names the wrong neighbor a reader would guess first — usually the part that looks adjacent in the rendered letterform but shares no actual boundary in the outline data.

## Refusals

- No pasting the glyph's raw path data into a card as if that were an explanation — cite point ranges and bounds, same discipline as citing a file path instead of pasting a script.
- No treating a derived shape (counter, aperture) as if it had independent geometry to edit.
- No smoothing over the ghost. A part that doesn't exist gets a card that says so, not silence.

## How a card gets built

Before writing any card: extract the real outline (`fontTools`, not a rendered image, not a memory of what Clarendon “should” look like), identify which point range the part occupies, and check it against a second independent source of the same typeface before trusting anything that looks surprising. This territory's ghost card exists because that check was necessary — the first look at the outline seemed wrong precisely where it was actually right.
