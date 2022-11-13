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

# Kong GW OSS V3 + PostgreSQLのdocker-compose.yml

上述のKong Admin APIドキュメントから「try it」を実行して学習するための環境です。

以下を参考に作成しています。

https://github.com/Kong/demo-scene/tree/main/kong-docker/postgres

Docker Composeが稼働する環境で下記のコマンドを実行するとKongが起動します。

```
$ docker-compose up -d
```

証明書が不正ですが、https(443ポート)でKong APIにアクセスでき、8001ポートでKong Admin APIにアクセスできるように設定してあります。
