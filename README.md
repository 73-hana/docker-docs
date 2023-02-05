- Dockerはクライアントサーバ型アーキテクチャを採用。Dockerデーモンはイメージやコンテナなどのオブジェクトを管理し、Dockerクライアントはコマンドを読み取りDockerデーモンに命令を伝える。

- コンテナを起動するコマンド`docker run -dp 3000:80 docker/getting-started`のうち、`-p 3000:80`はコンテナのポート80番とホストマシンのポート3000番をマップするオプションである。

- コンテナとはサンドボックスされたプロセスであり、コンテナのファイルシステムはイメージによって提供される。

- コンテナを作成するコマンド`docker build -t getting-started .`のうち、`-t`はイメージにタグ（名前）をつけるオプションである。

- 古いコンテナがホストマシンのポートを使用している場合、同じポートを指定して新しいコンテナを起動することはできない。その場合はホストマシンの別のポートを指定するか、古いコンテナを削除する必要がある。

- イメージを共有するには、Docker Hubが便利。コマンドラインでDocker Hubにログイン（`docker login -u <user-name-of-docker-hub>`）し、タグを変更（`docker tag <old-tagname> <new-tagname>`）し、そしてDocker Hubにプッシュ（`docker push <my-usename>/<image-name>`）する。

- 同一イメージから作成したコンテナでも、ファイルシステムに関する変更は外部から閲覧できない。

- データの入れ物をホストマシンに用意する手段として、ボリュームを作成することができる。`docker volume create <volume-name>`を実行しボリュームを作成し、ボリュームを指定してコンテナを起動（`docker run -dp 3000:3000 -v <volume-name>:<path-to-data-in-docker-container>`）する。

- 名前つきボリュームを利用する時、実際にデータが保存される場所を確認したい場合は`docker volume inspect <volume-name>`を実行する。