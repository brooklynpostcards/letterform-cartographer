## ワークマップ — Clarendon 小文字 `a`

テリトリー: 1 文字 `ClarendonLTStd.otf`, 引用 2026-08-21. 11 枚のカードが [`objects/`](objects/) に存在します - このファイルはカタログであり、コピーではありません。用語は `typography-fundamentals` スキルの用語集と比較して検証しました。記憶から作成された 2 つの用語（「アーチ」、「テール」）が間違っていたので置き換えました - [`reference/decisions.md`](reference/decisions.md) を参照してください。

### カタログ

| パート | タイプ | ステータス | カード |
| ------------- | --------------- | ----------------- | -------------------------------------------------------- |
| ステム | 脳卒中 | レベル | [`objects/stem.md`](objects/stem.md)                      |
| ボウル | 脳卒中 | レベル | [`objects/bowl.md`](objects/bowl.md)                      |
| フィニアル | 脳卒中 | レベル | [`objects/finial.md`](objects/finial.md)                  |
| ボール端子 | ストロークの終わり | レベル | [`objects/ball-terminal.md`](objects/ball-terminal.md)    |
| スプール | ストロークの終わり | レベル | [`objects/spur.md`](objects/spur.md)                      |
| カウンター | 負の空間 | ライブ・デリバティブ | [`objects/counter.md`](objects/counter.md)                |
| 開口部 | 負の空間 | ライブ・デリバティブ | [`objects/aperture.md`](objects/aperture.md)              |
| x-高さ | メトリック | レベル | [`objects/x-height.md`](objects/x-height.md)              |
| ベースライン | メトリック | レベル | [`objects/baseline.md`](objects/baseline.md)              |
| オーバーシュート | 修正 | 残り物 | [`objects/overshoot.md`](objects/overshoot.md)            |
| フットセリフ | 脳卒中 | 👻ゴースト | [`objects/foot-serif.md`](objects/foot-serif.md)          |

コールドリーダーはここで止まる。

### 1歩で全部

質問：「このClarendon `a`に重いスラブフットを付けて、顔の他の部分に合わせたい。それは何を触れるのか？」

1. 上のカタログを開くと、「フットセリフ」が明らかなドアです。
2. `objects/foot-serif.md` を開きます。テキストの最初の行に、この文字にはフットセリフがありません。状態: **ghost** と表示されます。
3. 停止。質問の前提は間違っています。より重くするためのフットセリフは存在しません。カードには、読者が意図したかもしれない2つの実際のストローク [`spur`](objects/spur.md) と [`ball-terminal`](objects/ball-terminal.md) の名前もあり、どちらもセリフではない理由を、引用された座標歩行で説明しています。

他のカードを開ける必要はない それがカタログのポイントだ

### ２回目の散歩は もっと短い

**Question:** 「カウンターって何？ 自分で大きくできるの？ 」

1. `objects/counter.md`を開けろ
2. **Hits**: `bowl`と`stem`から派生したものです
3. **Does not hit**: 「開口部」とは 別々の白い形を意味します
4. 答え: いいえ、それ自体ではありません。`bowl` または `stem` を編集します。カウンターが続きます。止めます。

### ３つ目の歩き方は、語彙そのものに関するものである。

**Question:** "このアーチの名前は？"

1. `arch.md` はありません。カタログには "Arch" という行がありません。
2. `reference/naming-collisions.md`はこの正確な質問を名付け、[`objects/finial.md`](objects/finial.md)を指す。この文字に対するスキルベースの用語であるが、ここでは「アーチ」は適用されない（ベースラインに戻らないので、アーチではない）。
3. 止まれ、言葉を修正して、幾何学的に位置づけるだけでなく。
