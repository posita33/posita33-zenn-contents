---
title: "【BP】Actorクラスを作成する"
free: false
---

## 【Blueprint】Actorクラスを作成する

Levelに配置できるActorクラスを作成します。

### 今回できること

BlueprintのActorクラスを作成できます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp_create_actor_class/2022-02-23-08-27-14.png)

## Blueprintのクラス（親クラス：Actor）を追加する

Blueprintでクラスを作成します。

### [Content Drawer]について

UE5から[Content Drawer]が実装されました。[Contents Drawer]は[Content Browser]と同様の働きをし、使わない時には非表示にできるので画面を広く使用できます。
[Content Drawer]や[Content Browser]はプロジェクトのアセットの管理がWindowsのエクスプローラのように操作できます。

「Contents Drawer」を表示するには、画面左下のタブをクリックするか、「Ctrl + Space bar」を入力します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp_create_actor_class/2022-02-23-08-07-11.png)
*Content Drawerを表示（Tabをクリック or Ctrl + Space bar）*

「Content Drawer」を非表示にするには、画面左下のタブをクリックするか、「Ctrl + Space bar」を入力します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp_create_actor_class/2022-02-23-08-08-19.png)
*Content Drawerを非表示（Tabをクリック or Ctrl + Space bar）*

### Blueprintを作成するフォルダを作成する

Blueprintを作成するフォルダを作成します。

フォルダは[Content Browser]の左側のフォルダアイコンがある項目を右クリック > [New Folder]を選択すると追加できます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp_create_actor_class/2022-02-23-08-10-03.png)

図のような構成になるようにフォルダ名を作成して名前を設定します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp_create_actor_class/2022-02-23-08-10-52.png)
*Content/（プロジェクト名）/Blueprints*

新規Blueprintのクラスを作成するには何種類か方法があります。

- [Content Browser],[Content Drawer]のAddボタンから、[Blueprint Class]を選択する
- [Content Browser],[Content Drawer]の空きスペースを右クリック、[Blueprint Class]を選択する
- 左上のBlueprintsメニューから[New Empty Blueprint Class…]を選択する

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp_create_actor_class/2022-02-23-08-17-35.png)

次に親クラスを選択します。
[Actor]を選択します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp_create_actor_class/2022-02-23-08-18-29.png)

最後に名前を設定します。
名前を[BP_HelloWorld]に設定します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp_create_actor_class/2022-02-23-08-20-05.png)

### すべて保存する

Blueprint側の説明はここまでになります。
[Content Browser]から[Save All]ボタンをクリックし、[Save Selected]ボタンをクリックしてプロジェクトの変更のあったアセットをすべて保存します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp_create_actor_class/2022-02-23-08-23-16.png)

## ファイル名やフォルダ構成はUE5-style-guideを参考にする

プロジェクト内で決まり事がなければ、名前の付け方や、フォルダの構成については[UE4-style-guide]を参考にしています。最新では[ue5-style-guide]になっていたのでこちらを参照した方が良さそうです。

https://github.com/Allar/ue5-style-guide

UE4-style-guideの方は日本語訳されている方がいます。UE4とUE5でそこまでまだ変更がないので十分役に立つ情報です。

https://github.com/akenatsu/ue4-style-guide/blob/master/README.jp.md
