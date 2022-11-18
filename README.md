# Open API Spec V3.1 of Admin Kong OSS V3

[Kong Admin APIドキュメント](https://david3080.github.io/kongadminapi)

以下を参考に作成しています
- [Kong GWのオフィシャルGithubサイトに置いてある中途半端なOASファイル](https://github.com/Kong/kong/blob/master/kong-admin-api.yml)
- [Kongのオフィシャルドキュメント上のAdmin APIサイト](https://docs.konghq.com/gateway/3.0.x/admin-api)
- [ドキュメントの元LUAファイル](https://github.com/Kong/kong/blob/master/autodoc/admin-api/data/admin-api.lua)

下記のルールで整理しています。
- 対象オブジェクトは、Service、Route、Consumer、Plugin、Certificate、SNI、Upstreamの順
(※ [Kongにおける証明書に関するブログ](https://konghq.com/blog/mutual-tls-api-gateway)によるとKong OSSではクライアント認証を行うmTLSプラグインが提供されていないため、クライアント証明書の検証するCA Certificateオブジェクトは使わないため対象から外しています）
- HTTPメソッドは、GET、POST、PUT、PATCH、DELETEの順
- OAS1ファイル上ではpathのURIは重複できないためKongオフィシャルドキュメントのパス順ではなく、操作対象のオブジェクトごとに整理しています
- OAS内のタグはオブジェクト名もしくは2つのオブジェクト名の組み合わせで作成しています
- 上記の考え方は[Kong Admin APIのオブジェクトごとの整理](./APIList.md)にまとめています。

# Kong GW OSS V3 + PostgreSQLのdocker-compose.yml

上述のKong Admin APIドキュメントから「try it」を実行して学習するための環境です。

以下を参考に作成しています。

https://github.com/Kong/demo-scene/tree/main/kong-docker/postgres

Docker Composeが稼働する環境で下記のコマンドを実行するとKongが起動します。

```
$ docker-compose up -d
```

証明書が不正ですが、https(443ポート)でKong APIにアクセスでき、8001ポートでKong Admin APIにアクセスできるように設定してあります。

PostgreSQLのボリュームを削除して開始したい場合は下記のコマンドを実行します。
```
$ docker volume rm kongadminapi_kong-db-data
```

# Kong Admin API Demo
[mockbinサンプルを実行できるKong Admin API OAS](https://david3080.github.io/kongadminapi/mockbin.html)からtry itを実行しながら下記のデモシナリオを実行します

## ① mockbin　APIをサービス登録する
1. [サービスの登録](https://david3080.github.io/kongadminapi/mockbin.html#/operations/1-2_create-service)
2. [ルートの登録](https://david3080.github.io/kongadminapi/mockbin.html#/operations/2-8_create-route-associated-to-a-specific-service)
3. [request-transformerプラグインを設定](https://david3080.github.io/kongadminapi/mockbin.html#/operations/4-8_create-plugin-associated-to-a-specific-service)し、ヘッダー"Accept: application/json"を追加.
4. "localhost:8000/mockbin"を実行してmockbinからJSONが帰ってくることを確認し、bodyのheders配列に「accept: "application/json"」が帰ってきていることを確認.

## (TODO)② mockbin　APIをターゲットに登録し、アップストリーム経由で実行する
## (TODO)③ consumerとauthを登録し、Basic認証でmockbin APIを実行する
## (TODO)④ rate-limitingプラグインを設定する
## (TODO)⑤ certificateとsniを設定し、httpsでmockbin APIを実行する

# やりたいことメモ
- [Stoplight Elementsデモサイト](https://elements-demo.stoplight.io/#/)を参考に複数のOASファイルから選択を可能にする
