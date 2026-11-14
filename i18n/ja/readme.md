# Letterform Cartographer

1 文字のシステムマップ: Clarendon LT Std ローマ文字で小文字 **a**。11 個の名詞カード - 9 つの生きたもの、1 つの残り物、1 人のゴースト - それぞれが実際のフォントの輪郭の正確な範囲を引用しています。再描画した近似ではありません。

## ライブデモ

`docs/index.html` - 文字のホバリング可能な図。各ホバリングは `objects/` から実際の `.md` カードを直接、ライブでレンダリングします。図はカードのコピーではなく、それらの上のビューアです。これを repo ルート (GitHub Pages: source = `/ (root)`, not `/docs`) から提供しますので、`docs/index.html` が `../objects/*.md` に対して相対的にフェッチすると解決します。`/docs` だけに制限されたページは、すべてのカードで 404 になります。

## なぜこれが存在するのか

グラフの外観は単なる点座標です。ボウル、カウンター、スパーはそのデータの範囲の周りに人間が描いた名前です。フォントファイル自体にラベルはありません。このリポは、一度行われたラベル化で、実際に抽出された外観 (`fontTools`) とロードされたタイプグラフィック参照スキルの両方を引用します。だから、誰も目で再導出する必要はありません。

## 1人の幽霊は 前から説明してる

Clarendon はスラブセリフであり、それが初めて知られたことであり、しばしば唯一のことである。そしてそれは自信的で間違った期待を生み出します。表面の全てのストロークが括弧付きのスラブフットで終わります。この小文字 `a` はそうではありません。そのステムは曲線状の突起で終わり、そのフィニアルはボール端子で終わっていて、フットセリフは文字のどこにも存在しません。これは単純化や芸術的な選択ではなく、実際の輪郭に関する事実です。最初の抽出は、この README が期待しないと言ったセリフが欠けているために破損していると考えられた後、2 つ目の独立した ZQX 1 と比較して確認されました。詳細については [`objects/foot-serif.md`](objects/foot-serif.md) を参照してください。

## 見知らぬ人やコールドAIセッションが これをどう使うか

1. `identity.md`と`rules.md`を一度読め 短い
2. `examples.md`を開けて 11の部品と 3つの短い歩行のカタログを
3. `objects/`でカードを開けて ここで止めろ
4. カタログにない名前を見つけましたか？（「アーチ」「テール」） まずは `reference/naming-collisions.md` をチェックしてください。おそらく既に答えられています。

**The one rule: load the catalog, then one card. Never all eleven at once.**

## ここに何がある？

| パス | ジョブ |
| --- | --- |
| `identity.md` | 誰が地図を作ったのか 誰の領土なのか 後の読者は誰なのか |
| `rules.md` | 何が名詞であるか、どうやって生/残り/ゴーストを決めるか、ヒット/ヒットしないルール |
| `examples.md` | 目録表+3歩行、2026年8月21日付 |
| `objects/` | 11枚のカード自体は 実際の棚です |
| `reference/card-types.md` | この地域で使われている3種類のカードの形状 |
| `reference/naming-collisions.md` | 4つの実際の語彙トラップを一度に書き下ろす |
| `reference/decisions.md` | 判断（フォント選択、用語修正、レンダリング技術）を記録し、その理由を示した。 |
| `docs/index.html` | ライブダイアグラム - `objects/` 上のビューアであり、コピーではありません |

## これが何でないか

フォントデザインのチュートリアルではなく、 Clarendon の監査でもなく、より素晴らしい文法でグリフのデータのコピーでもありません。カードと `ClarendonLTStd.otf` の実際の輪郭が一致しない場合、輪郭は正しくカードは間違っています。`objects/` のすべての数値的な主張は、チェックが可能なように輪郭点の範囲またはフォントテーブルの値を特に引用します。

## 地域とソース

- Font: Clarendon LT Std Roman (`ClarendonLTStd.otf`, Adobe), verified against a second independent Clarendon before use — see `reference/decisions.md`.
- Terminology: `typography-fundamentals` skill (glossary, counterform notes, classification reference). Two terms drafted from memory before that audit (“arch,” “tail”) were wrong and were replaced with the skill's actual terms (“finial,” “spur”).
- この図は、Clarendonや Akzidenz-Groteskをウェブフォントとして埋め込む代わりに、グリフと11のラベルワードをベクトルパスとして描画しています。どちらも商用フォントソフトウェアで、図のアートワークとして使用される特定の文字形だけが送られます。フォント自体は送られません。カードの本体テキスト（固定された単語リストではなく、無制限の散文）は、システムCSSフォントスタックであるHelvetica Neueを使用しています。Helvetica、Arial、sans-serifに戻ってきます。だから、どちらの方法でもフォントファイルは送られないのです。

Weekly Comp #11に記述された第6の形式に従って構築された: The Cartographer - 実際の実施中の仕事のシステムマップで、ICM Architectスキルの不変量（github.com/RinDig/icm-architect）を支柱として使用する。
