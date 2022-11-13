# Open API Spec V3.1 of Admin Kong OSS V3

[Kong Admin APIドキュメント](https://david3080.github.io/kongadminapi)

以下を参考に作成しています
- [Kong GWのオフィシャルGithubサイトに置いてある中途半端なOASファイル](https://github.com/Kong/kong/blob/master/kong-admin-api.yml)
- [Kongのオフィシャルドキュメント上のAdmin APIサイト](https://docs.konghq.com/gateway/3.0.x/admin-api)
- [ドキュメントの元LUAファイル](https://github.com/Kong/kong/blob/master/autodoc/admin-api/data/admin-api.lua)

下記のルールで整理しています。
- 対象オブジェクトは、Service、Route、Consumer、Plugin、Certificate、CACertificate、SNI、Upstreamの順
- HTTPメソッドは、GET、POST、PUT、PATCH、DELETEの順
- OAS1ファイル上ではpathのURIは重複できないためKongオフィシャルドキュメントのパス順ではなく、操作対象のオブジェクトごとに整理しています

# Kong GW OSS V3 + PostgreSQLのdocker-compose.yml

上述のKong Admin APIドキュメントから「try it」を実行して学習するための環境です。

以下を参考に作成しています。

https://github.com/Kong/demo-scene/tree/main/kong-docker/postgres

Certificate周りは以下のブログに整理されています。
https://konghq.com/blog/mutual-tls-api-gateway