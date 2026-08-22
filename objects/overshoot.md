---
id: overshoot
name: Overshoot
type: correction
status: leftover
anchor: [300, 483]
region: {shape: metric, y: 483}
---

# Overshoot

**What it is** — The a breaks its own metrics at both ends: 483 at the crest against a 468 x-height, and −15 at the base against a 0 baseline. Fifteen units past the line, top and bottom.

**Status** — Leftover, in the precise sense this map uses the word: an inherited correction that is still doing its job and must not be tidied away. Cited: glyph bounds (23, −15, 556, 483) against `sxHeight = 468` and baseline 0.

**Hits** — How big the letter looks. Round and pointed shapes read small when they stop exactly on a flat line, so the punchcutter pushed them past it. Remove the overshoot and the a shrinks optically next to n and x.

**Does not hit** — The metrics themselves. Nothing here is misaligned. This is the card most likely to be "fixed" by a cold reader who sees 483 ≠ 468 and assumes a rounding error. It is a correction, not a defect.
