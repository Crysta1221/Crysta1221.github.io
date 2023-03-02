---
title: "Optifine導入解説"
date: 2023-02-07T00:18:24+09:00
draft: false
slug: Optifine-intro
image: optifine.png
categories:
    - Minecraft
readingtime: false
---
{{< notice note >}}
このブログは、Qiitaから移行されたものです。Qiita版をご覧になりたい場合は、以下のURLよりアクセスしてください。  
https://qiita.com/Crysta1221/items/810fa69d8d537054bec1
{{< /notice >}}

# はじめに
どうもみなさんこんにちは。クリスタです。今回は、「徹底解説! Optifineの導入方法編」ということで、今更ほかのブログでやり方公開されてるのにわざわざ導入方法を書く必要なくね?と思う方も多いはず。
しかし! どのブログも「<font color="Red">**Optifineの導入に失敗した際の対処法**</font>」が少なすぎる!
なので、今回は導入の解説もしつつ、失敗した際のパターンをほぼすべてに焦点を当てて解説をする回です。では早速行きましょう!

## 1. Javaをインストール
ということで、まずはOptifineの導入に必須のJavaから入れていきましょう。すでにパソコンにJavaが入っているという方はこの項目をスキップしてください。
今回は以下のページからインストールしていきます。
[Javaのホームページ](https://www.java.com/ja/download/)
このページにまずはアクセスしましょう。ブラウザは、サポートの切れたInternet Explorer以外なら何でもいいです。下のようなページに飛ぶはずです。
![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/2467860/713b6a8f-44fe-a522-d997-4c98c4b8ae39.png)
この、赤枠の「Javaをダウンロード」というボタンをクリックしてください。ダウンロードされます。
![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/2467860/798bd9dc-c2f2-a6f6-f73c-f33cd431110f.png)
Chrome系は上の画像のように<font color="red">左下にダウンロードしたファイルが表示されます</font>。
一方、Edgeだけは特殊で、右上あたりにダウンロードするのがあるんですよね...中身は同じなのにめんどくさいですね。
とりあえずダウンロードできたら、そのファイルをクリックします。エクスプローラーを開かずに、ブラウザでダウンロードしたファイルが表示されているはずなのでそのファイルをクリックすることで簡単に開けます。

{{< notice warning >}}
ここから先は管理者の権限が必要です。
{{< /notice >}}

インストールには、管理者権限が必要です。これは不必要にアプリをインストールできないようにする保護機能なので管理者でログインしている場合は、UAC(ユーザーアカウント制御)という「はい」か「いいえ」で選ぶ画面が出てくるはずです。一方、標準ユーザーの場合はここでパスワードが必要です。もし、親が管理しているパソコンであれば、パスワードが必要になることが多いので許可を取ってパスワードを入れてもらいましょう。
実行するとこんな画面が出てきます。
![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/2467860/545c32c6-e38c-0a71-4526-6e619a54c5c9.png)
まずはライセンス条項を読みましょう。これは、Javaの利用規約で、簡単に言うと、
```
このJavaは商用利用ダメだから個人で利用してね! 
Javaをインストールしてエラーが起きたらエラーの内容をOlacle(Java開発元)に送るかもだけど
その情報の取り扱いについて書いてるから同意するかい? 同意するならインストールボタン押してね!
```
という感じです。軽めに書いてますがちゃんと読みましょう。同意する場合は、「インストール」ボタンを押しましょう。逆に同意しない場合、こっから先には進めないというのは察しがつくと思います。
Javaのインストール完了 という画面が出たら、その画面を閉じましょう。さて、Optifine入れよう!と進めがちですが、**一旦パソコンを再起動**しましょう。理由は、Javaをインストールした際、そのインストールを必ず適用させるため(つまり失敗しないようにするため)です。中途半端にインストールしてしまうと、Optifineが入らない可能性があります。再起動できたら、次の項目へレッツゴー!

## 2. Optifineの導入
さて、今回の山場Optifineの導入に行きます。ここからは完全に**パソコンとJavaの相性**により、方法が変わります。とりあえず、Optifineをダウンロードしてしまいましょう。以下のページに移動してください。
[Optifine公式ページ](https://optifine.net/downloads)
こんなページになります。
![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/2467860/31f46862-7d6f-c448-e343-c76ae0313651.png)
ここから、あなたのバージョンにあったOptifineを入れていくわけですが、今のMinecraftで最新のバージョンは、 `1.19.1` です。1.19あるいは1.19.1を入れる場合はそのままでよいわけですが、1.19より前のバージョンはどこ?と思うかもしれません。そのページに「Show all versions」というリンクがありますのでそれを押しましょう。
![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/2467860/1757c2d6-b8d8-9f3f-789f-24c4647be000.png)
そうすると、いろいろなバージョンが表示されるようになります。今回は例として、 `1.16.5` で解説しますが、どのバージョンでもやり方は同じですのでやり方としてご覧ください。
![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/2467860/e7762219-ddde-9562-a24a-30e031b9ba90.png)

目的のバージョンのところに「Download」というボタンがあります。ここをクリックしてください。

{{< notice info >}}
この後のページは広告が表示されます。ですのでこのページに書いてある方法に従ってください。変にクリックするだけで広告のページに飛ばされる恐れがあります。その際は落ちついてその広告ページのタブを閉じれば問題ありません。
{{< /notice >}}


注意にもある通りここから先は広告が表示されます。
![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/2467860/7a6d9d6c-345b-2eed-0a09-615baf2d2211.png)
私は、Braveという広告をブロックしてくれるブラウザを使っているので真っ白ですが真っ白のところにでかでかと広告が載ってるはずです。どこ押せばいいんや!となりますが、右上に注目。小さく、「Please wait 5 seconds.」と書かれていますね。はい、察しがつくと思いますが、5秒待たないとスキップできません。Youtubeの広告みたいですね。
![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/2467860/05bb40de-a61b-fbb1-6ad9-f7a25baac877.png)
5秒待つと、右上に「Skip」というボタンが表示されるようになりますのでクリックしましょう。
![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/2467860/ad635e17-6dbd-2018-d28f-b3a5ee14676f.png)
そうすると、このような画面になりますので今度こそ「Download」ボタンをポチりましょう。
さっきJavaをダウンロードしたみたいにダウンロードしたファイルが表示されます。では、こっからが山場です。相性が良ければ、さっきのようにファイルをクリックすると、
![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/2467860/c952bc13-d76b-3a50-2d65-46ba0ed79ae7.png)
このような画面になります。もし、このような画面になれば、Optifine Installerが表示された場合をご覧ください。それが表示されない場合は、下から該当する現象に合う項目を探してその方法を試してください。該当するものがない場合はまずは、`クリックしても反応しない、一瞬黒い画面が出る、プログラムから選択が出る`をご覧ください。

<details><summary>Optifine Installerが表示された場合</summary>

成功です! やりましたね! [3.起動構成の変更](#3-起動構成の変更) に移動して、残りの設定を済ませてしまいましょう。

</details>

<details><summary>クリックしても反応しない、一瞬黒い画面が出る、プログラムから選択が出る</summary>

残念ながら、Javaとの相性が良くないようです。JDKを入れてみましょう。今回は、Adopt Open JDKというものを使います。本当は、Olacle のOpen JDKを使ってもいいのですが、Javaのバージョン管理が簡単なAdopt Open JDKがおすすめなのでこちらで。
[Adopt Open JDKのページ](https://adoptopenjdk.net/)
![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/2467860/b42a2f1f-7fdb-2798-2e59-fece4d1d26d7.png)
このページに移動したら、まずは、1. Choose a version という項目があるので、それを一番下の「Open JDK 16(Latest)」にします。「Open JDK 16(Latest)」をクリックすると、選択できます。2はそのままでOKです。
![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/2467860/cfee6388-4859-f5db-b9de-fc040f0a1067.png)
上のようになったら、あとは赤枠のボタンを押してください。
![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/2467860/f48b6353-8d3e-d032-dfa4-2af68fe343aa.png)
今度はこんなページに飛ばされます。少し下にスクロールして下の画像と同じ場所まで移動してください。
Windowsの場合は、Windows x64 というものを探します。ここではWindowsで説明します。Mac、Linuxの場合も同様に探してください。
![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/2467860/f13ca58a-8692-8680-b224-411fe8c501c9.png)
Windowsの場合、上の画面まで行けたら、「Msi」というボタンを押してください。Msiというのはインストーラのことで、自動でJavaを入れてくれる便利なものです。ZipはインストールするものでなくJavaをそのままZipにしただけのものです。クリックすると、1.同様にダウンロードされます。またそれをクリックして実行します。
これも管理者権限が必要です。実行すると、以下の画面になります。
![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/2467860/2ca5c7c9-f392-ec2c-f3e2-225d0421f8fc.png)
Adopt Open JDK 11の画面ですが、16も変わりはありません。「次へ」をクリックします。
![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/2467860/c00c8ba4-160e-1e96-5dbe-4bff5e9bad20.png)
まず、`Set JAVA_HOME variable` を有効にします。×ボタンをクリックして、`ローカルハードドライブにインストール` をクリックして有効にします。
次に、その下、`JavaSoft(Olacle) registory keys` も同じようにしてローカルハードドライブにインストールにしてください。その後、「次へ」をクリックし、その後「インストール」をクリックしてください。
これで、Adopt Open JDKがインストールされます。インストール完了と表示されたらまたパソコンを再起動します。再起動後、エクスプローラーを開きます。その後、ダウンロードをクリックします。
![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/2467860/67b4924b-634b-9a87-9f7d-080af7bb4584.png)
その中にある、「Optifine～」で始まるファイルを探します。
![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/2467860/51e81979-05ad-f00f-fdc3-2619ff793ab9.png)
見つかったらダブルクリックして開きます。もし、成功していれば、2.Optifineの導入の一番下にある画像のようなものが表示されるはずです。それでもダメな場合、次の項目「Adopt Open JDKでも失敗する」を参照してください。
</details>

<details><summary>Adopt Open JDKでも失敗する場合</summary>

今後はコマンドプロンプトを使います。前提として、Javaのインストールが完了していることです。
まずは、WindowsキーあるいはWindowsの画面の左下にあるスタートボタンを押します。その後、`cmd` と入れると、`Windows コマンドプロンプト`というのが検索に引っ掛かりますのでそれをクリックするか、「開く」で開いてください。
![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/2467860/63a55130-25bf-0090-76bb-349ac8baafb6.png)
こんなちょっとかっちょいい画面が出てきましたか? そうしたら、試しにどのように使うかデモンストレーション代わりに以下のコマンドを入れてみましょう。
```bat
java -version
```
入れたら、Enterで実行します。そうすると、Javaのバージョンが表示されるはずです。私の場合、
```cs
openjdk version "16.0.2" 2021-07-20
OpenJDK Runtime Environment Temurin-16.0.2+7 (build 16.0.2+7)
OpenJDK 64-Bit Server VM Temurin-16.0.2+7 (build 16.0.2+7, mixed mode, sharing)
```
と表示されます。`'java' は、内部コマンドまたは外部コマンド、操作可能なプログラムまたはバッチ ファイルとして認識されていません。` と表示された場合、まずJavaのインストールをしていないか、失敗しているかの2択ですのでインストール/再インストールをしましょう。再インストールは一度Javaをアンインストールしてから再度インストールすることです。もし、Javaのバージョンが表示されたら、次は以下のコマンドを入れましょう。
```bat
java -jar
```
これを入れたら、`-jar`の後にスペースを押してください。その後、Optifineのファイルをコマンドプロンプトの画面にドロップします。どうドロップするか。Optifineのファイルをクリックしたまま、コマンドプロンプトの画面までマウスカーソルを移動させ、コマンドプロンプトの画面のどこかにマウスカーソルが来たら、離します。そうすると全体のコマンドは以下のようになるはずです。
```bat
java -jar c:\Users\<パソコンのユーザ名>\Downloads\Optifine~ .jar
```
こうなってたらOKです。Enterを押してください。そうすると、2.Optifineの導入の一番下のOptifine Installerという画面が出るはずです。
もし、これをやっても無理!という場合はコメント欄に「やったこと」を記述し可能であればスクショを添付していただくと説明します。
</details>

<details><summary>Javaをインストールできません。スイッチに失敗しましたと表示された場合</summary>

Javaのインストールが完了していないまま続行したためJarファイルを開けなくなっています。一度コントロールパネルからJavaをアンインストールし、再度インストールしてみてください。

</details>

## 3. 起動構成の変更
さて、今回の山場は過ぎました。ここで注意し忘れていたのですが、

{{< notice warning >}}
Optifine Installerを起動する前に、一度マイクラのランチャーからそのバージョンを起動している必要があります。つまり、1.16.5のOptifineを入れる場合は、1.16.5のマイクラを起動している必要があります。
{{< /notice >}}

こういうことです。起動したらもう閉じてOKです。その後、Optifine Installerの「Install」というボタンを押します。 `Install Optifine~ successly!` みたいに表示されたらOptifineの導入は終わりです。お疲れ様でした。後は、マイクラのランチャーとマイクラの画面を閉じて、ランチャーを起動すると、起動構成にOptifineが追加されています。
さて、終わりでもいいのですが、複数のOptifineを利用する予定の場合は、フォルダ分けをしてしまいましょう。
ランチャーを開き、起動構成に移動します。
![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/2467860/e410c52b-0131-1ae1-aede-bd10d35ec02a.png)
こうすると、Optifineの起動の設定ができます。
![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/2467860/82114994-8b85-ac56-00b2-63e86dc9913f.png)
重要なのはゲームディレクトリです。既定のディレクトリにすると、いちいち起動構成を変更する必要があります。また、リソパの管理、マイクラのバージョン管理も面倒になります。参照ボタンを押すと、
![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/2467860/e5556680-b2bb-21f6-503f-b60f6e59cb98.png)
このようになりますので、まずは、`Roaming` というフォルダをクリックし、「新しいフォルダを作成」ボタンを押して、フォルダを作成します。フォルダの名前はわかりやすいものがいいです。作成したら、作成したフォルダを選択して、「OK」を押します。その後、ゲームディレクトリや名前、バージョンなどの画面になったら「保存」ボタンを押します。これで再度「プレイ」を押すことで今度こそ導入は終わりです。お疲れ様でした!

## 4. 終わりに
いかがでしたか?無事Optifineは入れられましたでしょうか? 一応失敗する方向けに書かせていただきましたが、もしここに書いてる方法でもうまくいかない場合は、プロフィールのお問い合わせよりお願いします! Twitterもやっていますのでフォローのほどよろしくお願いします。
それでは次回でお会いしましょう!

