# Apex Naming Guide
# 目次

# Apex 命名規則
- 全般
- クラス名・インターフェース名
- メソッド名
    - 修飾語
    - データベースアクセス
    - データの取得
    - データの設定・操作
        - データの検証
    - 非推奨
- 変数名
    - 修飾語
    - 接尾語
    - 仮引数
- 定数名

## はじめに
<!-- 命名規則を運用する目的を記述する -->

## 全般
- [SHOULD] 一般的でない略語は使用しない。
- [SHOULD] 一般的な略語は積極的に使用する。
- **[MUST]** 頭字語や類語は単語として綴りの記法を適用する。

```
// ok
XmlHttpRequest
getCustomerId

// ng
XMLHTTPRequest
getCustomerID
```

## クラス名・インターフェース名
**[MUST]** 名詞・動詞を名詞化した語を使用。
**[MUST]** アッパーキャメルケース。
- 記録する: XxxLoger
- 整形する: Formatter
- 抽象クラス: AbstractXxx
- インターフェース: XxxInterface
- ファクトリ: XxxFactory
- テストクラス: XxxTest

## メソッド名
**[MUST]** ローワーキャメルケース
**[MUST]** 動詞(句)を使用。
### 修飾語
- yyyを無視してxxxする: xxxIgnoreYyy
### データベースアクセス
以下の用語を使用する。
データベースアクセスしない場合、以下の用語を使用してはならない。
- queryXxx  `Database.query(query)`
- insertXxx
- updateXxx
- upsertXxx
- deleteXxx
- undeleteXxx
### データの取得
- クエリ結果の取得: queryXxx
- インスタンスの取得（ファクトリメソッド）: createXxx, newXxx `Date.newInstance(2017,1,1)`
    - 組み込みクラス（コレクションなど）のインスタンス
    - SObjectのインスタンス
    - Apexクラスのインスタンス
- プロパティの取得: getXxx
    - プロパティの値を直接返す
    - プロパティの値を処理して返す
### データの設定・操作
- プロパティの設定: setXxx
- 取り除く: removeXxx
- インスタンスの変換 (コンバータメソッド): toXxx
#### データの検証
- ただしい状態かを検証→エラーコード返却: validateXxx
- 期待した状態かを検証→データの修正: ensureXxx
- 前提条件を表す: assertXxx
    - 組み込みのassertメソッドの使用を検討する
    - assertメソッドをエラー代わりに使用してはならない
    - assertメソッドで発生したexceptionは通常catchしない
### 非推奨
言葉の示す範囲が広く、命名に使用するのは不適切
- 除外する: filter
- 切り抜く: clip
- 状態を見る: check、test、judge
<!--
※未整理
create, build, make, generate
- 数える: count
### 状態の変更・確認
#### 初期化
initialize, setup
#### 破棄
destroy, dispose
#### 確認
contains, exists
-->

## 変数名
- **[MUST]** 名詞を使用する
- **[MUST]** ローワーキャメルケース
- **[MUST]** イテレータ( i, j, k )、例外( e )以外に一文字の変数名を使用しない。
- **[MUST]** 一時的な変数であっても説明的な変数名を使用する。
### 修飾語
- 利用可能な: availableXxx
- 未知の: unknownXxx
- 対象外の: ignoreXxx
- 未処理の: rawXxx
- 最大・最小の: minXxx, maxXxx
- 入力された: received
- 期待値: expected
- 正常な: validXxx
- 異常な: invalidXxx
- 変更前: OriginalXxx
- 現在の: CurrentXxx
- 目的の: 名詞To動詞 `listToUpdate`
### 接尾語
- 数: xxxChar、xxxNum、xxxQuantity
- 条件: xxxCondition `searchCondition`
    - xxxlengthは使用しない
### 仮引数
- pXxx (コンストラクタ・メソッドの中で同じ変数名を使用したい場合は仮引数にpをつける)

## 定数名
**[MUST]** 大文字のスネークケース