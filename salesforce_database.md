# 目次

# Salesforceデータベース 規約

## はじめに
オブジェクト名
レコードタイプを使用するときは全レコードタイプを包括するような物理名をつけること。でないと混乱を招く。特に自身に参照関係を作るときに参照関係の物理名の設定において。
項目
子リレーション名：子の物理名 + s　　（Children__r は、オブジェクトレコードのリストであることに意識的になるため）