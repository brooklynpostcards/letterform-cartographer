# Letterform Cartographer

A system map of one glyph: the lowercase **a** in Clarendon LT Std Roman. Eleven noun cards — nine live, one leftover, one ghost — each citing an exact range of the real font outline, not a redrawn approximation of it.

## 现场演示

`docs/index.html` — — 这个字母的一个可悬浮图。 每个悬浮都从 `objects/` 直接从这个存储库中提取和渲染实际的 `.md` 卡片。 图中的任何东西都不是这些卡片的副本,而是它们的查看器。 从存储库根目录(GitHub Pages: source = `/ (root)`, not `/docs`)提供它,因此 `../objects/*.md` 的相对提取解决了 — — 仅限于 ZQX7 的页面在每张卡片上都会出现 404。

## 为什么这种情况存在

“碗 ” 、 “计数器”和“刺”是人类围绕这些数据范围绘制的名称 — — 字体文件中没有任何东西会自行标记。 这个存储库就是这种标记,只要完成一次,就可以根据真正提取的轮廓(`fontTools`)和加载的印刷参考技巧引用,所以没有人需要用眼睛重新导出它。

## 一个鬼,解释在前面

Clarendon is a slab serif — that's the first and often only thing anyone knows about it, and it creates a confident, wrong expectation: that every stroke in the face ends in a bracketed slab foot. This lowercase `a` doesn't. Its stem ends in a curved spur, its finial ends in a ball terminal, and no foot serif exists anywhere on the letter. That's not a simplification or an artistic choice being described loosely — it's a fact about the actual outline, verified against a second independent Clarendon after the first extraction was nearly discarded as corrupt for lacking the very serif this README just told you not to expect. See [`objects/foot-serif.md`](objects/foot-serif.md) for the full account.

## 一个陌生人 — — 或一个冷人工智能会话 — — 如何使用这个

1. 读一下`identity.md`和`rules.md`，它们很短
2. 打开 `examples.md`,它是一个目录表,包含所有 11 个零件加上 3 个短暂的工作步骤。
3. 需要一个部件? 在`objects/`中打开相应的卡片,停在那里。
4. 遇到一个不在目录中的名字 ( “ 拱 ”, “尾 ” )? 首先检查`reference/naming-collisions.md` — 它很可能已经被回答。

**The one rule: load the catalog, then one card. Never all eleven at once.**

## 这里有什么

| 路径 | 約伯 |
| --- | --- |
| `identity.md` | 谁是制图师,这是谁的领土,谁是后来的读者 |
| `rules.md` | 这里的名词是什么,如何决定活/剩余/鬼,命中/不命中规则 |
| `examples.md` | 目录表+三个工作步行,日期2026-08-21 |
| `objects/` | 十一张卡本身的实际货架 |
| `reference/card-types.md` | 这个领土使用的三张牌形状 |
| `reference/naming-collisions.md` | 四个真正的词汇陷阱,写下来一次 |
| `reference/decisions.md` | 记录的决定(字体选择;术语更正;渲染技术)及其理由 |
| `docs/index.html` | 实时图—一个查看器在`objects/`,而不是它的副本 |

## 这不是什么

不是字体设计教程,也不是对Clarendon的审计,也不是以更加简洁的语言复制字符的数据。 如果某张卡片和`ClarendonLTStd.otf`中的实际轮廓不一致,那么轮廓是正确的,而卡片是错误的 — — `objects/`中的每个数值声明都引用了一个等高线点范围或字体表值,这样就可以进行检查。

## 领土和来源

- 字体: Clarendon LT Std Roman (`ClarendonLTStd.otf`, Adobe ), 使用前与第二个独立的 Clarendon 进行验证 — 见 `reference/decisions.md`。
- 术语:`typography-fundamentals`技能(词汇表、对照表注释、分类参考 ) 。 在审核之前从记忆中草拟的两个术语( “拱 ” 、 “尾 ” ) 是错误的,并被该技能的实际术语取代( “终结 ” 、”刺激 ” ) 。
- 该图将字符和11个标签字作为矢量路径,而不是嵌入Clarendon或Akzidenz-Grotesk作为网页字体 — — 两者都是商业字体软件;只有用作图画的特定字体才会发送,而不是字体本身。 卡片正文(无限散文,而不是固定的字词列表)使用系统CSS字体堆栈 — — Helvetica Neue,回归到 Helvetica、Arial 和无衬线体 — — 因此它不会发送字体文件。

按照 Weekly Comp #11 中描述的第六种形式构建: The Cartographer — 一个真实、有效的工作体的系统地图,使用 ICM Architect 技能的不变量 (github.com/RinDig/icm-architect) 作为脚手架。
