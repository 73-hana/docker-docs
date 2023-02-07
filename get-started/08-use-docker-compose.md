# docker composeを利用する

Docker Composeはコンテナを複数持つアプリケーションを定義し共有するためのツールである。Docker Composeを利用することでアプリケーションスタックをファイルに定義しプロジェクト用リポジトリに保存できる。

# Docker Composeのインストール

Linuxマシンの場合のみ別途インストールが必要である。インストールされているかどうかは`docker-compose version`で確認できる。

#　Composeファイルの作成

アプリプロジェクトのルートでdocker-compose.ymlというファイルを作成する。そのファイルにはまずスキーマバージョンを書き、次にアプリケーションの一部として実行したいサービスを定義していく。

# アプリのサービス定義

サービスのエントリとコンテナのイメージを定義する。サービス名はネットワークエイリアスとなる。

# MySQLのサービス定義

アプリサービスを定義したdocker-compose.ymlファイルに、別のコンテナであるMySQLの設定も記入する。

`docker run`を用いてコンテナを実行したときは、名前付きボリュームが自動的に生成されたが、Docker Composeの場合は明示的に定義する必要がある。

# アプリケーションスタックの実行

アプリケーションスタックを起動するには`docker-compose up -d`コマンドを用いる。バックグラウンドで起動させたいので`-d`オプションを追加する。ログを調べたい場合は`docker-compose logs -d`コマンドを用いる。

# 全てを削除

全てを解体したい場合は、`docker-compose down`を実行するか、Dockerダッシュボードを使い削除する。しかし、Docker Composeの名前付きボリュームは削除されないので、`docker-compose down -volumens`とオプションを追加する必要がある。