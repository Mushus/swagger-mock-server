# swagger-mock-server

github の webhook を設定してコミットしたら勝手に立つモックサーバー

## デプロイ

勝手にやってくれるから5分ほど待つんだ。

## 備考

サーバー立てる側には以下をインストールする必要がある

* docker
* docker-compose

そして　Amazon System Manager の Parameter Store に設定しておく  
キー名は `SSH_KEY` で入れる

```
# キーを作る
ssh-keygen -t ecdsa -b 521 -C "メールアドレスとかPCの名前とか" -f hoge
# hoge と hoge.pub ができる
cat hoge.pub | base64
# 標準出力する内容をコピペして Parameter Store に突っ込む
```

あと `TARGET_HOST` と `TARGET_USER` も合わせて入れる  
デプロイするサーバーには先程の `hoge.pub` を書き込んでおく

```bash
mkdir .ssh
chmod 700 ~/.ssh
hoge.pub >> .ssh/authorized_keys
chmod 600 ~/.ssh/authorized_keys
```

## その他

swagger のサンプルは公式の petstore。example の値が足りてなくてそのままでは動かないことに注意。  
ドキュメントは `-l html` で吐き出せるので将来的に吐き出したい。

gulp でファイル監視してドキュメントアップロードしたらサーバー立つとかも応用すればできるはず  
いまは時間ないのでやらない。