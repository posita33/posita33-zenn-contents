---
title: "UnrealVS 拡張のインストール"
free: false
---

UnrealVS拡張というVisual StudioのExtensionが提供されています。
インストールしておくと便利なのでインストール方法と環境設定について紹介します。

https://docs.unrealengine.com/4.27/ja/ProductionPipelines/DevelopmentSetup/VisualStudioSetup/UnrealVS/

## UnrealVS 拡張のインストール

（バージョンのインストールフォルダ）/Engine/Extras/UnrealVS/VS2019
UnrealVS.vsixをダブルクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_01_vs2019_unreal_vs/2022-02-06-21-35-50.png)

[Install]ボタンをクリックするとインストールが始まります。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_01_vs2019_unreal_vs/2022-02-06-21-36-03.png)

インストールが完了したら[Close]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_01_vs2019_unreal_vs/2022-02-06-21-36-41.png)

nrealVS 拡張のインストールを確認します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_01_vs2019_unreal_vs/2022-02-06-21-37-16.png)
*Extensions > Manage Extensions*

InstalledをクリックするとUnrealVSがインストールされていることが確認できます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_01_vs2019_unreal_vs/2022-02-06-21-38-10.png)
*UnrealVSがインストールされていることが確認できる*

## UnrealVS 拡張の設定

### [Build Startup Project]コマンドの追加

ツールバーにUnrealVSを表示します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_01_vs2019_unreal_vs/2022-02-06-21-38-52.png)

ツールバーにUnrealVSが表示されたら、右クリックし、[Customize...]を選択します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_01_vs2019_unreal_vs/2022-02-06-21-39-17.png)
*ツールバーを右クリック > Customize…*

[Commands] > [Toolbar]から[UnreaVS]を選択し、[Add Command…]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_01_vs2019_unreal_vs/2022-02-06-21-43-27.png)
*Commands > ToolbarからUnreaVSを選択 > Add Command…*

[Extensions]を選択し、[Build Startup Project]を選択し、[OK]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_01_vs2019_unreal_vs/2022-02-06-21-43-53.png)
*Extensionsを選択 > Build Startup Projectを選択 > OKをクリック*

コマンドが追加されます。
必要なコマンドは追加しておいた方がよさそうです。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_01_vs2019_unreal_vs/2022-02-06-21-46-03.png)

ツールバーに追加したコマンドが表示されるようになりました。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_01_vs2019_unreal_vs/2022-02-06-21-46-28.png)

[Build Startup Project]コマンドはC++のソースコードをCompileする際に非常に便利なコマンドです。

### UnrealVS 拡張の設定やコマンドのショートカット登録

UnrealVS > General > Hide Non-Game Startup ProjectをTrueに設定します。
Gameのプロジェクトだけを表示する設定です。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_01_vs2019_unreal_vs/2022-02-06-21-49-45.png)

[Build Startup Project]のショートカットキーを設定します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_01_vs2019_unreal_vs/2022-02-06-21-49-59.png)

