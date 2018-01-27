# Apex Practice Guide
# 目次

# Apex プラクティスガイド

## はじめに
Apex のベストプラクティス

ソースコードの見た目に関することは[こちら](apex_style.md)

## インスタンス
### Singleton
インスタンスが一つしか作られないことを明示的にする。
- 自身のインスタンスをプライベートのクラス変数に保持する。
- 外部からコンストラクタをコールできないようにする。
- getInstanceメソッドで、インスタンス未作成の場合はnewし、作成済みの場合はインスタンスを返す。

```
private static 自クラス名 singleton = new 自クラス名();

private 自クラス名() {}

public static 自クラス名() {
	return singleton;
}
```

### 共通クラス
共通メソッド、共通定数を保持するクラス。インスタンスを作れないようにする。
- 外部からコンストラクタをコールできないようにする。

```
private 自クラス名() {}
```

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

