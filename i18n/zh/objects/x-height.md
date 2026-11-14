---
id: x-height
name: x-height
type: metric
status: live
anchor: [600, 468]
region: {shape: metric, y: 468}
---

# x高度

**What it is** — 468 个 1000 的单位。 小写字母构建的行,以及在给定点大小下最能决定文本面是大还是小的单个数字。

**Status** — 引用：`OS/2.sxHeight = 468`和`ClarendonLTStd.otf`。

**Hits** — 字体中的每个小写字母都要一次改变。 这是地图上最昂贵的数字,也是唯一一个爆破半径完全离开这个字母的数字。

**Does not hit** — 这个字符的实际测量高度。 a 的顶点为 483,而不是 468。 这一间隙是故意的,并且在 [overshoot](overshoot.md) 处单独映射。
