- Dockerはクライアントサーバ型アーキテクチャを採用。Dockerデーモンはイメージやコンテナなどのオブジェクトを管理し、Dockerクライアントはコマンドを読み取りDockerデーモンに命令を伝える。

- コンテナを起動するコマンド`docker run -dp 3000:80 docker/getting-started`のうち、`-p 3000:80`はコンテナのポート80番とホストマシンのポート3000番をマップするオプションである。

- コンテナとはサンドボックスされたプロセスであり、コンテナのファイルシステムはイメージによって提供される。

- コンテナを作成するコマンド`docker build -t getting-started .`のうち、`-t`はイメージにタグ（名前）をつけるオプションである。

- 古いコンテナがホストマシンのポートを使用している場合、同じポートを指定して新しいコンテナを起動することはできない。その場合はホストマシンの別のポートを指定するか、古いコンテナを削除する必要がある。

- イメージを共有するには、Docker Hubが便利。コマンドラインでDocker Hubにログイン（`docker login -u <user-name-of-docker-hub>`）し、タグを変更（`docker tag <old-tagname> <new-tagname>`）し、そしてDocker Hubにプッシュ（`docker push <my-usename>/<image-name>`）する。

- 同一イメージから作成したコンテナでも、ファイルシステムに関する変更は外部から閲覧できない。

- データの入れ物をホストマシンに用意する手段として、ボリュームを作成することができる。`docker volume create <volume-name>`を実行しボリュームを作成し、ボリュームを指定してコンテナを起動（`docker run -dp 3000:3000 -v <volume-name>:<path-to-data-in-docker-container>`）する。

- 名前つきボリュームを利用する時、実際にデータが保存される場所を確認したい場合は`docker volume inspect <volume-name>`を実行する。

- 名前付きボリュームはデータの保管場所を確認する必要があるが、バインドマウントを使えばホスト上のディレクトリを指定して接続できる。ボリュームもマウントも`-v`オプションで指定できる。

- コンテナのログを確認するには`docker logs -f <container-id>`を用いる。`-f`はフォローの意。

- 複数のコンテナを互いに接続させたい場合は、同一ネットワーク上に配置し、ネットワークを用いて接続させるだけで良い。まずはネットワークを作成（`docker network create xxxxx`）し、コンテナを立ち上げるときにネットワークに登録する（`docker run -d --network xxxxx --network-alias xxx -v xxx:xxx mysql`）。--network-aliasでつけた別名が、ネットワーク上のホスト名になる。

- Docker Composeはコンテナを複数持つアプリを定義し共有するためのツールである。LinuxはDockerとは別にダウンロードする必要がある。

- Docker Composeの場合は、アプリプロジェクトのルートでdocker-compose.ymlファイルを生成する必要がある。名前付きボリュームは明示的に定義する必要がある。

- アプリケーションスタックを起動するには`docker-compose up -d`コマンドを用いる。`-d`はバックグランドで実行するオプション。アプリケーションスタックを解体する場合は`docker-compose down`コマンドを用いる。しかし名前付きボリュームは残ったままになってしまうので、`docker-compose down --volumes`とオプションを追加する必要がある。