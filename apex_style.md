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
- SOQL
- コメント
    - 実装コメント
    - ドキュメントコメント


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
- **[MUST]** メソッド間に3行以上空行を置く。
- **[MUST]** メソッド内の論理的な区切りに2行の空行を置く。
- **[MUST]** ソースコードを見やすくする目的で適宜1行の空行を置く。
### 空白
- **[MUST]** 行末に空白を置かない。
- **[MUST]** カンマ、セミコロンの直後に空白を置く。
- **[MUST]** 二項演算子とオペランドの間に空白を置く。
- **[MUST]** 単項演算子とオペランドの間に空白を置かない。

```
a + b // ok
a+b   // ng

a++   // ok
a ++  // ng
```

- **[MUST]** キャスト演算子の直後に空白を置く。

```
(User) obj // ok
(User)obj  // ng
```

- **[MUST]** 丸括弧の内側1文字目に空白を置く。ただし、丸括弧の中がからの場合、及びキャスト演算子の場合は空白を置かない。

```
method( str ) // ok
method(str)   // ng
```

- **[MUST]** クラス、メソッド、コンストラクタの宣言で使用する中括弧の前に空白を置く。
- **[MUST]** コレクションの宣言で使用する中括弧の直前に空白を置かない。
- **[MUST]** if、while、forなどのキーワードと後続の丸括弧の間に空白を置く。
- **[MUST]** メソッド名と後続の丸括弧の間に空白を置かない。
<!-- TODO: コレクションの初期化の中括弧 List<String>{} か List<String> {} か -->
### 縦列
- **[MUST]** 前後の行に同じ演算子が使用されている場合、空白を使って縦を揃える。
- **[MUST]** 前後の行で同じ変数を使用している場合、空白を使って縦を揃える。
- **[MUST]** 開始カッコは揃えない。閉じカッコは縦列で揃える。
- **[MUST]** カンマ、セミコロンで揃える。

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
if ( ( a == b ) && ( c == d ) ) // ok
if ( a == b && c == d )         // avoid
```

- **[MUST]** 三項演算子の条件句は丸括弧で囲む
### インデント
- **[MUST]** インデントはタブ文字を使用する。
- **[MUST]** ブロック内の文は1レベルインデントする。
### 行
- **[MUST]** 1行につき1宣言まで。
- **[MUST]** 1行につき1文（statement）まで。
- **[MUST]** クラス宣言文、メソッド宣言文で改行を行わない。
### 改行・折り返し
- [SHOULD] カンマの前で改行しない
- [SHOULD] 演算子の前後で改行しない
- [SHOULD] 改行のあとの文は1レベル深くインデントする。

## ステートメント
- **[MUST]** ステートメントのifやwhileなどと丸括弧の間は1つ空白を置く。1つ以上置かない。
<!-- ifとかwhileとかは一般的になんと呼ばれる？ -->

```
if ( isActive ) {  // ok
if( isActive ) {   // ng
```

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

### 繰り返し文
- [SHOULD] do-while文は避け、for文を使用する。
- **[MUST]** for文のセミコロンのあとに空白を入れる。

## SOQL
<!-- **[MUST]** インラインSOQLを書く場合は、SELECTの前で改行し、インデントを **TODO** 個置く。-->
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

```
    // TODO: コメント
```

### ドキュメントコメント
仕様を記述する
Apexdocの記述方法に従う