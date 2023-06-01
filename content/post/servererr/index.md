---
title: "Minecraftのサーバー接続エラー解説"
date: 2023-04-02
draft: false
slug: server_err
image: optifine.png
categories:
    - Minecraft
readingtime: false
---

## はじめに
お久しぶりです。クリスタです。今回は、「Minecraftにおけるサーバーの接続エラーを解説」する回でございます。
自分がよくいる鯖がアップデートされてサーバーのエラーがここ最近出るようになったのである程度解説しておけば怖くはないかなと思ったのでぜひ最後まで見ていただけると幸いです。

## エラー一覧
### <h4><font color="Red">Could not connect to a default or fallback server.Incorrectly configured address/port/firewall?</h4></font>

このエラーはサーバーが、複数のサーバー間を移動できるプラグイン「BungeeCord」や「Waterfall」を導入していてその設定がミスっている際によく起こります。そのため、クライアント側ではなくサーバー側の問題なので修正されるのを待ちましょう。

### <h4>java.net.ConnectException: Connection timed out: no further information</h4>

このエラーは、`Commection timed out` サーバーへの接続先が見つからなかった...ということです。つまり、接続しようとしてたアドレスが存在しないか、サーバーがまだ起動していないことを指しています。`nor further information`はこれ以上の情報が見つからなかったことを指しています。

### <h4>Connection refused: no further information</h4>

このエラーは接続しようとしたサーバーが接続を拒否したために発生するエラーです。なぜ拒否されたかは`no further information`により不明です。これはサーバー側のエラーのことが多いです。

### <h4>プロフィール公開鍵が失効しています~...</h4>

このエラーは接続先のサーバーが1.19以上で発生しやすいです。1.19以降チャットの通報機能が強化されたため署名機能も追加されました。クライアント側のMinecraftとMinecraft Launcherの再起動で直ることが多いです。

### <h4><font color="red">Kicked by Whilist</h4></font>

これはおなじみホワイトリストに存在しないためキックされたというメッセージですね。ホワイトリストは、管理者しか追加できないのでもしなかったら管理者の人に聞いてみましょう。

## おわりに
とりあえず、よく出そうなメッセージだけを解説しました。他にもこのメッセージってどういうこと!?などありましたら、このページの一番最後にコメントを書くことができますので可能な限りスクリーンショットとどうしたらそうなったのかを入れてもらえれば私が時間のある時に答えると思います。それではまた次回お会いしましょう!