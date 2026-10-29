# Town Pack — 町・家・バーの背景とバーの環境音

Town Pack は、小さな町を舞台にした物語のための完成済み背景素材です。描かれた背景3枚——町の入口の街角、家の玄関、夜のバー——と、バーの環境音ループを収録しています。物語・シーン・キャラクターは含まないので、どこで画像を見せるかはゲームが決めます。

内蔵の2つのゲームがすでにこのセットを共用しています。**Cthangover** は町の入口と玄関を、**My Novel** テンプレートは3枚の背景とバーの環境音をすべて使います。どちらのゲームも同じファイルをこの mod から読み込むため、Town Pack 側の修正や画質向上は両方に届きます。

## 収録内容

町の入口 `town/town_entry`：縞模様の日除けがかかった店々が並ぶ、石畳の街角です。

![町の入口の背景：石畳の街角に立つ、緑と白の日除けがついた角建物。](assets/town_entry.jpg)

家の玄関 `home/vestibule`：階段、肘掛け椅子、額絵のあるホールです。

![玄関の背景：暖かな光のホールに、木の階段、肘掛け椅子、ベンチ、額装された絵。](assets/vestibule.jpg)

バー `bar/bar`：提灯の灯るテーブル、カウンター、瓶の棚です。

![バーの背景：梁の見える天井の下、提灯に照らされたテーブル、カウンター、瓶の棚。](assets/bar.jpg)

バーの環境音 `bar/bar_ambient`：Ambience サウンドチャネル用の、バーの雰囲気を収めた Ogg Vorbis ループです。

3枚の画像はいずれも 1920 × 1024 です。それぞれに、同じ名前に `_depth` という接尾辞を付けたグレーの対応ファイルがあります：

![町の入口の深度マップ：同じ構図のグレースケール版。](assets/town_entry_depth.jpg)

深度画像を直接目にすることはありません。背景を表示するとき、ゲームは `<name>_depth` も読み込み、ライティングシステムに渡します。システムはこれを使って、シーンの上に置かれた光を計算します。深度画像のない背景も、普通に表示されます。

## どこで見られるか

- **Cthangover:** `town_entry` シーン（町の入口）と `home_vestibule` シーン。
- **My Novel テンプレート:** `my_novel_town`、`my_novel_home`、`my_novel_bar`。バーのシーンでは `bar/bar_ambient` も鳴ります。

同じ町の入口が、My Novel テンプレートでは物語の一行とともにゲームの幕を開けます：

![My Novel の最初のシーン：町の入口の背景に「夕暮れの町。街灯はもうともり、石畳を涼しい風が吹き抜けていく」の一文。](assets/reuse-my-novel.jpg)

そして Cthangover では、同じ絵の上を別の物語が自分の選択肢で彩ります：

![Cthangover の町の入口：同じ背景に「家に帰る」と「路地を調べる」の選択肢。](assets/reuse-cthangover.jpg)

Town Pack は両方のゲームのコレクションに含まれ、一緒に読み込まれます。インストールしても、ほかのゲームにこれらの場所が追加されるわけではありません。背景を使うのは、ゲーム自身のシーンです。

## 自分のゲームで使う

1. 自分のコンテンツ mod の `depends` リストに `town_pack>=1` を追加します。
2. ゲームのコレクションに `town_pack>=1` を加えます。My Novel テンプレートの **Assets** ブロックがその例です。
3. リソースは下記の名前で参照します。名前は `backgrounds/` と `sounds/` からの相対で、拡張子は付きません。

```jsonc
// mods/my_game/manifest.json — 既存のリストに追加
"depends": ["town_pack>=1"]
```

テンプレートの `my_novel_bar` シーンから取った、バーを表示して環境音を鳴らすシーンです：

```json
{
  "name": "my_bar",
  "defaultBackground": "bar/bar",
  "defaultAmbient": "bar/bar_ambient"
}
```

シナリオは会話の途中で絵を切り替えることもできます：

```scenario
background town/town_entry
text "こんな時間、通りはひっそりとしている。"
```

使える名前は次のとおりです：

```text
town/town_entry     backgrounds/town/town_entry.png
home/vestibule      backgrounds/home/vestibule.png
bar/bar             backgrounds/bar/bar.png
bar/bar_ambient     sounds/bar/bar_ambient.ogg
```

## 自分のゲーム向けに画像を差し替える

Town Pack を編集せずに画像を差し替えるには、自分の mod に同じ相対名のファイル（例：`backgrounds/bar/bar.png`）を置き、その `depends` に `town_pack>=1` と書きます。所有者に依存する mod は後から読み込まれ、そちらが優先されます。背景を差し替えるときは、同名の `_depth` ファイルも一緒に置いてください。そうしないと Town Pack の元の深度画像がそのまま見つかり、光が古い絵の構図に合わせて落ちてしまいます。

依存関係がなければ、同じ名前を置く2つの mod の優先順位は未定義です。この問題はリソースマップツールがエラーとして報告します。

## うまく表示されないとき

1. 背景が真っ黒、または表示されない場合は、名前の打ち間違いがまず疑わしいです。名前は大文字小文字を区別し、区切りは `/` です。
2. Town Pack がインストールされているだけでなく、起動したゲームに含まれているか確認してください。
3. バーの音が鳴らない：シーンの `defaultAmbient` が `bar/bar_ambient` になっているか、**Settings → Sound** で **Ambience** が有効か確認してください。音の再生は Audio Engine mod が担います。
