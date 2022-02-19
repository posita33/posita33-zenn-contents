---
title: "Unreal Engine 5のインストール"
free: false
---

:::message alert
Unreal Engine 5 早期アクセスで書いています。
今後正式版が出た時にUIの変更があります。
:::

## Unreal Engineの開発に必要なマシンスペック

:::message
UnrealEngineはグラフィックボードを積んだPCが必要になります。
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

## Unreal Engine 5早期アクセスをダウンロード

この本を執筆している段階ではUnreal Engine 5が早期アクセス（Early accessなのでEAと略されることもあります）です。正式版がリリースされたタイミングで入手方法が変わってきます。

![](https://storage.googleapis.com/zenn-user-upload/297c239ca9be-20220109.png)

インストールする際にオプションで以下の2つを有効にしてください。
C++の開発で必要になります。

- **エンジンソース**
- **デバッグに必要なエディタシンボル**

![](https://storage.googleapis.com/zenn-user-upload/452e4f1da6ca-20220109.png)

インストールする際にオプションを有効にし忘れても後からインストールできます。

![](https://storage.googleapis.com/zenn-user-upload/1f5a4151377c-20220109.png) 
*ライブラリタブの[UE5起動]ボタンの右側の▼をクリック > オプション*

## 一足先にUE5 正式版を試したい方

Unreal EngineはGitHubからソースコードを取得できます。「ue5-main」ブランチがUE5の正式版ソースコードになります。
一足先にUE5正式版を試したい方はコチラの記事を参考に試してみるのもおススメです。

https://zenn.dev/pokotaro/articles/7d60ecaf7a2f57


https://twitter.com/posita33/status/1490217759820890113


## オンラインラーニング：Unreal Engine 5クイックスタート

オンラインラーニングに[**Unreal Engine 5クイックスタート**]というチュートリアルがすでに用意されています。この本ではC++とBlueprintに焦点を当てていますので、何ができるのか興味がある方にはおススメのチュートリアルです。

![](https://storage.googleapis.com/zenn-user-upload/f18dff77aefb-20220109.png)

インストール方法やUIが少し見ない間に変わっていくので、最新の情報を入手してインストールしてください。EpicGames公式の情報を参考にすることをオススメします。

