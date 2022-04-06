---
title: "Unreal Engine 5のインストール"
free: false
---

:::message alert
Unreal Engine 5 早期アクセスで書いています。
今後正式版が出た時にUIの変更があります。
:::

:::message
2022/2/23 Unreal Engine 5 Preview 1が使用できるようになりました。
Unreal Engine 5 早期アクセスで書かれているので一部UIが違います。
随時更新します。
:::

## Unreal Engineの開発に必要なマシンスペック

:::message
UnrealEngineはグラフィックボードを積んだPCが必要になります。
SSDやHDDの空き容量も100GBくらい余裕がある状態であることを確認してください。
:::

公式ドキュメントのマシンスペックを確認してから始めてください。
UnrealEngine5では標準プロジェクトでLumenが使われるので、DirectX 12 対応のグラフィックボードを積まないとクラッシュします。

https://docs.unrealengine.com/4.27/ja/Basics/InstallingUnrealEngine/RecommendedSpecifications/

## EpicGamesLauncherのインストール

UnrealEngineを使用するにはEpicGamesLauncherをインストールします。

https://www.unrealengine.com/ja/download  

ダウンロードページに移動したら「**パブリッシングライセンス**」の方の「今すぐダウンロード」をクリックします。

![パブリッシングライセンスを選択する](https://storage.googleapis.com/zenn-user-upload/5522cb1f5d53-20220109.png)

次のページが表示されると「EpicGamesLauncher」のインストーラーがダウンロードされます。
ダウンロードしたページにUnrealEngineのインストール方法についての動画が公開されています。インストール方法は見るタイミングによって変わっているので、公式が提供している動画を参考にする方がいいです。

![](https://storage.googleapis.com/zenn-user-upload/49d8d3543a4d-20220109.png)

## Unreal Engine 5 をインストールする

EpicGamesLauncherの[Unreal Engine]タブから[ライブラリ]に移動します。
Engineバージョンの[+]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_01_ue5_install/2022-02-23-04-55-30.png)

バージョンが書かれている▼の個所をクリックするとインストールするバージョンが選べます。
[5.0.0]を選択します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_01_ue5_install/2022-04-06-22-44-22.png)

[インストール]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_01_ue5_install/2022-04-06-22-45-45.png)

[オプション]をクリックします。

:::message
C++の開発をしない方はこのままインストールボタンをクリックして大丈夫です。
:::

![](/images/books/ue5_starter_cpp_and_bp_001/chap_01_ue5_install/2022-04-06-22-47-00.png)

[デバッグに必要なエディタシンボル]を有効☑にし、[適用]ボタンをクリックします。

C++の開発では以下の2つの項目は必要になります。

- **エンジンソース**
- **デバッグに必要なエディタシンボル**

![](/images/books/ue5_starter_cpp_and_bp_001/chap_01_ue5_install/2022-04-06-22-49-54.png)

[インストール]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_01_ue5_install/2022-02-23-05-05-31.png)

Unreal Engine 5のインストールが開始されます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_01_ue5_install/2022-04-06-22-50-32.png)

## オンラインラーニング：Unreal Engine 5クイックスタート

オンラインラーニングに[**Unreal Engine 5クイックスタート**]というチュートリアルがすでに用意されています。この本ではC++とBlueprintに焦点を当てていますので、何ができるのか興味がある方にはおススメのチュートリアルです。

![](https://storage.googleapis.com/zenn-user-upload/f18dff77aefb-20220109.png)

インストール方法やUIが少し見ない間に変わっていくので、最新の情報を入手してインストールしてください。EpicGames公式の情報を参考にすることをオススメします。

