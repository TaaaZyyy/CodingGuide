# Apex Naming Guide
# 目次



# Apex スタイルガイド

## はじめに
Apex のベストプラクティス

ソースコードの見た目に関することは[こちら](apex_style.md)


## SOQL
### SOQLインジェクション対策
ユーザ入力値を文字列としてのみ扱うようにする
#### 静的クエリ
バインド変数を使用する。

```
String queryName = '%' + name + '%';
List<Contact> contacts = [
						SELECT
							Id
						FROM
							Contact
						WHERE
							Name LIKE :queryName
						];
```

#### 動的クエリ
String.excapeSingleQuotes(str) を使用する。
静的クエリを使用できる場合は基本的に静的クエリを使用する。

```
String query = '';
query += 'SELECT ';
query += '    Id ';
query += 'FROM ';
query += '    Contact ';
query += 'WHERE ';
query += '    Name LIKE \'%' + String.excapeSingleQuotes(name) + '%\' ';
Database.query(query);
```

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

