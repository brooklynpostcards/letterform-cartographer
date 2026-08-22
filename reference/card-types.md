## Card types (closed set)

Three card types exist in this territory.

### Stroke / stroke-ending

A contiguous range of the outer contour. Required fields: what it is (one line, naming the skill-defined term), status with cited point range, hits, does not hit.

### Negative space (derived)

A shape bounded by strokes with no contour of its own — the counter, the aperture. Required fields are the same, but "hits" for these is almost always "nothing directly" — a derived shape has no geometry to edit, only strokes that bound it.

### Metric

A font-wide reference line, not part of the glyph's own contour — x-height, baseline, overshoot. These cite the font's own tables (`OS/2`, `hhea`) rather than the outline, and their "hits" line names every glyph in the font, not just this one — the one place in this territory where a card's blast radius leaves the letter.

## The ghost is not a fourth type

`foot-serif.md` uses the Stroke template with `status: ghost`. A ghost does not get its own shape — it gets the shape the reader expected, filled with the finding that nothing is there.

## If a twelfth part shows up

Only if the outline itself changes (a different weight, a redrawn glyph) — a new card follows one of the three templates above and gets added to the catalog table in `examples.md`. `examples.md` stays a dated snapshot otherwise.
