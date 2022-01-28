---
title: "【BP】Actorクラスを作成する"
free: false
---

## Blueprintのクラス（親クラス：Actor）を追加する
Blueprintでクラスを作成します。
Blueprintを作成するフォルダを作成します。

![](https://storage.googleapis.com/zenn-user-upload/86f17b944b31-20220110.png)
*（プロジェクト名）/Blueprints*

新規Blueprintのクラスを作成するには何種類か方法があります。

- コンテンツブラウザのAddボタンから、[Blueprint Class]を選択する
- コンテンツブラウザの空きスペースを右クリック、[Blueprint Class]を選択する
- 左上のBlueprintsメニューから[New Empty Blueprint Class…]を選択する
- 
![](https://storage.googleapis.com/zenn-user-upload/8ac7cd070292-20220110.png)

次に親クラスを選択します。
[Actor]を選択します。

![](https://storage.googleapis.com/zenn-user-upload/9a1c44459ee9-20220110.png)

最後に名前を設定します。
名前を[BP_SampleActor]に設定します。

![](https://storage.googleapis.com/zenn-user-upload/3d0a675d639c-20220110.png)

## ファイル名やフォルダ構成はUE5-style-guideを参考にする

プロジェクト内で決まり事がなければ、名前の付け方や、フォルダの構成については[UE4-style-guide]を参考にしています。最新では[ue5-style-guide]になっていたのでこちらを参照した方が良さそうです。

https://github.com/Allar/ue5-style-guide

UE4-style-guideの方は日本語訳されている方がいます。UE4とUE5でそこまでまだ変更がないので十分役に立つ情報です。

https://github.com/akenatsu/ue4-style-guide/blob/master/README.jp.md
