# アプリケーションの共有

Dockerイメージを共有するには、Dockerレジストリを使う必要がある。デフォルトはDocker Hubである。

## リポジトリ作成

イメージを送信するにはDocker Hubにアクセスし、リポジトリを作成する。

## イメージを送信

コマンドラインで`docker login -u <my-username>`を実行し、Docker Hubにログインする。そして、イメージのタグを、`<my-username>/<image-name>`の形に変更する。最後に`docker push <my-username>/<image-name>`を実行し、ローカルホストからDocker Hubにプッシュする。

## 新しいインスタンスでイメージを実行

Play With Dockerというサービスを使えば、まっさらなインスタンスでアプリを実行できる。