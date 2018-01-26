# Apex Naming Guide
# 目次



# Apex スタイルガイド

## はじめに

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