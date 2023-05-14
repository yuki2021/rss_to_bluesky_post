# RSSをBlueskyに自動投稿するスクリプト

## 概要

基本的にはこちらの方のPythonスクリプトを参考に、RSSを読み込むようにしてlambdaで動くようにしただけ。

TwitterToBluesky - bluemo-public

https://scrapbox.io/blu3mo-public/TwitterToBluesky

## zipファイルにする方法

Python3.10をインストールしたローカル環境で次のようにコマンドを叩いていきます。（macのみ）

```
$ python -m venv venv
$ source venv/bin/activate
$ pip install -r requirements.txt
```

venv/lib/python<Pythonバージョン>/site-packagesディレクトリに移動し、Lambda関数のコードと同じディレクトリにすべての依存関係をコピーします。

最後にディレクトリをZIPファイルに圧縮します。

```
cd lambda_package
zip -r ../lambda_package.zip .
```

lambda関数を作成して、環境変数を設定する。

環境変数は下記。

- ATP_HOST
-- Blueskyのホスト名を記入する　例: https://bsky.social
- ATP_USERNAME
-- ユーザ名を入力する　例: yuki2021.bsky.social
- ATP_PASSWORD
-- パスワードを入力する
- RSS_FEED_URL
-- データを取りたいRSSフィードのURLを入力する　例: https://www.ituki-yu2.net/rss

後は、EventBridgeなりで動かせば指定の時間にブログの最新記事をBlueskyに投稿します。

## 注意点

- ランタイム設定のハンドラーは`bluesky_post.lambda_handler`です。
- タイムアウト時間は1分ぐらいです。