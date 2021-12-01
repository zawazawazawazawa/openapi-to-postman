このrepositoryは [openapi-to-postman](https://github.com/postmanlabs/openapi-to-postman)をもとにfreeeのPublic APIを叩きやすいように変更を加えたものです


## 概要
freeeのPublic APIスキーマからPOSTMANのcollectionを作成するscriptです

[POSTMAN](https://www.postman.com/)

[freee developers site](https://developer.freee.co.jp/)

## 変換スクリプトの使い方

```
$ git clone git@github.com:zawazawazawazawa/openapi-to-postman.git
$ cd openapi-to-postman
$ node node convert.js --tag='Account items' --schema_path='swagger.yml'
```
cliから実行するときに渡す引数
- tag
  - 特定のendpointのcollectionだけ欲しいときに使います。freee APIの各endpointのtagを渡してください。
  - tagはリファレンスに載っているリソースの英語名です。勘定科目の場合は `Account items` になります。
  - 未指定の場合、全endpointのcollectionが作成されます。

- schema_path
  - collectionに変換する対象のfreee Public APIのスキーマの絶対pathを指定してください。
  - 現行版の最新スキーマは [freee developers site](https://developer.freee.co.jp/) の各種APIリファレンスを参照して下さい。

## 出力されるcollectionの使い方

tagを指定した場合は `{tag名}.json` 、未指定の場合は `collection.json` という名前のファイルが出力されます。

`--tag="Account items` と指定した場合のファイル名は `account-items.json` です。 

POSTMANからファイル指定でimportすると以下の構成のcollectionが作成されます。
```
free API/
       └ {Tag名}/
               ├ GET {リソース名} 一覧の取得
               ├ GET {リソース名} 詳細情報の取得
               ├ POST {リソース名} の作成
               ├ PUT {リソース名} の更新
               └ DELETE {リソース名} の削除

```
Tag名のcollectionの下に各種HTTPメソッドに対応したrequestが作成されます。

どのrequestも `company_id` と `accesstoken` という名前pararmeterはの環境変数を受け取るようになっています。

POSTMANのenvironmentかcollectionに環境変数を設定して利用してください。

その他のparameterは、スキーマのexampleの値がvalueに設定されています。

`partner_id` などはそのままでは動かないので適宜正しい値に変更してください。


