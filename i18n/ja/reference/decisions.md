## 決定

`icm-md-writer` の決定記録形式に従ってログされるため、後のセッションで再論証もしくは無声に呼び出しを逆転させない。

---

**Decision:** Map Clarendon LT Std (`ClarendonLTStd.otf`, Adobe), not Ringold (`Ringold-Clarendon`, Bijou Type).

**Context:** Adobe Fonts returned two “Clarendon” matches. Ringold is a 2020s Bijou Type design by Dan Rhatigan with a style cut named “Clarendon”; Clarendon URW / Clarendon LT Std are digitizations of the original 1845 Fann Street Foundry design.

**Options considered:** Ringold (available, contemporary reinterpretation), Clarendon URW (Adobe Fonts, faithful digitization), Clarendon LT Std (found locally, same lineage as URW's source).

**Rationale:** The brief was “the classic slab serif” — the historical original, not a contemporary typeface that borrowed its name for one cut. Clarendon LT Std was confirmed on the user's own machine and verified against a second independent source (SuperClarendon) before use.

**Consequences:** `objects/` のカードはすべて `ClarendonLTStd.otf` を特に引用しています。 Ringold の輪郭から作成したカードは一致しません - 形状が異なります（これをテストしました：Ringoldの小文字 a は一般的な二階建てパターンに従いますが、端子の幾何学的形状は同じではありません）。

---

**Decision:** Rename “Arch” → **Finial**, “Tail” → **Spur**.

**Context:** どちらのカードも、まず一般的な印刷技術から草案され、それからロードされた`typography-fundamentals`スキルの`glossary.md`に対してオーディットされた。

**Options considered:** 「アーチ」と「テール」を保持するか，スキル自身の定義した用語に切り替える。

**Rationale:** `glossary.md` does not define “Arch” at all. It defines **Finial** — “an ornamental terminal stroke at the top of characters such as *a* and *f*” — explicitly for this letter. It defines **Tail** only for Q, K, R, and g's loop, not for *a*; it defines **Spur** as “the terminal to the stem of a rounded letter,” which is the correct fit. `rules.md` for this territory says a card must cite grounded terminology, not memory — using “Arch” and “Tail” would have violated this map's own rule.

**Consequences:** `reference/naming-collisions.md` documents both swaps as the collision a reader is likely to hit first, since “arch” and “tail” are the words most people reach for by analogy to *n*/*m*/*h* and *g*/*Q* respectively.

---

**Decision:** 実際の輪郭の点内多角形スキャンから，眼で置かれた境界箱を置き換えて，幹と終端領域を再導出した。

**Context:** Building the live diagram surfaced that `stem`'s hover region (`x: 428, y: 52, w: 145, h: 306`) mostly covered background, not ink — its anchor and clip rectangle had been eyeballed from the earlier text-only coordinate walk rather than checked against the actual filled shape. A systematic scan (`fontTools` outline, ray-casting point-in-polygon, counter treated as a hole) found the stem's real ink at mid-height spans only x=302–440, not the x=428–573 range the original card used — the card had conflated the glyph's overall right bound (556, which belongs to the spur) with the stem's own edge.

**Options considered:** １枚のカードを孤立にパッチするか，または同じ方法で各ストロークカードのアンカーと領域を再スキャンする。

**Rationale:** 手で置いた領域の一つが間違っていた場合、他の領域も同じように作成され、ユーザが偶然気づいた領域だけでなく、同じチェックを受ける。5 つのストロークアンカーはすべてポリゴン内点で再検証されました。4 つ（ボウル、フィニアル、ボール端子、スパー）は既に実際のインク上に置かれていますが、フィニアルの領域の長方形は実際の インク比率に合わせて締め付けられました（~52% vs. ステムの元の ~0%）。長方形では曲線ストロークを完璧に結びつけることはできません。フィニアルとボウルは正しくフィットしても、インク覆い率が 50% 近くに到達します。その原因は、凹面が必ずしも背景を引っ張るからです。これは曲線文字形の直線クリップに対して予想されるものであり、欠陥ではありません。

**Consequences:** `objects/stem.md` and `objects/finial.md` were rewritten with corrected `anchor`/`region` frontmatter and corrected prose (the old stem card's claim that its right edge reached x=556 was wrong and is called out in the card itself rather than silently fixed).

---

**Decision:** Cap `stem`'s region at y≥165 and `spur`'s at y≤165, instead of letting both run through y=60–165.

**Context:** The corrected stem region above still spanned y=60–355, which overlaps `spur`'s region (y=−22–190) across x=332–440 — the exact band where the spur's curl lifts off the stem's base. Hotspots are layered in DOM order, so within that overlap `spur`'s hotspot (added later) always won, making `stem` unreachable by hover in its lower third even though its region rectangle was, on paper, mostly on-ink.

**Options considered:** ステムペイントが最後になるようにDOMを再配列する（原因ではなく症状を修正する -- どの部分が到達不能になるかを反転するだけ）、ある領域を任意に縮小する、2つのストロークのインクが分離する実際の点でy領域を分割する。

**Rationale:** The segment scan (`reference/decisions.md`'s earlier entry) shows the spur's ink exists as an isolated island separate from the stem only below y≈165; above that, only the stem's own segment continues. Splitting the two regions at y=165 removes the overlap entirely rather than papering over it with z-order.

**Consequences:** `objects/stem.md` region height shrank to 185 (y:165–350); `objects/spur.md` region height shrank to 187 (y:−22–165). Both anchors re-verified on-ink after the change.

---

**Decision:** Highlight rendering switched from a hard `clip-path` to a blurred `mask` (feGaussianBlur, stdDeviation 16) for every rect/circle region.

**Context:** Once the highlights were actually visible (previous entry), the boundary itself was still wrong in a different way: a region's straight edge frequently has no anatomical meaning — it exists only to stop the highlight from bleeding into a neighbouring part (e.g. the stem/spur split at y=165, which sits mid-curve on a single unbroken vertical stroke with no real joint there). A hard clip made that arbitrary cut look like a rectangle had been pasted over the letter, most visibly on `spur`, whose highlight had a flat horizontal top slicing straight across the curl.

**Options considered:** (1) フォントの実際のベジエコマンドから真のサブパスを手動で追跡し、すべての境界が実際のインクに従うようにする。これは原始パスデータと直接比較して調べました。いくつかの部分（特にボール端末の螺旋）が自分自身の上に二重になり、視覚的に確認するのが難しいギャップや自己交差を導入する危険性があるため、クリアな点指数カットに戻せないので、今のところ拒否されています。 (2) 直線ではなく楕円形 - 曲線部分では直線より良いが、任意のハードエッジです。 (3) ハードクリップではなくソフトマスク。

**Rationale:** マスクは実際のシルエットに到達する前に完全に不透明になり、人工境界の近くの不透明度を減らすだけです。これは「この正確な長方形」ではなく、「このストロークの一般的な面積」と読みます。境界は実際に測定された事実ではなく、判断の結果です。前のエントリのカウンターパンチ技術は影響されません。アクセントフィルと背景色のパンチは同じマスクを共有します。つまり、カウンターの真のエッジは全体的に鮮明に保たれます。DOM検査だけでなく、直接の視覚的ズームで確認できます。

**Consequences:** `defs` はストロークカードごとに共有された `<filter id="soft-edge">` と `<mask>` を発生させます (旧 `<clipPath>` を置き換えます)。`fillPath`/`punch` は `clip-path` の代わりに `mask="url(#mask-ID)"` を使用します。カードの内容は変更されません。これは純粋なレンダリング技術であり、どの領域のスコープを変更するのではありません。

---

**Decision:** Replace the blurred mask (previous entry) with a hard-edged `ellipse` clip for `bowl`, `finial`, and `spur`; `stem` stays a literal `rect`.

**Context:** ブラーは「明白な長方形」の問題を解決したが、新しい問題を導入した。柔らかく不透明なグローは不正確に読み取られ、図の残りの鮮明で平坦な色言語（ソリッドClarendonフィル、ソリッドAkzidenzラベル、ハードエッジカウンターカットアウト）と衝突する。ツールを*少し*精度低下させて「正確でない」を解決することは間違った取引であった。

**Options considered:** より小さなぼかし半径（まだソフトで、少ないだけ）、フォントの実際のベジエコマンドから手で追跡した真のサブパス（上記のエントリで調査され拒否された - ボール端末の螺旋はクリーンカットに縮小されない）、軸に並べた長方形よりもカーブストロークに適したハードエッジ形状。

**Rationale:** A rectangle has flat sides, so any edge that crosses a stroke does so as a dead-straight cut — the artifact that made `spur` look like a box. An ellipse has no flat sides: wherever its boundary crosses the stroke, it does so at an angle, which reads as a rounded, deliberate highlight rather than a pasted-on shape, while staying exactly as hard-edged and “measured” as the rest of the diagram. `stem` is excluded because it's genuinely a straight vertical stroke — a rect is the anatomically correct shape there, not a compromise.

**Consequences:** `objects/bowl.md`, `objects/finial.md`, `objects/spur.md` frontmatter changed `region.shape` from `rect` to `ellipse` (same `x`/`y`/`w`/`h` — now read as an ellipse's bounding box, `cx`/`cy` at its center, `rx`/`ry` at half its width/height). `docs/index.html` gained a shared `regionShapeEl(r)` helper so the clip-path defs, the highlight fill/punch, and the hotspot all build the identical rect/circle/ellipse from one place instead of three separately-maintained branches — the kind of duplication that let the coordinate-space bug (two entries up) go unnoticed as long as it did. The blur filter and per-card masks were removed entirely.

---

**Decision:** Pull `stem`'s left edge in from x=320 to x=328, narrowing its region from 120 to 112 wide.

**Context:** `stem` の領域と `counter` の境界 (x=157–323) は 3 単位 (320-323) で重なり合っています。カウンターパンチ (上の 2 項目) は既にソリッドフィルがカウンターの真の穴の上を描画することを防いでいるので、これは色精度のバグではありません。しかし、丸みを帯びた直角の角が曲線の穴をほとんど擦る 3 ユニットのスライバーは、近くで視覚的に不安定なように読み取られるような不正確なものであり、そのようにフラグされています。

**Rationale:** `stem` と `counter` は本当に解剖学的に境界を共有しています - `objects/stem.md` のヒットラインがそう言っています（「ステムの左端はカウンターの右壁でもあります」）。 この修正はその隣接性を否定するのではなく、それを近接ミスとしてレンダリングすることを止めるだけです。引き込み境界 (x=328, w=112) でインク比率チェックを再実行すると、 100% のインク覆いが見つかりました。これは元の 120 幅領域の 92% よりも厳しい値です。この高さでトリミングされている 3 個のユニットはいずれも固体ステムインクではありません。

**Consequences:** `objects/stem.md` 領域の幅を 120→112, x 320→328 に変更しました。アンカー (380,210) はインク上で再確認しました。文字の変更は必要ありません。カードの引用したインク範囲 (x=324–440 から y=210) はすでに正確です。レンダリング領域のみ、意図的に保守的なサブセットが移動しました。
