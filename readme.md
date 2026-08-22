# Letterform Cartographer

A system map of one glyph: the lowercase **a** in Clarendon LT Std Roman. Eleven noun cards — nine live, one leftover, one ghost — each citing an exact range of the real font outline, not a redrawn approximation of it.

## Live demo

`docs/index.html` — a hoverable diagram of the letter. Each hover fetches and renders the actual `.md` card from `objects/`, live, straight out of this repo. Nothing in the diagram is a copy of the cards; it's a viewer over them. Serve it from the repo root (GitHub Pages: source = `/ (root)`, not `/docs`) so `docs/index.html`'s relative fetch to `../objects/*.md` resolves — Pages restricted to `/docs` alone would 404 on every card.

## Why this exists

A glyph outline is just point coordinates. "Bowl," "counter," "spur" are names a human draws around ranges of that data — nothing in a font file labels itself. This repo is that labeling, done once, cited against both the real extracted outline (`fontTools`) and a loaded typography reference skill, so nobody has to re-derive it by eye.

## The one ghost, explained up front

Clarendon is a slab serif — that's the first and often only thing anyone knows about it, and it creates a confident, wrong expectation: that every stroke in the face ends in a bracketed slab foot. This lowercase `a` doesn't. Its stem ends in a curved spur, its finial ends in a ball terminal, and no foot serif exists anywhere on the letter. That's not a simplification or an artistic choice being described loosely — it's a fact about the actual outline, verified against a second independent Clarendon after the first extraction was nearly discarded as corrupt for lacking the very serif this README just told you not to expect. See [`objects/foot-serif.md`](objects/foot-serif.md) for the full account.

## How a stranger — or a cold AI session — uses this

1. Read `identity.md` and `rules.md` once. They're short.
2. Open `examples.md`. It's a catalog table of all eleven parts plus three short worked walks.
3. Need one part? Open exactly its card in `objects/`. Stop there.
4. Hit a name that isn't in the catalog ("arch," "tail")? Check `reference/naming-collisions.md` first — it's very likely already answered.

**The one rule: load the catalog, then one card. Never all eleven at once.**

## What's here

| Path | Job |
| --- | --- |
| `identity.md` | Who the cartographer is, whose territory this is, who the later reader is |
| `rules.md` | What counts as a noun here, how Live/Leftover/Ghost are decided, the Hits/Does-not-hit rule |
| `examples.md` | The catalog table + three worked walks, dated 2026-08-21 |
| `objects/` | The eleven cards themselves — the actual shelves |
| `reference/card-types.md` | The three card shapes this territory uses |
| `reference/naming-collisions.md` | Four real vocabulary traps, written down once |
| `reference/decisions.md` | Logged decisions (font choice; terminology corrections; rendering technique) with rationale |
| `docs/index.html` | The live diagram — a viewer over `objects/`, not a copy of it |

## What this is not

Not a font-design tutorial, not an audit of Clarendon, not a copy of the glyph's data in nicer prose. If a card and the real outline in `ClarendonLTStd.otf` ever disagree, the outline is right and the card is wrong — every numeric claim in `objects/` cites a contour point range or a font table value specifically so that check is possible.

## Territory and sourcing

- Font: Clarendon LT Std Roman (`ClarendonLTStd.otf`, Adobe), verified against a second independent Clarendon before use — see `reference/decisions.md`.
- Terminology: `typography-fundamentals` skill (glossary, counterform notes, classification reference). Two terms drafted from memory before that audit ("arch," "tail") were wrong and were replaced with the skill's actual terms ("finial," "spur").
- The diagram outlines the glyph and eleven label words as vector paths rather than embedding either Clarendon or Akzidenz-Grotesk as web fonts — both are commercial font software; only the specific letterforms used as diagram artwork are shipped, not the fonts themselves. Card body text (which is unbounded prose, not a fixed word list) uses a system CSS font stack — Helvetica Neue, falling back to Helvetica, Arial, and sans-serif — so it ships no font file either way.

Built following the sixth form described in Weekly Comp #11: The Cartographer — a system map of a real, in-force body of work, using the ICM Architect skill's invariants (github.com/RinDig/icm-architect) as scaffolding.
