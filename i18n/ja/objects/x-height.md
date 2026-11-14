---
id: x-height
name: x-height
type: metric
status: live
anchor: [600, 468]
region: {shape: metric, y: 468}
---

# x-高さ

**What it is** — 1000分の468。小文字を構成する行、テキストが与えられた点サイズで大文字か小文字かを決定する単一の数値。

**Status** — ライブ。引用：`OS/2.sxHeight = 468`と`ClarendonLTStd.otf`。

**Hits** — フォントのすべての小文字文字を一度に変更します。これはこのマップで変更するには最も高価な数字であり、爆発半径がこの文字を完全に離れる唯一の数字です。

**Does not hit** — この文字は実際に測定された高さです。a は 468 ではなく 483 で頂点にあります。このギャップは意図的に [overshoot](overshoot.md) に別々にマッピングされています。
