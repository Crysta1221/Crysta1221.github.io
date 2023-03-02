---
title: "【備忘録】矢がヒットしたプレイヤーを検知"
date: 2023-02-19T00:18:24+09:00
draft: true
slug: 23-03-02
categories:
    - コマンド
readingtime: false
---

## はじめに
お久しぶりです。クリスタです。今回は、「矢がヒットしたプレイヤーを検知」する方法をご紹介したいと思います。
実はもっと早くからこの方法を編み出していたのですが、ローカル環境でデバックした際村人では成功したのに対し、マルチ環境に移行させプレイヤーで試すと
コマンドが実行されないということに気づき修正するのにかなりの時間がかかってしまいました...(ただ、修正でもなぜこれで通ったかは私もわかりません)

## 方法とは...
前回は、効能付き矢`tripped_arrow`に色を付けて、そのNBTを読み取っていました。今回もある程度似ています。  
今回使うのは、同じく効能付き矢`tripped_arrow`に今度はプレイヤーに対する効果を付与し、その効果を得たプレイヤーを取得するという方法です。  
どういうこと...?ってなるかもしれません。つまりは、
```md
1. 効能付き矢に、前回のColor+effectをつける
2. effectはプレイヤーにヒットした際に/effect と同様の効果をもたらす
3. プレイヤーに付与したeffectをexecuteで検知し、そのプレイヤーに対し、矢をヒットしたことにする
```
という感じです。実際に例を紹介します。こちらは海外のYoutubeを参考にさせていただきました。

{{< youtube iIwh2sywDx0 >}}

こちらの概要欄にあったコマンドをこちらに表示します。
```mcfunction
#矢の取得
give @p minecraft:tipped_arrow{CustomPotionEffects:[{Id:27,Amplifier:68,Duration:1,ShowParticles:0b}],CustomPotionColor:16777215}

#リピートブロック、無条件、常時実行
execute if entity @e[nbt={HurtTime:10s,ActiveEffects:[{Id:27b,Amplifier:68b}]}] as @e[nbt={HurtTime:10s,ActiveEffects:[{Id:27b,Amplifier:68b}]}] run say 1
```
シングルワールドで、まず最初に矢を取得し、その後リピートコマンドブロックを`give`で取り出してコマンドを入れます。
その後、取得した矢をオフハンドに持ち、弓で村人に当てると、`[村人]1`とチャットに表示されます。  
この時、私は村人検知できたのならプレイヤーも行けるやろ理論でマルチ環境に移行し、知り合いとデバックしたところダメでした...
このコマンドの欠点はプレイヤーでは何もならないということです。では、どうすればプレイヤーも検知できるのか...
```mcfunction
#矢の取得
give @p minecraft:tipped_arrow{CustomPotionEffects:[{Id:27,Amplifier:68,Duration:1,ShowParticles:0b}],CustomPotionColor:16777215}
```
を、
```mcfunction
#矢の取得
give @p minecraft:tipped_arrow{CustomPotionEffects:[{Id:27,Amplifier:68,Duration:2,ShowParticles:0b}],CustomPotionColor:16777215}
```
に、
```mcfunction
#リピートブロック、無条件、常時実行
execute if entity @e[nbt={HurtTime:10s,ActiveEffects:[{Id:27b,Amplifier:68b}]}] as @e[nbt={HurtTime:10s,ActiveEffects:[{Id:27b,Amplifier:68b}]}] run say 1
```
を、
```mcfunction
#リピートブロック、無条件、常時実行
execute if entity @e[nbt={ActiveEffects:[{Id:27b,Amplifier:68b}]}] as @e[nbt={HurtTime:10s,ActiveEffects:[{Id:27b,Amplifier:68b}]}] run say 1
```
にしてください。何が変わったかというと、`HurtTime:10s`をなくし、また`Duration:`を1から2にしました。`HurtTime:`は傷ついたか判定で用いられるのですが、別になくしても問題なかったです。プレイヤーが検知できなかったのはおそらく、`Duration`つまりポーションの持続時間が1tickだったため、この1tickを検知できていなかった模様です。2tickにしたところなぜか動きました。なぜ動いたかは...不明です。(ここのところ有識者頼む...!)
## おわりに
いかがだったでしょうか？今回のこの方法もなかなかに使える場面が多いと思います。ぜひ活用してみてください!
次回の備忘録は未定ですが、そのうち私が引っ掛かったコマンドの罠でも書いておこうかと思います。では次回をお楽しみに!

## Tips
{{< notice tip >}}
コマンドを実行する前に`/`(スラッシュ)を必ず入れてください。ただし、データパックは`/`は必要ありません。
{{< /notice >}}

{{ template "_internal/disqus.html" . }}