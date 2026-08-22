---
id: x-height
name: x-height
type: metric
status: live
anchor: [600, 468]
region: {shape: metric, y: 468}
---

# x-height

**What it is** — 468 units of 1000. The line the lowercase is built to, and the single number that most determines whether a text face reads large or small at a given point size.

**Status** — Live. Cited: `OS/2.sxHeight = 468` in `ClarendonLTStd.otf`.

**Hits** — Every lowercase glyph in the font at once. It is by far the most expensive number on this map to change, and the only one whose blast radius leaves this glyph entirely.

**Does not hit** — This glyph's actual measured height. The a crests at 483, not 468. That gap is deliberate and is mapped separately at [overshoot](overshoot.md).
