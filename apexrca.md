# Apex(team)
# 目次

- ファイルの構成
  - 文量
  - 改行コード
  - 文字コード
  - 空行
  - 空白
	- 縦列
  - 括弧
  - インデント
  - 行
  - 改行・折り返し
- ステートメント
  - 条件文
  - 繰り返し文
  - try-catch文
- SOQL
- コメント
  - 実装コメント
  - ドキュメントコメント
- 命名規則
  - クラス名・インターフェース名
  - メソッド名
  - 変数名
  - 定数名

# Apex スタイルガイド

## はじめに
コードの読みやすさを向上させ、エンジニアがコードを迅速かつ完全に
理解できるようにすることを目的とする。

基本的にはパフォーマンスを多少犠牲にしても、見やすさを重視する。

## ファイルの構成
ファイルは、空白業で区切られるセクションと、各セクションを識別する
オプションのコメントで構成される。
### 改行コード
- **[MUST]** CRLF
### 文字コード
- **[MUST]** UTF-8
### 空行
論理的に関連するコードをセクションに分け、可読性を高める目的で適宜使用する。
- **[MUST]** ファイルの末尾に空行を置かない。
- **[MUST]** **メソッド間は２行以上空行を入れる。**
### 空白
- **[MUST]** 行末に空白を置かない。
- **[MUST]** カンマ、セミコロンの直後に空白を置く。
- **[MUST]** 二項演算子とオペランドの間に空白を置く。
- **[MUST]** 単項演算子とオペランドの間に空白を置かない。
- **[MUST]** キャスト演算子の直後に空白を置く。
- **[MUST]** **丸括弧の内側1文字目に空白を置く。ただし、丸括弧の中がからの場合は空白を置かない。**
- **[MUST]** クラス、メソッド、コンストラクタの宣言で使用する中括弧の前に空白を置く。
- **[MUST]** コレクションの宣言で使用する中括弧の直前に空白を置かない。
- **[MUST]** if、while、forなどのキーワードと後続の丸括弧の間に空白を置く。
- **[MUST]** メソッド名と後続の丸括弧の間に空白を置かない。
### 縦列
- **[MUST]** **前後の行に同じ演算子が使用されている場合、空白を使って縦を揃える。**
- **[MUST]** **前後の行で同じ変数を使用している場合、空白を使って縦を揃える。**
- **[MUST]** **開始カッコは揃えない。閉じカッコは縦列で揃える。**
- **[MUST]** **カンマ、セミコロンで揃える。**
```
this.shouldUpdateJinzaiDev3   = JINKAI_DEV_3_TARGET_ORGANIZATIONRANK_SET.contains(org.OrganizationRank__c);
this.shouldUpdateKouka        = KOUKA_TARGET_ORGANIZATION_SET.contains(           org.OrganizationRank__c);
this.shouldUpdateMg           = MG_TARGET_ORGANIZATION_SET.contains(              org.OrganizationRank__c);
```
```
static final List<String> KYUTAI_FIELD_KEY_LIST       = new List<String>{'KYUTAI_1'      , 'KYUTAI_2'      , 'KYUTAI_3'      };
static final List<String> JIKOSHINKOKU_FIELD_KEY_LIST = new List<String>{'JIKOSHINKOKU_1', 'JIKOSHINKOKU_2', 'JIKOSHINKOKU_3'};
static final List<String> JINKAI1_FIELD_KEY_LIST      = new List<String>{'JINKAI1_1'     , 'JINKAI1_2'     , 'JINKAI1_3'     };
static final List<String> JINKAI2_FIELD_KEY_LIST      = new List<String>{'JINKAI2_1'     , 'JINKAI2_2'     , 'JINKAI2_3'     };
static final List<String> JINKAI3_FIELD_KEY_LIST      = new List<String>{'JINKAI3_1'     , 'JINKAI3_2'     , 'JINKAI3_3'     };
```
### 括弧
- **[MUST]** 中括弧、カギカッコで行を始めない。
- [SHOULD] 演算子を複数含む式は優先順位を明確にするため、丸括弧を使用する。
```
if ( a == b && c == d )         // AVOID!
if ( ( a == b ) && ( c == d ) ) // RIGHT
```
- **[MUST]** 三項演算子の条件句は丸括弧で囲む
### インデント
- **[MUST]** **インデントはタブ文字を使用する。**
- **[MUST]** ブロック内の文は1レベルインデントする。
### 行
- **[MUST]** 1行につき1宣言まで。
- **[MUST]** 1行につき1文（statement）まで。
- **[MUST]** **極力改行しない**。
- **[MUST]** **クラス宣言文、メソッド宣言文で改行を行わない。**
### 改行・折り返し
- [SHOULD] カンマの前で改行しない
- [SHOULD] **演算子の前後で改行しない**
- [SHOULD] 改行のあとの文は1レベル深くインデントする。

## ステートメント
- **[MUST]** ステートメントの予約語と丸括弧の間は1つ空白を置く。1つ以上置かない。
### 条件文
- **[MUST]** 条件文のブロックの中が1行の場合、条件文に続けて1行で記述する。中括弧を省略しない。中括弧の内側には空白を1つ置く。
- **[MUST]** 丸括弧と中括弧の間に空白を1つ置く。
```
if ( jugyouin.NextMonthEnterdCompanyRoot__c != null ) { jugyouin.NyushaKeiro__c =  jugyouin.NextMonthEnterdCompanyRoot__c; }  // [C37] 翌月入社経路
```
```
if (      shokusei  ==  'EXP' ) {  employeementPattern  =  '半年契約'; }
else if ( shokusei  ==  'CV'  ) {  employeementPattern  =  'CV';      }
```
- **[MUST]** 複数行にまたがる条件文の中括弧は省略しない。
### 繰り返し文
- [SHOULD] do-while文は避け、for文を使用する。
- **[MUST]** for文のセミコロンのあとに空白を入れる。
### try-catch文

## SOQL
- **[MUST]** インラインSOQLを書く場合は、SELECTの前で改行し、インデントを **TODO** 個置く。
- **[MUST]** インラインSOQLの予約後は縦を揃え、予約後以外の句はインデントする。
- **[MUST]** インラインSOQLの閉じカギカッコは予約後と同じインデントに揃える。
- **[MUST]** インラインSOQLのSELECTする項目の記述は、1行につき1語までとする。
- **[MUST]** インラインSOQLのカンマは縦列を揃える。

```
for ( WCMSheet2__c wcmSheet : [
								SELECT
									Id        ,   // SalesforceId
									Name      ,   // 時期 - 氏名 - バージョン
									Account__c,   // 従業員
									Will_s2__c    // ２～３年後Will本人
								FROM
									WCMSheet2__c
								WHERE
									UpsertKey__c IN : wcmSheetUpsertKeySet
								] ) {
```
## コメント
### 実装コメント
特定の実装に関するコメント。
コード自体で容易に入手できない追加情報を提供するために使用し、乱用しない。
- **[MUST]** 日本語を使用する。
- [SHOULD] コードの不活性化の目的でコメントを使用しない（不要なコードは削除する）。
- **[MUST]** TODOコメントは以下の形式を使用。
    // TODO: コメント
### ドキュメントコメント
仕様を記述する
Apexdocの記述方法に従う

## 命名規則
- [SHOULD] 一般的でない略語は使用しない。
- [SHOULD] 一般的な略語は積極的に使用する。
- **[MUST]** 頭字語や類語は単語として綴りの記法を適用する。
```
// good
XmlHttpRequest
getCustomerId

// bad
XMLHTTPRequest
getCustomerID
```
### クラス名・インターフェース名
- **[MUST]** アッパーキャメルケース
- **[MUST]** 名詞を使用。
### メソッド名
- **[MUST]** ローワーキャメルケース
- **[MUST]** 動詞(句)を使用。
### 変数名
- **[MUST]** ローワーキャメルケース
- **[MUST]** イテレータ( i, j, k )、例外( e )以外に一文字の変数名を使用しない。
- **[MUST]** 一時的な変数であっても説明的な変数名を使用する。
### 定数名
- **[MUST]** 大文字のスネークケース

<!--
## プラクティス
### アクセス
- アクセス修飾子を適切に使用する
### クラスメソッド・クラス変数
- [SHOULD] インスタンスからクラスメソッド、クラス変数にアクセスしない。
### 定数
- 数値定数は-1、0、1を除いて直接コーディングしない。
### 変数代入
- **[MUST]** 1つのステートメントで複数の変数に同じ値を代入しない。
```
fooBar.fChar = barFoo.lchar = 'c'; // AVOID!
```
### メソッド定義
- オーバーライドは避ける。どうしても必要な場合はコメントに目的・意図を書く。
-->
