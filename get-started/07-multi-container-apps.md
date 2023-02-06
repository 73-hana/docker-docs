# 複数コンテナのアプリ

通常、コンテナは１つのことをしっかりと実行するべきである。

## コンテナのネットワーク機能

コンテナは、デフォルトでは独立した状態で実行されるため、同じマシン上の他のプロセスやコンテナの挙動を窺い知ることはできない。しかしネットワーク機能を用いて同じネットワーク上のコンテナと通信できる。

# MySQLの起動

同じネットワーク内にいるコンテナ同士しか通信できないため、まずはネットワークを作成するために`docker network create todo-app`を実行する。そしてMySQLのコンテナを実行しネットワークに紐付ける。

`docker run -d --network todo-app --network-alias mysql -v todo-mysql-data:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=secret -e MYSQL_DATABASE=todos mysql:8.0`

`-v todo-mysql-data:/var/lib/mysql`では名前付きボリュームをコンテナのディレクトリにバインドしている。事前に`docker volume create todo-mysql-data`を実行していないが、Dockerは先のコマンドで名前付きボリュームを使いたいということを認識し自動的にボリュームを生成する。`--network-alias mysql`でネットワークの別名を付与できる。この別名コンテナのホスト名にもなるため、DNSの名前解決にも使われる。

MySQLが動作しているか確認するには、`docker exec -it <container-id> mysql -u root -p`を用いてコマンドラインからMySQLにログインを試みる。

## MySQLに接続

`--network-alias`でコンテナにエイリアスを付けているので、同一ネットワーク上のコンテナに接続するにはそのエイリアスに接続するだけで良い。

## MySQLとアプリを動かす

`docker run -dp 3000:3000 -w /app -v "$(pwd):/app" --network todo-app -e MYSQL_HOST=mysql -e MYSQL_USER=root -e MYSQL_PASSWORD=secret -e MYSQL_DB=todos node:18-alpine sh -c "yarn install && yarn run dev"`コマンドを用いてTodoアプリを動かす。その後`docker logs <container-id>`コマンドでログを確認し、mysqlと接続できていることを確認する。