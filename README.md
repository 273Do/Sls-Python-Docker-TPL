# Serverless-Python(Flask)-Docker-Template

ローカルの Docker 環境で AWS Lambda(Serverless Framework)と Python(Flask)でサーバーレス API を実装，デプロイします．

# 使い方

1.  リポジトリを用意しましたのでクローンしてください．

2.  `docker-compose.yml`の`container_name`にコンテナ名を設定し，`docker compose build` で Docker イメージを構築します．

3.  `docker compose up -d`でデタッチドモードでコンテナを起動します．

4.  `docker exec -it 設定したコンテナ名 /bin/bash`でコンテナの中に入ります．

5.  `serverless` でプロジェクトを作成します．

    1. 今回は Flask で実装してみたいので`AWS / Python / Flask API`を選択します．
    2. プロジェクト名を設定します．
    3. Serverless Framework のログインを求められますので，表示されたリンクからログインしてください(`Login/Register`を選びます)．
    4. アプリを作成するか既存のアプリを選択するか聞かれますのが，`Skip Adding An App`を選択します．
    5. AWS の認証を求められますので，`Save AWS Credentials in a Local Profile`を選択して事前準備で用意したアクセスキーを入力します．
    6. 作成されたディレクトリに移動し，`npm i`を実行します．

6.  `serverless.yml`で Python のバージョン(`runtime`の部分)を`python3.9`に変更し，`custom`の`wsgi`に`pythonBin: /usr/bin/python3`を追加します．

7.  `docker-compose.yml`にのコメントアウトされている部分を解除し，`FLASK_APP`に app.py のパスを指定します．

8.  `exit`でコンテナから抜け, `docker compose down`でコンテナの終了させます．

9.  `docker compose up`でコンテナ内の flask アプリがローカルで起動します．この時点で http://localhost:5000 を GET メソッドで叩くと，json で`Hello from root!`とレスポンスが返ってきます．

10. コンテナの中に入って，`aws configure`コマンドで AWS の認証をしておきましょう．region(AWS サーバー)や output format(デフォルトは json)はお好みでどうぞ．

11. デプロイする時はコンテナの中に入り，`serverless.yml`のあるディレクトリに移動し，`sls deploy`を実行します．すると AWS に自動でデプロイされます．デプロイ後，ターミナルにデプロイ先のリンクが表示されます．AWS コンソールからも確認できます．また，Lambda と API Gateway が作成，接続されているのを確認できます．
