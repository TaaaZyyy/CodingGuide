# Lightningコンポーネント
## 概要
### 一言で言うと
動的なWebアプリケーションを開発するためのUIフレームワーク。
サーバー側ではApex、クライアント側ではJavascriptで動く。
カプセル化されたコンポーネントを組み合わせる（コンポジション）ことで迅速な開発を可能にする。
### 学習の際の注意点
Lightning コンポーネントフレームワークは Visualforce よりも大規模であり、洗練され、複雑です。
それほど機能的でない Lightning コンポーネントアプリケーションを記述する場合でさえ、JavaScript に精通している必要があります。
他言語と比較してjavascriptは学習する必要がある十分な違いが存在します。たとえば、オブジェクトと継承、範囲ルール、真と偽を分ける予測不能な動作などです。
### 開発ツール
- [Chrome DevTools](https://developers.google.com/web/tools/chrome-devtools/)
- [Salesforce Lightning Inspector](https://developer.salesforce.com/docs/atlas.ja-jp.210.0.lightning.meta/lightning/inspector_intro.htm)
### デバッグ
- コードのどの行で失敗しているのかをすばやく見つけるには、コードを実行する前に [Pause on all exceptions (すべての例外で一時停止)] オプションを有効にします。
- Lightning コンポーネントのデバッグモードの有効化（設定>Lightningコンポーネント>デバッグモードを有効化）
- Salesforce Lightning Inspector Chrome 拡張機能
- console.log()

### 利用の前提
- カスタムSalesforceドメイン名を定義していること
### CLASSICでどこでつかえる？？？？バンドルできる場所

### コンポーネント（バンドル）
LightningコンポーネントによるWebアプリケーションの構成単位。
インスタンスとして利用できるため、再利用性高い。
HTML、CSS、javascript

### コンポーネント

### イベント
インターフェースイベント発生時に対応するハンドラを作成する。

### Lightning 基本コンポーネント

### Field Service Lightning 
### Lightning Design System
cssフレームワーク。Salesforceの提供サービスが利用しているデザインを利用できる。商用可。
積極的に使う。独自のCSSスタイルは最終手段的に限定された特別なケースでのみ使用。
#### 注意点
SLDS コンポーネントは Lightning コンポーネントではありません。Lightning 組み込みコンポーネントの中で必要なものが見つからない場合、自分でコンポーネントを作成するための開始点として SLDS サイトを使用します。（SLDS は、Salesforce が目指している未来の世界を表します。）
#### 使用方法1
1. https://www.lightningdesignsystem.com/ から使用したいコンポネントを見つける
2. 使用箇所にコメントでLDSを使用する旨を記載する（保守開発を用意にするため）

```
<!--
    Lightning Design System の data table を使用する
    https://www.lightningdesignsystem.com/components/data-tables/
-->
```

3. コードをコピペする
4. 目的に合わせてクラスを変更する
5. 目的に合わせてコードを修正する

## 設計手順
アプリケーションをコンポーネントに分解する。
最初に最も小さく、最も内側のコンポーネントから作成していく。

テスト '/c/アプリケーション名.app'




### aura名前空間
アプリケーションロジックを簡略化するコンポーネント
### ui名前空間
ボタン、入力項目などユーザインターフェース
### force名前空間
Salesforce固有のコンポーネント


コントローラ
ヘルパー
スタイル
ドキュメント
レンダラ
設計
SVG




```
<aura:component controller="AccountsController">
    <aura:attribute name="accounts" action="{!c.doInit}"/>
    <aura:handler name="init" value="{!this}" action="{!c.doInit}"/>
</aura:component>	

```







たとえば、one.app コンテナ (Lightning Experience と Salesforce アプリケーション) では、レコードに移動する、レコードを作成または編集する、URL を開くといった、イベントの処理がサービスとして提供されます。
他のコンテナではこれらのサービスは提供されません。あるコンテナのサービスに依存するコンポーネントは、そのサービスが提供されない別のコンテナでは機能しません。たとえば、新規レコードの作成に force:createRecord イベントを使用すると、Lightning Experience では適切に機能しますが、そのコンポーネントをスタンドアロンアプリケーションや Lightning Out 内で使用すると、イベントを処理するものがないため、動作が停止します
ここが重要な部分です。Lightning コンポーネントコードは、それを内部で実行するコンテナのサービスのみにアクセスできます。そのコンテナが別のコンテナの内部にある場合も同じです。




ヘルパーはシングルトンであり、コンポーネントのすべてのインスタンスで共有されます。


コントローラ JavaScript コードで属性値を取得および設定するには get メソッドと setメソッドを使用します。
 


コンポーネントの属性の値を他のコンポーネントが操作できないようにするには、属性を private にします。そうしない場合は、属性がコンポーネントの公開 API の一部になります。
非公開属性の名前には、プレフィックスとしてアンダースコアを使用して (_myAttribute など)、非公開属性であることを明確にするとよいでしょう)


expando は軽微なバグやメモリーリークにつながる場合があるということです。うまく機能すると思われる一方で、問題が発生する可能性も捨てきれません。そのため、Salesorce では expando の使用はお勧めしません。










Lightning コンポーネントフレームワークは、Visualforce のこれらの制限事項に対処するように設計されました。特に、コンポーネントは (意図的に) 疎結合されています。この疎結合のメカニズムがイベントです。








Lightning コンポーネントコントローラのコードはクライアント側で実行されますが、データはサーバ側に保存されます。キャッシュがない場合、新しいデータが必要になるたびに何らかのサーバ要求を行うことになります。それはおそらく、Visualforce コントローラであれば記述することがなかったコードです。


