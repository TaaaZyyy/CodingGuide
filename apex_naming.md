# Apex Naming Guide
# 目次
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
- その他
    - 省略可能な単語

# Apex 命名ガイド

## はじめに
ソースコードの可読性を向上させ、保守性・開発速度を向上させるための参考として、命名ガイドをここに提示する。
良い命名が思い浮かばないときはそもそも設計に問題がある場合もあるので、設計の見直しも検討すること。

## 全般
- [SHOULD] 説明的で意味・意図を表している命名を行う。
- [SHOULD] 他の意味に取られるような命名をしない。
    - 名前が「他の意味と間違われることはないだろうか？」と何度も自問自答する。
- [SHOULD] 抽象的な名前、汎用的な名前は使用しない。具体的で意味が明確な名前を使用する。
- [SHOULD] 長すぎず短すぎず、スコープに見合った長さで命名を行う。
- [SHOULD] 一般的でない略語は使用しない。
- [SHOULD] 一般的な略語は積極的に使用する(省略可能な単語の項を参考)。
- [SHOULD] 特殊な業務用語を覗いて英語を使用する。
- **[MUST]** 頭字語や略語は単語として綴りの記法を適用する。
    <!-- - 参考: [AOSP Java Code Style for Contributors](https://source.android.com/setup/code-style#treat-acronyms-as-words) -->

```
// ok
XmlHttpRequest
getCustomerId

// ng
XMLHTTPRequest
getCustomerID
```

## クラス名・インターフェース名
- **[MUST]** アッパーキャメルケース。
    - インナークラス、Enum、カスタム例外もアッパーキャメルケースで命名する
- [SHOULD] 名詞・動詞を名詞化した語を使用。
- [SHOULD] (システムコード_)接頭語_名詞 で命名する
    - ex. `S2_VP_MovieListController`
- [SHOULD] 33文字以内で命名する(システム上クラス名は40文字まで。テストクラス作成を考慮(ZT_XxxTest)。)
    - トリガハンドラはトリガ名を使ってテストクラスを作成するため40文字まで。

### 接尾語
<!-- - 抽象クラス: AbstractXxx -->
<!-- - インターフェース: XxxInterface -->
<!-- - ファクトリ: XxxFactory -->

| 役割 | 接尾語 |
|:-|:-|
| 役割 | 接尾語 |
| コントローラ | Ctrl |
| 拡張コントローラ | ExtCtrl |
| バッチ | Batch |
| トリガ | Trigger |
| トリガハンドラ | TriggerHandler (40文字を超える場合は、Handler) |
| スケジューラ | Schedule |
| テストクラス | Test |
| ロジック | Logic |
| DTO | Dto |
| DAO | Dao |
| 共通部品ロジック | Util |

### 接頭語
- クラス単位でテストクラスを作成するときは元のクラスの接頭語を残してZT_をつける `ZT_BT_UserBelongUpdateBatch`
    - でないと通常のクラスとテストクラスの並び順が変わり、検索性が悪くなる

| 役割 | 接尾語 |
|:-|:-|
| Visualforceコントローラ | VP_ |
| Componentコントローラ | VC_ |
| 拡張コントローラ | VX_ |
| バッチ | BT_ |
| ロジック | BL_ |
| ウェブサービス | WS_ |
| トリガハンドラ | TH_ |
| スケジューラ | SC_ |
| テストクラス | ZT_ |
| DTO | DT_ |
| DAO | DA_ |
| 共通部品ロジック | UL_ |


## メソッド名
- **[MUST]** ローワーキャメルケース
- [SHOULD] 動詞(句)を使用。
- [SHOULD] 引数、戻り値との関係が明確な名前をつける。
    - うまく命名できない場合は設計に問題がよくあるので設計を見直してみる。
- [SHOULD] publicメソッドの場合、クラス名・インスタンス名とメソッド名で意味が重複しないように命名する。
<!-- - [SHOULD] publicメソッドはオブジェクト名と組み合わせて使用したときに冗長にならないように命名する -->

<!--
### 修飾語
- yyyを無視してxxxする: xxxIgnoreYyy
- -->

### データベースアクセス
以下の用語を使用する。
データベースアクセスしない場合、以下の用語を使用してはならない。
- queryXxx
    - cf. `Database.query(query)`
- insertXxx
- updateXxx
- upsertXxx
- deleteXxx
- undeleteXxx

### データの取得
- クエリ結果の取得: queryXxx
- インスタンス(他者)の取得: createXxx, newXxx
    - 組み込みクラス（コレクションなど）のインスタンスの取得
    - SObjectのインスタンスの取得
    - Apexクラスのインスタンスの取得
- インスタンス(自身)の取得: newInstance
    - cf. `Date.newInstance(2017,1,1)`
- プロパティの取得: getXxx
    - プロパティの値を直接返す
    - プロパティの値を処理して返す

### データの設定・操作
- プロパティの設定: setXxx
- 既にあるものに別の何かを追加する: addXxx
- 既にあるものに付け加える: appendXxx
- 一部を取り除く: removeXxx
- 空にする: clearXxx
- 初期状態に戻す: resetXxx
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
- 除外する: filterXxx
    - 戻り値が除外されたものなのか、除外されて残ったものなのかが明確でない。
    - 代案: excludeXxx、selectXxx
- 状態を見る: checkXxx、testXxx、judgeXxx
    - 処理の内容がわからない。戻り値が何を意味するか不明。
    - 代案: validateXxx、ensureXxx
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
- **[MUST]** ローワーキャメルケース
- **[MUST]** イテレータ( i, j, k )、例外( e )以外に一文字の変数名を使用しない。
- [SHOULD] 名詞(句)を使用する
    - ただしBoolean型は `isActive` などtrueが何を意味するのかひと目で分かる命名にする。
    - 迷ったら github でソース検索してHitが多い方を使用するとよい。

| 形式 | 意味 | 例 |
|:-|:-|:-|
| is + 形容詞 | 状態 | isEmpty |
| is + 名詞 + 過去分詞 | 状態 | isCellSelected |
| is + ~able | 可能 | isUpdatable |
| can + 動詞 | 可能 | canRead |
| has + 過去分詞 | 完了 | hasChanged |
| ~Exists | 存在 | userExists |
| has + 名詞 | 所有 | hasNext |



- [SHOULD] 一時的な変数であっても説明的な変数名(修飾語を使う)を使用する。
- [SHOULD] スコープにあった長さの変数名を使用する(ローカル変数に長過ぎる変数名を使用すると可読性が落ちる)
- [SHOULD] 汎用的な名前を避ける
    - `tmp, retval // avoid`
- **[MUST]** クラス名(Enumを含む)と同名の変数名は使用しない。
    - クラス変数・静的メソッドを使用するとコンパイルエラーになる

```
public enum Enumtest {HOGE}

private void method001(Enumtest enumtest) {
    System.debug(Enumtest.HOGE);
    // Static field cannot be referenced from a non static context
}
```

### 修飾語
例
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
- 目的の: 名詞To動詞
    - `listToUpdate`
    <!-- よく使用される updateHogeList は動詞+目的語なのでガイドライン違反になる -->

### 接尾語
例
- 数: xxxChar、xxxNum、xxxQuantity
- 条件: xxxCondition

### 仮引数
- pXxx (コンストラクタ・メソッドの中で同じ変数名を使用したい場合は仮引数にp(引数(parameter)のp)をつける)


## 定数名
- **[MUST]** 大文字のスネークケース


## その他
### 省略可能な単語
略語が一般的なものは略語を使用する。
- eval (evaluate, evaluation)
- doc (document)
- str (string)
- num (number)
- avg (average)
- mon (Monday)
- img (image)
- msg (message)

<!--
### 業務用語

| 意味 | 使用単語 |
|:-|:-|
| 兼務 | additionalPost |
| 職制 | shokusei |
| 職務 | shokumu |
| 部門Mgr | manager |
| 部長 | departmentChief |
| 上長 | superior |
| 従業員番号 | employeeNumber |
| フィードバック | feedback |
| 考課 | evaluation |
| 評価 | rating、assessment |
| 考課者 | evaluatePersonName |
| 新規性 | novelty |
| 所属 | belonging |
| 人事 | humanAffairs |
| 入社日 | hireDate |
| 備考 | remark |
| 役職 | title |
| 成果 | achievement |
| 行動評価 | behavioralAssessment |
| 再現性 | reproducibility |
| 汎用性 | versatility |
| 休職中連絡先 | duringLeaveContact |
| 出向先 | secondmentTo、secondedDestination |
| 出向元 | secondmentFrom |
| 出向 | secondment |
| 受入出向者 | acceptedSecondedEmployee |
| 送出出向者 | sentSecondedEmployee |
| 正式名称 | seishikiMeishou |
| WCMシート | wcmSheet, wcm |
DB設計ガイドを作成したら重複するので別ファイルに切り出す
-->

### 一般用語

| 意味 | 使用単語 |
|:-|:-|
| 電話番号 | Phone |
| 携帯電話番号 | Mobile |
| メールアドレス | Email |
| ヨミガナ・カナ | Kana |
