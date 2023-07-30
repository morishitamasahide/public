# JupyterNotebook_mm
コンテナを実行し、その中でjupyter notebookを立てることで、どこでもjupyter notebookができるようにするためのテンプレート

# はじめに
- Dockerfile : イメージのビルドのための定義
  - ベースとなるイメージから新しいDockerイメージを作成する手順を定義
  - 必要となるソフトウェアのインストール、ファイルのコピー、環境設定の手順など

- docker-compose.yml : 複数のコンテナの定義と関連付け
  - 1つ以上のコンテナの設定を定義し、それらのコンテナがどのように相互作用するかを指定する
  - ネットワーク、ボリューム、環境変数、依存関係などを定義
  - DockerFileよりももっとホストマシンspecificな印象

# 実行コマンド
JupyterNotebook_mmディレクトリに移動し、下記を実行

（初回のみ or DockerFileを更新した場合）
```
docker-compose build # docker-compose.ymlで指定されたサービスのイメージをビルドする. ホストマシンのDockerのローカルイメージストアに保存される. ローカルイメージストアはDockerデーモンが管理しており、システムのHDD上の特定のディレクトリに物理的に保存されている
```

コンテナの立ち上げ（すべて）
```
docker-compose up -d # バックグラウンドでコンテナを実行し、新しいコンテナ名を表示. この場合、docker-compose.ymlで定義されたすべてのコンテナ（サービス）を立ち上げる
```

コンテナの立ち上げ（Jupyterのみ）
```
docker-compose up -d jupyter # サービス名（コンテナ名）を指定
```

コンテナの消し方（down/stop）

```
docker-compose down # コンテナを停止し、docker-compose up で作成した コンテナ、ネットワーク、ボリューム、イメージを削除する
```

```
docker-compose stop # 「削除せずにコンテナを停止する」
```

Jupyter Notebookへのアクセス
```
http://localhost:8888 # 注 : Jupyter Notebook コマンドで起動した場合、コンテナ経由ではなく、直接ホストマシン上でJupyter Notebookを起動することになるため行わない
```

# その他メモ
- コンテナ内で立ち上げられたjupyter notebookのworkディレクトリがホストコンピュータのworkspaceにマウントしている
  - ので、work内に保存すれば、workspaceに保存される（逆も然り）

- ホストマシンのDockerデーモンが管理するDockerイメージのリスト
```
docker images
```

- docker imageの削除（コンテナが存在していると削除できない）
  - ```docker rmi [イメージID]```
  
- 動いているコンテナの確認
  - docker ps
  
- 停止しているコンテナの確認
  - docker ps -a

