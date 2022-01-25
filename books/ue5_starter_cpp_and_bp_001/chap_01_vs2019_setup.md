---
title: "1.2. Visual Studio 2019のセットアップ"
free: false
---

## Unreal Engine用にVisual Studioをセットアップ
公式ドキュメントにVisual Studioの設定手順が公開されています。
Unreal Engine 4.25以降はVS2019を使用するように書かれているので、VS2019を使用します。
2022年1月9日の段階ではVS2022が最新です。
https://docs.unrealengine.com/4.27/ja/ProductionPipelines/DevelopmentSetup/VisualStudioSetup/

### Visual Studioのインストール
Visual Studioの最新版は2022なので、2019をインストールするには少し手間がかかります。

https://visualstudio.microsoft.com/ja/dev-essentials/

[今すぐ参加またはアクセス]をクリックします。
![](https://storage.googleapis.com/zenn-user-upload/f9adbfe566ec-20220109.png)

Microsoftアカウントのログインが求められるので、Microsoftアカウントがない人は作成してください。

Visual Studio Communityのダウンロードをクリックします。
![](https://storage.googleapis.com/zenn-user-upload/554566f9f854-20220109.png)

検索バーから[Visual Studio Community 2019]を検索して、「Download」をクリックします。
![](https://storage.googleapis.com/zenn-user-upload/4027bdde2be3-20220109.png)

ダウンロードされたexeファイルを実行します。
![](https://storage.googleapis.com/zenn-user-upload/e7e70f36fca1-20220109.png)

Visual Studio Installerが立ち上がります。
[C++によるゲーム開発]を有効にして、開発に必要な項目を選択します。
![](https://storage.googleapis.com/zenn-user-upload/c4c6302f2b1e-20220109.png)


Visual Studio Installerが立ち上がります。
[C++によるゲーム開発]を有効にして、開発に必要な項目を選択します。
![](https://storage.googleapis.com/zenn-user-upload/43b6d23c3440-20220109.png)

英語UIで開発していきたい人は、言語パックの「日本語」を無効にし、「英語」のみを有効にします。
筆者は検索時に英語の方が見つかりやすいので英語UIを使って開発しています。この本も英語UIでVisual Studioの操作します。
![](https://storage.googleapis.com/zenn-user-upload/c2109f3e1a72-20220109.png)

Visual Studioを日本語のUIで開発したい方はこちらの記事を参考にしてください。
https://blog.siliconstudio.co.jp/2021/02/606/

英語と日本語が有効になっていると、ファイルの文字コードをShift-JISで作成してしまいます。
UnrealEngineは文字コードをUTF-8で処理するので、UE5側でコンパイルをした際に、エラーログにエラーが表示されますが、文字化けしてしまいます。
![](https://storage.googleapis.com/zenn-user-upload/81ce90f52e63-20220109.png)

[インストール]をクリックします。
![](https://storage.googleapis.com/zenn-user-upload/6511bfc9c6bd-20220109.png)

Visual Studioのインストールが開始されます。
![](https://storage.googleapis.com/zenn-user-upload/6f5f1c2214f2-20220109.png)

インストールが完了したら、再起動します。
![](https://storage.googleapis.com/zenn-user-upload/d3f3618d2b2b-20220109.png)

### デバッグに必要なエディタシンボルがインストールされているか確認する
デバッグに必要なエディタシンボルが入っているか確認しましょう。
EpicGamesLauncherの起動横の▼＞オプションから確認できます。
![](https://storage.googleapis.com/zenn-user-upload/d0f700672890-20220109.png)

デバッグに必要なエディタシンボルが入っていなかったら追加しましょう
![](https://storage.googleapis.com/zenn-user-upload/1b602710c3cf-20220109.png)

### C++プロジェクトを作成し、使用するエディタをVisual Studio 2019に設定する
C++プロジェクトを作成し、使用するエディタをVisual Studio 2019に設定する
FirstPersonテンプレートのC++プロジェクトを作成します。

- FirstPersonテンプレート
- C++
- StarterContent：オフ
![](https://storage.googleapis.com/zenn-user-upload/d5045357413a-20220109.png)

C++を書いていくエディターをVisual Studio 2019に設定します。
[Editor Preferences...]を開きます。
![](https://storage.googleapis.com/zenn-user-upload/8ebfecafcf8a-20220109.png)

SouceCodeカテゴリのSource Code Editorから[Visual Studio 2019]を選択します。
![](https://storage.googleapis.com/zenn-user-upload/29d4270cc1c9-20220109.png)


プロジェクトを再起動すると設定が反映されます。
![](https://storage.googleapis.com/zenn-user-upload/f8b41e7ffd2f-20220109.png)

Visual Studioでのソリューションファイルを更新しておきます。
![](https://storage.googleapis.com/zenn-user-upload/37699f524d94-20220109.png)

Visual Studio 2019でプロジェクトを開きます。
![](https://storage.googleapis.com/zenn-user-upload/f99e832c2da6-20220109.png)

Visual Studio 2019でC++のソースコードが編集できるようになります。
![](https://storage.googleapis.com/zenn-user-upload/995bb14db6cf-20220109.png)

### Visual Studioの推奨の設定

Solusion Configurationsの幅を広くします。
![](https://storage.googleapis.com/zenn-user-upload/866d344132a8-20220109.png)

Commandsタブを選択します。
Toolbarを[Standard]に変更します。
Solution Configurationsを選択し、[Modify Selection]をクリックします。
![](https://storage.googleapis.com/zenn-user-upload/0dae0f9fa21e-20220109.png)

Widthを200に設定します。
![](https://storage.googleapis.com/zenn-user-upload/392a757c3745-20220109.png)

Solusion Configurationsの一覧が見やすくなります。
![](https://storage.googleapis.com/zenn-user-upload/2220fba9348f-20220109.png)

> 通常、コードにエラーがあると エラー リスト(Error List) ウィンドウが自動的にポップアップします。しかし、UE の作業中に誤ったエラー情報が エラー リスト ウィンドウに表示され場合があります。UE で作業する際は、この エラー リスト ウィンドウをオフにして、出力 (Output) ウィンドウを使用して実際のコード エラーを確認することを推奨します。エラー リスト ウィンドウをオフにするには、次の手順に従ってください。
引用：Unreal Engine 用に Visual Studio をセットアップする

![](https://storage.googleapis.com/zenn-user-upload/a1372560fc8d-20220109.png)

Projects and Solutions > Generalの[Always show error list if build finishes with error （ビルドがエラーで終わった場合、常にエラー リストを表示する）]をオフに設定します
![](https://storage.googleapis.com/zenn-user-upload/f8f9311605e4-20220109.png)

出力 （Output） ウィンドウを使用して実際のコード エラーを確認することを推奨されています。
![](https://storage.googleapis.com/zenn-user-upload/791f9f0bba1e-20220109.png)

Visual Studio 2019側で、Build > Build Solutionを行うと、Outputウィンドウにエラー内容が表示されます。エラーの行をダブルクリックするとエラーの箇所に移動します。
![](https://storage.googleapis.com/zenn-user-upload/1eb2f13c8c73-20220109.png)

外部依存関係フォルダの無効化をします。
ソリューションエクスプローラで不要なフォルダを非表示にする。
![](https://storage.googleapis.com/zenn-user-upload/10b70f58a506-20220109.png)

次に有料のExtensionを使用するか使用しないかで変わってくるので別の項目に分けます。
