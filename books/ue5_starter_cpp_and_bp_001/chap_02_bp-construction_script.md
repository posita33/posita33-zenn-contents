---
title: "【BP】Construction Script"
free: false
---

## 【Blueprint】Construction Script

### 今回できること

今回はConstructionScriptを使用して、Level EditorのDetailパネルでPointLightのプロパティを変更します。

ConstructionScriptタブはPlayが実行される前に、配置したActorのComponentの設定を確認しながら変更する処理が書けるタブです。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-construction_script/2022-02-24-06-54-57.png)

変数の目のアイコンを有効にする（Instance Editableを有効にする）とLevelEditorの[Details]パネルでViewportに配置後でも、値を変更できます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-construction_script/2022-02-24-06-52-31.png)

### 学習用の新規レベル「Chapter_2_ConstructionScript」を作成する

学習用に新規レベルを作成します。
[File]から[New Level…]を選択します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-02-23-11-21-55.png)

[Basic]を選択し、[Create]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-02-23-11-23-32.png)

[File]メニューからCurrent Levelを保存します。
ショートカット「Ctrl + S」でも保存できます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-02-23-11-24-39.png)

「Maps」フォルダを選択し、Nameに「Chapter_2_ConstructionScript」を入力し、[Save]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-construction_script/2022-02-24-05-42-40.png)

### Blueprintを複製する

「BP_Component」を複製（Ctrl + W）して、「BP_ConstructionScript」を作成します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-construction_script/2022-02-24-05-45-09.png)

### LevelEditorで編集可能な変数を追加する

追加したComponentをLevelに配置してから、BlueprintのConstruction Scriptを使用してプロパティを変更します。

「BP_ConstructionScript」をダブルクリックしてBlueprint Editorを開きます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-construction_script/2022-02-24-05-46-30.png)

PointLightのプロパティをBlueprintのConstruction Scriptから変更するための変数を作成します。

| VariableName | VariableType           | 変数の概要                               |
| ------------ | ---------------------- | ---------------------------------------- |
| IsVisible    | Boolean                | PointLightの表示（true）/非表示（false） |
| Intensity    | Real(Float)            | PointLightの光の強さ                     |
| LightColor   | Linear Color Structure | PointLightの色                           |


![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-construction_script/2022-02-24-05-50-14.png)

追加した変数にCategoryを設定します。

- Category：Point Light

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-construction_script/2022-02-24-05-52-48.png)

変数[IsVisible]の右側「目のアイコン」をクリックし、「目が開いた状態」に設定します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-construction_script/2022-02-24-06-08-40.png)

変数[Intensity]は[Details]パネルの[Instance Editable]をチェックします。
変数[Intensity]の「目のアイコン」が「目を開いた」状態になります。
「目のアイコン」は[Instance Editable]が有効/無効を表しています。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-construction_script/2022-02-24-06-12-15.png)

変数[LightColor]の「目のアイコン」を開いた状態にします。
すべての変数の目が開いた状態になりました。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-construction_script/2022-02-24-06-13-42.png)

[Compile]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-construction_script/2022-02-12-09-07-39.png)

LevelEditorに戻り、「BP_ConstructionScript」をViewportにDrag&Dropします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-construction_script/2022-02-24-06-15-15.png)

「BP_ConstructionScript」の[Details]パネルに「Point Light」と書かれたCategoryが表示されます。
先ほど追加した変数が表示されています。
変数の「目のアイコン」が開いた状態では、LevelEditorの[Details]パネルから変数の値を設定できます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-construction_script/2022-02-24-06-18-50.png)

### ConstructionScriptでPointLightの表示/表示を設定する

[Derail]パネルに表示された変数を使用して、Point Lightのプロパティを変更できるようにします。
「BP_ConstructionScript」をダブルクリックしてBlueprint Editorを開きます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-construction_script/2022-02-24-06-20-03.png)

Construction Scriptタブを開きます。
[Construction Script]ノードが今回やることのStartになるノードです。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-construction_script/2022-02-24-06-22-35.png)

[Components]パネルからPointLightをDrag&Dropします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-construction_script/2022-02-24-06-23-54.png)

PointLightのGetノードからDrag&Dropし、[Set Visibility]を選択します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-construction_script/2022-01-27-13-24-43.png)

変数[IsVisible]のGetノードを追加します。
[Set Visibility]ノードの[New Visibility]ピンとGetノードを接続します。
[Construction Script]ノードの実行ピンを[Set Visibility]ノードの実行ピンに接続します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-construction_script/2022-02-24-06-27-21.png)

[Compile]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-construction_script/2022-02-12-09-07-39.png)

[Details]パネルの変数[IsVisible]を有効/無効にすることで、Point Lightの表示/非表示を制御できます。
ConstructionScriptに処理を書くことで、Viewportに配置してからのComponentの設定を変更できます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-construction_script/2022-02-24-06-31-35.png)

処理が書けたのでコメントボックスを追加しましょう。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-construction_script/2022-01-27-13-25-36.png)

### ConstructionScriptでPointLightのIntensity（光の強さ）を調整をする

次にPointLightのIntensity（光の強さ）を調整します。
Componentの[PointLight]と変数[PointLight]のGetノードを追加します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-construction_script/2022-02-24-06-34-19.png)

[PointLight]のGetノードからDrag&Dropし、[Set Intensity]を選択します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-construction_script/2022-01-27-13-26-04.png)

変数[Intensity]のGetノードと[Set Intensity]ノードのNew Intensityピンを接続します。
[Set Visibility]ノードの実行ピンと[Set Intensity]ノードの実行ピンを接続します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-construction_script/2022-02-24-06-37-11.png)

[Compile]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-construction_script/2022-02-12-09-07-39.png)

[Details]パネルの変数[Intensity]の数値を大きくすると光が強くなります。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-construction_script/2022-02-24-06-39-08.png)

変数[Intensity]のDefault Valueに数値[5000.0]を設定します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-construction_script/2022-01-27-13-26-54.png)

[Compile]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-construction_script/2022-02-12-09-07-39.png)

変数[Intensity]の矢印ボタンをクリックします。
設定した値をDefault Valueに戻ります。
ConstructionScriptで設定できるようにすると最初の状態に戻したい時が出てきます。最初の状態へ戻すためにDefault Valueを設定しましょう。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-construction_script/2022-02-24-06-42-21.png)

処理が書けたのでコメントボックスを追加しましょう。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-construction_script/2022-01-27-13-27-27.png)

### ConstructionScriptでPointLightのLightColorを調整をする

次にPointLightのLightColor（光の色）を調整します。
Componentの[PointLight]と変数[LightColor]のGetノードを追加します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-construction_script/2022-02-24-06-44-11.png)

変数[LightColor]のGetノードからDrag&Dropし、[Set Light Color]を選択します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-construction_script/2022-01-27-13-27-52.png)

変数[LightColor]のGetノードと[Set Light Color]ノードのNew Light Colorピンを接続します。
[Set Intensity]ノードの実行ピンと[Set Light Color]ノードの実行ピンを接続します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-construction_script/2022-01-27-13-28-03.png)

[Compile]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-construction_script/2022-02-12-09-07-39.png)

[Details]パネルの変数[LightColor]を変更することで、PointLightの色を変更できます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-construction_script/2022-02-24-06-48-31.png)

処理が書けたのでコメントボックスを追加しましょう。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-construction_script/2022-01-27-13-28-27.png)

### ConstructionScriptの振り返り

変数の目のアイコンを有効にする（Instance Editableを有効にする）とLevelEditorの[Details]パネルでViewportに配置後でも、値を変更できます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-construction_script/2022-02-24-06-52-16.png)

BlueprintのConstructionScriptでは、LevelEditorの[Details]パネルの変数の変更をViewportに配置したActorに対して反映できます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-construction_script/2022-01-27-13-30-09.png)

Web上でBlueprintを共有できるサイトがありますので、今回のBlueprintを共有しています。

https://blueprintue.com/blueprint/69vrgwy-/

[Set Visibility]ノードはPointLightの表示/非表示を設定できます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-construction_script/2022-01-27-13-30-59.png)

[Set Intensity]ノードはPointLightの光の強さを設定できます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-construction_script/2022-01-27-13-31-10.png)

[Set Light Color]ノードはPointLightの光の色を設定できます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-construction_script/2022-01-27-13-31-27.png)

Actorを親に選択したBlueprintEditorは最初[EventGraph]タブと[ConstructionScript]タブに処理を書くことができます。
EventGraphはPlayが実行されてから、Eventが発生した時に実行されるタブです。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-construction_script/2022-02-24-06-58-35.png)

ConstructionScriptタブはPlayが実行される前に、配置したActorのComponentの設定を確認しながら変更する処理が書けるタブです。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-construction_script/2022-02-24-06-55-16.png)

Playが実行される前か後かで使用方法を考えます。

### すべて保存する

Blueprint側の説明はここまでになります。
[Content Drawer]から[Save All]ボタンをクリックし、[Save Selected]ボタンをクリックしてプロジェクトの変更のあったアセットをすべて保存します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-construction_script/2022-02-24-06-59-50.png)

## 【参照URL】

https://docs.unrealengine.com/4.27/ja/ProgrammingAndScripting/Blueprints/UserGuide/UserConstructionScript/

