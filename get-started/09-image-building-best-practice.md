# イメージ構築のベストプラクティス

## 安全性の検査

イメージのセキュリティ脆弱性を検査するためには、まず`docker scan --login`でログインを行い、`docker scan <image-name>`でイメージをスキャンできる。

## イメージの階層化

イメージ内の各レイヤーが使ったコマンドを表示するためには、`docker image history`コマンドを用いる。レイヤを省略させずに表示するには`docker image history --no-trunc getting-started`コマンドを用いる。

