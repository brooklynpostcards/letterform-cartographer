## 决定

根据 `icm-md-writer` 的 Decision Record 形状进行记录 — 这样后续会话就不会重新论证或无声地逆转任何调用。

---

**Decision:** Map Clarendon LT Std (`ClarendonLTStd.otf`, Adobe), not Ringold (`Ringold-Clarendon`, Bijou Type).

**Context:** Adobe Fonts返回了两个“Clarendon”匹配。 Ringold是Dan Rhatigan在20世纪20年代设计的Bijou Type,其风格切割名为“ZQx5 ” ; Clarendon URW / Clarendon LT Std是1845年Fann Street Foundry原始设计的数字化版本。

**Options considered:** Ringold(可用,当代重新解释 ), Clarendon URW(Adobe Fonts,忠实数字化 ) 、 Clarendon LT Std(本地发现,与URW的源相同 ) 。

**Rationale:** Clarendon LT Std在用户自己的计算机上进行了确认,并在使用之前与第二个独立来源(SuperClarendon)进行了验证,这样用户就能够在使用过程中选择最适合自己的字体。

**Consequences:** Every card in `objects/` cites `ClarendonLTStd.otf` specifically. A card built from Ringold's outline would not match — the shapes differ (this was tested: Ringold's lowercase a follows the general double-storey pattern but its terminal geometry is not identical).

---

**Decision:** 重新命名“拱门”→**Finial**,“尾巴”→ **Spur**。

**Context:** 这两张牌首先是从一般的印刷知识起草的,然后对照加载的`typography-fundamentals`技能的 `glossary.md` — — 整个地图应该基于的源代码进行审核。

**Options considered:** 保留“拱门”和“尾巴 ” ( 常见的术语,可以说对于普通读者来说更清楚)相对于切换到技能自定义的术语。

**Rationale:** `glossary.md` 根本没有定义“拱 ”, 它明确地为这个字母定义了 **Finial** — “ 在 *a* 和 *f* 等字符的顶部的装饰性终端线 ” ; 它只为 Q、K、R 和 g 的循环定义 **Tail**,而不是为 *a* 定义;它将 **Spur** 定义为“圆形字母的末尾 ”, 这是正确的匹配。 对于这一领域,`rules.md` 规定卡片必须引用基础术语,而不是记忆 — — 使用“拱”和“尾巴”会违反本地图自己的规则。

**Consequences:** `reference/naming-collisions.md` 将两种交换作为读者可能首先碰到的碰撞记录下来,因为 “arch” 和 “tail” 是大多数人分别通过类比 *n*/*m*/*h* 和 *g*/*Q* 来使用的词。

---

**Decision:** 从实际轮廓的多边形点扫描中重新导出干部和末端区域,替换通过眼睛放置的边界框。

**Context:** Building the live diagram surfaced that `stem`'s hover region (`x: 428, y: 52, w: 145, h: 306`) mostly covered background, not ink — its anchor and clip rectangle had been eyeballed from the earlier text-only coordinate walk rather than checked against the actual filled shape. A systematic scan (`fontTools` outline, ray-casting point-in-polygon, counter treated as a hole) found the stem's real ink at mid-height spans only x=302–440, not the x=428–573 range the original card used — the card had conflated the glyph's overall right bound (556, which belongs to the spur) with the stem's own edge.

**Options considered:** 单独修补一张卡片,而不是使用相同的方法重新扫描每张笔画卡片的锚点和区域。

**Rationale:** 如果一个手动放置的区域是错误的,那么其他区域也会以同样的方式构建,并且需要进行相同的检查,而不仅仅是用户偶然注意到的区域。 所有五个笔画锚点都通过多边形中的点重新验证;四个(碗、端子、球端子、刺)已经放在真正的墨水上,但端子的区域矩形被拉紧以匹配其实际墨水比例(~52% vs. stem的原始~0 % ) 。 矩形不能完美地绑定曲线笔画 — 即使正确配合,端子和碗都接近50%的墨水覆盖率,因为它们的凹面必然会拉入一些背景。

**Consequences:** `objects/stem.md` 和 `objects/finial.md` 被重写,修正了 `anchor`/`region` 的前端材料和修正了文体(旧主卡声称其右边缘达到 x=556 是错误的,并在卡本身中调用而不是默认修复 ) 。

---

**Decision:** Cap `stem`'s region at y≥165 and `spur`'s at y≤165, instead of letting both run through y=60–165.

**Context:** 上面的经过校正的干部区域仍然跨越y=60–355,,它与`spur`的区域(y=−22–190)重叠,横跨x=332–440 — — 即尖端卷曲从干部基部升起的确切带状区域。 热点按照DOM顺序层叠,因此在这一重叠中,`stem`的热点(后来添加的)总是获胜,使得ZQX4无法通过悬停在其下三分之一处到达,即使其区域矩形在纸上大多是墨水上。

**Options considered:** 重新排列 DOM 以便最后使用主干绘图(修复症状,而不是原因 — — 只是翻转哪个部分变得无法触及 ) ; 任意收缩一个区域;在两笔墨水分开的实际点分割 y 范围。

**Rationale:** 区段扫描(`reference/decisions.md` 的早期条目)显示,在 y≈165 以下,刺的墨水作为一个孤立的岛屿存在,与茎分离;在此之上,只有茎的区段继续存在。 在 y=165 分割两个区域可以完全消除重叠,而不是用 z 序来覆盖它。

**Consequences:** `objects/stem.md` 区域高度缩小到 185 (y:165–350 ) ; `objects/spur.md` 区域的高度缩减到 197 (y:−22–165 ) 。 两个锚点在更改后重新验证了墨水。

---

**Decision:** 对于每个矩形/圆形区域,高亮渲染从硬 `clip-path` 切换到模糊的 `mask`(feGaussianBlur, stdDeviation 16 ) 。

**Context:** 一旦亮点实际可见(上一条目 ), 边界本身仍然在另一种方式上是错误的:一个区域的直线边缘通常没有解剖学意义 — — 它仅仅存在于阻止亮点流入邻近部分(例如y=165,的茎/刺分裂位于曲线中间的一个连续的垂直线上,没有真正的关节 ) 。 一个硬夹使任意切割看起来像是粘贴在字母上面的矩形,最明显的是`spur`,其亮点有一个平坦的水平顶部直接切割穿过卷曲。

**Options considered:** (1) 从字体的实际贝塞尔命令手动追踪真正的子路径,以便每个边界都跟随真正的墨水 — 直接对照原始路径数据进行调查;目前被拒绝,因为一些部分(特别是球端螺旋)在自身上重叠,这种方式不能减少到清洁的点索引切割,而不会引入真正的风险或难以视觉验证的自交叉。 (2) 椭圆而不是直线 — 在曲线部分上比直线更好,仍然是一个任意的硬边缘。 (3) 软蒙版而不是硬剪辑。

**Rationale:** 带有模糊的矩形/圆形的蒙版将保持每个 * 真实 * 墨水边缘与之前一样清晰 — — 蒙版在达到真实轮廓之前就已处于完全不透明状态 — — 并且只在人工边界本身附近减少不透明度,因为在这里没有真正的边缘需要保留。 这看起来像是“这笔画的一般面积 ”, 而不是“这个确切的矩形 ”, 因为边界实际上是一种判断,而不是测量的事实。 上一条目中的反冲技术不受影响:重点填充和背景颜色冲印共享相同的蒙版,因此反冲器本身的真实边缘始终保持清晰,通过直接视觉缩放确认,而不仅仅是 DOM 检查。

**Consequences:** `defs` 现在每张动作卡发出一个共享的 `<filter id="soft-edge">` 和一个 `<mask>` (取代了旧的每张卡 `<clipPath>` ) ; `fillPath`/`punch` 使用 `mask="url(#mask-ID)"` 而不是 `clip-path`。 没有改变卡片内容 — 这纯粹是渲染技术,而不是任何区域的重新范围化。

---

**Decision:** 用硬边缘 `ellipse` 剪辑替换模糊蒙版(上一个条目 ), 用于 `bowl`、`finial` 和 `spur`;`stem` 仍然是字面上的 `rect`。

**Context:** 模糊修复了“显而易见的矩形”问题,但引入了一个新的问题 — — 柔和、模糊的发光看起来不准确,并且与图表中清晰、平坦的颜色语言(实心 Clarendon 填充、实心 Akzidenz 标签、硬边缘计数器切割)的其余部分发生冲突。

**Options considered:** 更小的模糊半径(仍然柔软,只是少了一些 ) ; 从字体的真正贝塞尔命令手动追踪真正的子路径(在上面的条目中进行了调查并被拒绝 — — 球端螺旋不会减少到干净的切割 ) ； 硬边形状比轴对齐矩形更适合于曲线笔画。

**Rationale:** 矩形有平面边,因此任何边界交叉的线条是直线切割 — — 这种人工制品使得`spur`看起来像一个方框。 椭圆没有平面边:无论其边界在哪里交叉线条,它都在一个角度上,这样看起来就像一个圆形,故意突出,而不是粘贴的形状,同时保持与图中其他部分一样的硬边缘和“测量 ” 。 `stem`被排除在外,因为它是真正的直线垂直线条 — — 直线是解剖学上正确的形状而不是妥协。

**Consequences:** `objects/bowl.md`, `objects/finial.md`, `objects/spur.md` frontmatter changed `region.shape` from `rect` to `ellipse` (same `x`/`y`/`w`/`h` — now read as an ellipse's bounding box, `cx`/`cy` at its center, `rx`/`ry` at half its width/height). `docs/index.html` gained a shared `regionShapeEl(r)` helper so the clip-path defs, the highlight fill/punch, and the hotspot all build the identical rect/circle/ellipse from one place instead of three separately-maintained branches — the kind of duplication that let the coordinate-space bug (two entries up) go unnoticed as long as it did. The blur filter and per-card masks were removed entirely.

---

**Decision:** 将 `stem` 的左边缘从 x=320 拉入到 x=328,,从而缩小其区域的宽度从 120 到 112。

**Context:** `stem` 的区域和 `counter` 的边界 (x=157–323) 重叠了 3 个单位 (320–323 ) 。 反冲孔(上面两个条目)已经防止实体填充在反冲孔的真正孔洞上绘制,因此这从来不是颜色准确性错误 — — 但一个圆直角几乎擦过一个弯孔的 3 单位片段正是那种近距离看起来视觉上不稳定的不准确性,并且被标记为这样。

**Rationale:** `stem` 和 `counter` 在解剖学上确实有一个共同的边界 — `objects/stem.md` 自己的 Hits 行说明了这一点 ( “ 茎的左边缘也是计数器的右壁 ” ) 。 修复方法不是否认这种毗邻关系,而是停止将其渲染为近似错误。 在拉入边界(x=328, w=112)上重新运行油墨比例检查发现 100% 的油墨覆盖率,比原始 120 宽区域的 92% 更紧。

**Consequences:** `objects/stem.md` 区域宽度改变为 120→112, x 320→328。 Anchor (380,210) 重新确认了墨水上。 无需文字更改 — — 卡片引用的墨水范围(x=324–440 到 y=210)已经准确;只有渲染区域,其故意保守的子集,被移动。
