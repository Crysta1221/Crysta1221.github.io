---
title: "【備忘録】弓ごとに別々の効果を発動させる"
date: 2023-02-18T00:18:24+09:00
draft: false
slug: 23-02-18
categories:
    - コマンド
readingtime: false
links:
  - title: 次回の記事はコチラから
    description: 【備忘録】矢がヒットしたプレイヤーを検知
    website: /p/23-03-02
---

## はじめに
お久しぶりです。クリスタです。今回は、「弓ごとに別々の効果を発動させる」という方法をご紹介したいと思います。
例えば、炎の弓、氷の弓、雷の弓のように弓を複数使うかつ別々の効果を起こしたい場合、それぞれどの弓から発射されたら炎にするかどうかを調べるのは
大変です。  
そこで今回は海外のサイトで見つけた方法をご紹介したいと思います。

## 方法とは...
具体的にどのようにして区別させるか...なのですが、今回はクロスボウを使います。なぜクロスボウかというと、クロスボウはコマンドで装填済みの矢を
決めることができます。そして今回はこの装填済みの矢のNBTを調べて区別するというわけです。
今回はクロスボウに`minecraft:tripped_arrow`を装填させます。この`tripped_arrow`は何かというと効能付き矢のことです。これはクリエイティブで実際に出すことができます。さらに、この効能付きの矢ですが、NBTに`color`というのがあります。これは効能付き矢の色を決めるものでRGBで決められます。この矢の色でどの効果をもたらすのかを判別します。  
ここで一つ難点があります。矢のNBTには`color`があるのですが、クロスボウには全く同じものはありません。Minecraftは、クロスボウの装填前の矢と発射後の矢でNBTが変わるという厄介な点があります。  
クロスボウで装填前の矢のNBTは、`{CustomPotionColor:255}`になりますが、発射されるとこれが、`{Color:255}`に変化します。  
まずは`{CustomPotionColor:255}`を設定したクロスボウを`give`で取得します。(このコマンドをコピー後、貼り付ける前に`/`を入れてください)
```mcfunction
give @p crossbow{ChargedProjectiles:[{id:"minecraft:tipped_arrow",Count:1b,tag:{CustomPotionColor:255}},{},{}],Charged:1b} 1
```
次にコマンドブロックを用意します。これも`give`で取得します。(このコマンドをコピー後、貼り付ける前に`/`を入れてください)
```mcfunction
give @p command_block
```
コマンドブロックの中は次のコマンドを入れてください。
```mcfunction
#リピート、常時実行
execute as @e[type=arrow,nbt={Color:255,inGround:1b}] at @s run <実行したい内容>
```
これは、`execute`で、色が255で地面に着いた矢としてコマンドを実行するものです。  
これを改造することでこんなこともできます。
```mcfunction
execute as @e[type=arrow,nbt={Color:255,inGround:1b}] at @s run summon armor_stand ~ ~ ~ {NoGravity:1b,Invulnerable:1b,Invisible:1b,Tags:["aqua"]}
execute as @e[type=armor_stand,tag=aqua] at @s run scoreboard players add @s Aqua 1
execute as @e[type=armor_stand,tag=aqua,scores={Aqua=..1200}] at @s run fill ~ ~1 ~ ~ ~ ~ water keep
execute as @e[type=armor_stand,tag=aqua,scores={Aqua=1200..}] at @s unless block ~ ~ ~ iron_bars run fill ~ ~1 ~ ~ ~ ~ air
kill @e[type=armor_stand,tag=aqua,scores={Aqua=1200..}]
```
上のコマンドはすべてデータパックでの活用例です。(一応一行ずつコマブロに移植することもできます)
```mcfunction
#配布用アイテム
give @p crossbow{ChargedProjectiles:[{id:"minecraft:tipped_arrow",Count:1b,tag:{CustomPotionColor:255}},{},{}],Charged:1b} 1
```
こちらは実際に動くために必要なクロスボウです。  
実際に使ってみると、着弾地点に水が生成されるようになります。(1分で勝手に消える仕様です)高いところに移動したりするのにすこ～し便利になりました。

## おわりに
いかがだったでしょうか？これだけでもいろいろなゲームを作ったりする際に少し便利になるのではないでしょうか...?  
実はこの`{inGround:1b}`、プレイヤーにヒットするのは検知できません。そのため、プレイヤーにヒットした場合は何も起こらないのが弱点です。次回はこの解決法もお教えしますのでお楽しみに...!

## Tips
{{< notice tip >}}
コマンドを実行する前に`/`(スラッシュ)を必ず入れてください。ただし、データパックは`/`は必要ありません。
{{< /notice >}}
