# JavaScript Style Guide
# 目次

- ソースファイル標準
    - ファイル名
    - 改行コード
    - 文字コード
    - 特殊文字
        - 空白
        <!-- - エスケープ -->
        <!-- - 非ASCII文字 -->
<!-- - ソースファイル構造 -->
- 書式
    - カッコ
    - インデント
    - ブロックスタイル
    - 行折り返し（Line-wrapping）
    - ステートメント
    <!-- - 空行 -->
    - 空白
    - 水平整列（Horizontal alignment）


# JavaScript スタイルガイド

## はじめに
コードの読みやすさを向上させ、エンジニアがコードを迅速かつ完全に
理解できるようにすることを目的とする。

**[MUST] プロジェクトの規定と矛盾する場合はプロジェクトの規定を優先させること。**

基本的には [Google JavaScript Style Guide](https://google.github.io/styleguide/jsguide.html) に従う。

## ソースファイル標準
### ファイル名
- **[MUST]** ファイル名は英小文字、アンダースコア、ダッシュ、数字のみ使用できる。
### 改行コード
- **[MUST]** CRLF
### 文字コード
- **[MUST]** UTF-8
### 特殊文字
#### 空白文字
- **[MUST]** 半角スペースのみ使用可能。
<!-- #### エスケープ -->
<!-- #### 非ASCII文字 -->

<!-- ## ソースファイル構造 -->
## 書式
### カッコ
- **[MUST]** 制御文（if, else, for, do, whileなど）の中括弧は省略しない。ステートメントの最初の文は新たな行で開始する。
    - ただし、単一行に収まり、elseをもたない場合、中括弧をつけずに1行に置くことができる。
- **[MUST]** 空でないブロックの字下げスタイルは [K&R スタイル](https://ja.wikipedia.org/wiki/%E5%AD%97%E4%B8%8B%E3%81%92%E3%82%B9%E3%82%BF%E3%82%A4%E3%83%AB#K&R%E3%81%AE%E3%82%B9%E3%82%BF%E3%82%A4%E3%83%AB) に従う。
- [SHULD] 空のブロックの場合、マルチブロックステートメント（if/else, try/catch/finally）でない限り、開始中括弧の直後に終了中括弧を使用できる。
### インデント
- **[MUST]** 1レベル空白2文字。
### ブロックスタイル
- 配列リテラル（[]）は任意のスタイル（ブロックスタイルを含む）を選択可能。
- オブジェクトリテラル（{}）は任意のスタイル（ブロックスタイルを含む）を選択可能。
- クラスリテラルはブロックスタイルで記述する。
- 無名関数はブロックスタイルで記述する。
- スイッチステートメント:

```
switch (animal) {
  case Animal.BANDERSNATCH:
    handleBandersnatch();
    break;

  case Animal.JABBERWOCK:
    handleJabberwock();
    break;

  default:
    throw new Error('Unknown animal');
}
```
### 行折り返し（Line-wrapping）
- 注: すべての状況でラインラップする方法を正確に示す包括的決定論的な設定はない。
- TODO: 折り返し位置
- **[MUST]** 折り返し後は2レベル以上インデントする。

### ステートメント
- **[MUST]** １行に複数のステートメントを記述しない。
- [SHOULD] １行の文字は80文字に制限する。これを超える場合は行の折り返しを行う。
    - ただし、長いURLやコピペを前提としたシェルコマンドなどは除く。

<!-- ### 空行 -->
### 空白
- **[MUST]** 行末に空白を置かない。
- **[MUST]** 予約語（if, for, catchなど）と丸括弧の間に空白を1文字置く。
- **[MUST]** 先行する閉じ中括弧がある予約語（else, catchなど）は閉じ中括弧との間に空白を1文字置く。
- **[MUST]** 開始中括弧の前に空白を1文字置く。
    - **[MUST]** オブジェクトリテラル、配列リテラルの要素の場合は空白を置かない。 `foo({a: [{c: d}]})`
- **[MUST]** 二項演算子、三項演算子の両隣に空白を1文字置く。
- **[MUST]** 単項演算子の場合、直前に空白を置かない。
- **[MUST]** カンマ、セミコロンのあとに空白を1文字置く。前には空白を置かない。
- **[MUST]** オブジェクトリテラル内のコロンのあとに空白を1文字置く。
- **[MUST]** コメントのダブルスラッシュのあとに空白を1文字以上置く。

### 水平整列（Horizontal alignment）
- [SHULD] 水平整列は推奨されない。
    - アライメント基準のゆらぎ、レビュー遅延、マージ競合
    - 他言語やプロジェクトによって推奨される場合がある（Apexなど）<!-- tajima -->

```
// ok
{
  tiny: 42,
  longer: 435,
};

// avoid
{
  tiny:   42,  // permitted, but future edits
  longer: 435, // may leave it unaligned
};
```

### 関数の引数
- 可能な限り引数は1行にすべて収める。場合によっては関数の開始丸括弧語に改行する。
- [SHOULD] 複数行に別れる場合は1行に1引数を置くことが推奨される。
- **[MUST]** 関数の引数に行折り返しを行う場合は2レベルインデントを行う。

```
// ok
doSomething(
    descriptiveArgumentOne, descriptiveArgumentTwo, descriptiveArgumentThree) {
  // …
}
doSomething(
    veryDescriptiveArgumentNumberOne,
    veryDescriptiveArgumentTwo,
    tableModelEventHandlerProxy,
    artichokeDescriptorAdapterIterator) {
  // …
}
// avoid
doSomething(veryDescriptiveArgumentNumberOne, veryDescriptiveArgumentTwo,
    tableModelEventHandlerProxy, artichokeDescriptorAdapterIterator) {
  // …
}
```
### その他
- 基本的にシングルクォートを使用し、エスケープが必要な場合はダブルクォートを使用する。よしなに使い分け。<!-- tajima -->

<!-- ロジック -->
## 機能
### 変数宣言
- **[MUST]** ローカル変数の宣言に var を使用しない。const, let を使用すること。
- **[MUST]** 変数の再割り当てをする必要が無い限り、constをデフォルトで使用する。
- **[MUST]** 変数の宣言は1行に1変数まで。
- **[MUST]** スコープを最小限にするため、変数は使用される直前に宣言されること。
- 必要に応じてJSDocのtypeアノテーション（もしくはインライン）で変数の説明を記述する。

```
const /** !Array<number> */ data = [];

/** @type {!Array<number>} */
const data = [];
```

### 配列リテラル
- **[MUST]** 最後の要素と閉じ括弧の間に改行がある場合は、最後の要素の後にカンマを付けること。
- **[MUST]** 配列コンストラクタ `new Array()` を使用しないこと。配列リテラル `[]` を使用する。
<!-- 5.2.4. Destructuring -->
<!-- 5.2.5 Spread operator -->

### オブジェクトリテラル
- **[MUST]** 最後の要素と閉じ括弧の間に改行がある場合は、最後の要素の後にカンマを付けること。
- **[MUST]** オブジェクトコンストラクタ `new Object()` を使用しないこと。オブジェクトリテラル `{}` を使用する。
- **[MUST]** クォート付きキーとクォートなしキーを混在させない。

```
// ng
{
  a: 42, // struct-style unquoted key
  'b': 43, // dict-style quoted key
}
```

<!-- 5.3.4 Computed property names -->

...

<!-- 命名 -->
