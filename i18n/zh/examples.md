## 工作映射 — Clarendon 小写 `a`

领土:一个符号,`ClarendonLTStd.otf`,引用于2026-08-21。 十一张牌存放在[`objects/`](objects/) — — 这个文件是目录,而不是复制。 术语对照`typography-fundamentals`技能词汇表进行了审核;两个从记忆中草拟的术语(“arch ” 、 “tail ” ) 错误并被替换 — — 见[`reference/decisions.md`](reference/decisions.md)。

### 目录

| 部分 | 类型 | 现状 | 卡片 |
| ------------- | --------------- | ----------------- | -------------------------------------------------------- |
| 茎 | 中风 | 生命 | [`objects/stem.md`](objects/stem.md)                      |
| 碗 | 中风 | 生命 | [`objects/bowl.md`](objects/bowl.md)                      |
| 菲尼亚尔 | 中风 | 生命 | [`objects/finial.md`](objects/finial.md)                  |
| 球端子 | 行程结束 | 生命 | [`objects/ball-terminal.md`](objects/ball-terminal.md)    |
| 軌跡 | 行程结束 | 生命 | [`objects/spur.md`](objects/spur.md)                      |
| 计数器 | 負空間 | 活的，衍生的 | [`objects/counter.md`](objects/counter.md)                |
| 光圈 | 負空間 | 活的，衍生的 | [`objects/aperture.md`](objects/aperture.md)              |
| x高度 | 公制 | 生命 | [`objects/x-height.md`](objects/x-height.md)              |
| 基线 | 公制 | 生命 | [`objects/baseline.md`](objects/baseline.md)              |
| 超速 | 更正 | 剩余 | [`objects/overshoot.md`](objects/overshoot.md)            |
| 脚衬线体 | 中风 | 👻鬼 | [`objects/foot-serif.md`](objects/foot-serif.md)          |

冷读取器在此停止,除非某个部分需要打开。

### 一次步行,全部

*问题 : " 我想给这个 Clarendon `a` 一个更重的板脚,以配合面部的其余部分,这是什么触摸? " *

1. 打开上面的目录。 “Foot serif”是显而易见的门。
2. 打开`objects/foot-serif.md`,在正文的第一行中显示:此字符没有脚衬线体。 状态:**ghost**。
3. 停止。 问题的前提是错误的 — — 没有现存的脚塞里夫字体可以加重。 卡片还指出了两个读者可能意味着的真正字体:[`spur`](objects/spur.md)和[`ball-terminal`](objects/ball-terminal.md),并用引用的坐标步骤解释了为什么这两个字体都不是塞里夫。

没有必要打开其他卡片来回答这个问题,这就是目录的意义所在。

### 第二次散步,更短

**Question:** “那我干的你爽不爽? ” 侯龙涛有些不解的问道。

1. 打开`objects/counter.md`
2. **Hits**: 没有直接 — 它是从`bowl`和`stem`衍生出来的。
3. **Does not hit**: 孔径,一个单独的白色形状人们通常意味着而不是。
4. 答案:不,不能单独运行。 编辑 `bowl` 或 `stem`;计数器会跟着运行。

### 第三步,关于词汇本身

**Question:** “那你打算怎么办? ”

1. 没有 `arch.md`。 目录中没有名为"Arch"的行。
2. `reference/naming-collisions.md` 给这个问题命名,并指向 [`objects/finial.md`](objects/finial.md) — — 这个字母的技能术语,原因是 “arch” 不适用于这里(它永远不会返回到基线,所以它不是 ) 。
3. 停止,与词汇纠正,而不仅仅是几何位置。
