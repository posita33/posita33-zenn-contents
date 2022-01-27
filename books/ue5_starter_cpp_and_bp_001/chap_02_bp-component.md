---
title: "【BP】Componentを追加する"
emoji: "🦁"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["unrealengine", "ue5", "ue4", "blueprint"]
published: false
---


## 【Blueprint】Componentを追加する

### 今回できること
【要執筆】。

### 学習用の新規レベル「Chapter_2_Component」を作成する
学習用の新規レベルを作成します。
[File]から[New Level…]を選択します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-component/2022-01-27-09-46-22.png)
*File > New Level…*

[Default]を選択します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-component/2022-01-27-09-46-34.png)

[Default]を選択
「Maps」フォルダに「Chapter_2_5_Component」を入力し、[Save]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-component/2022-01-27-09-46-51.png)
*Mapsフォルダを選択 > Name：Chapeter_2_5_Component > Saveボタンクリック*

### Engine ContentからStaticMeshとMaterialをコピーする
「Engine Content」に入っているStaticMeshをプロジェクトフォルダにコピーして使用します。

[Content Browser]の[Settings]ボタンをクリックし、[Show Engine Content]を有効にします。
![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-component/2022-01-27-09-47-58.png)
*[Content Browser]の[Settings]ボタンをクリック > [Show Engine Content]を有効*

[Show Engine Content]を有効にすると[Content Browser]が表示されます。
「Engine Content」から「StaticMesh」と「Material」をコピーするので、「CPP_BP」に「Materials」「Meshes」フォルダを作成します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-component/2022-01-27-09-48-38.png)

「Engine Content」の「BasicShaps」フォルダに移動します。
「BasicShaps」フォルダには、PlaceActorからDrag&DropでViewportに追加できるプリミティブのメッシュが格納されています。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-component/2022-01-27-09-48-53.png)

[Engine Content]を直接変更してしまうと、他のプロジェクトでEngine Contentを使用している箇所にも影響してしまいます。
[Engine Content]のStaticMesh「Cube」を先ほど作成した「Meshes」フォルダにコピーします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-component/2022-01-27-09-49-11.png)

CubeをMeshewフォルダにDrag&Drop > [Copy Here]を選択
「Meshes」フォルダに「Cube」がコピーされました。
名前を「SM_SampleCube」に変更します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-component/2022-01-27-09-49-21.png)

「SM_SampleCube」の質感を設定するためのMaterial「BasicShapeMaterial」を「Materials」フォルダにコピーします。
![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-component/2022-01-27-09-49-39.png)
*「BasicShapesフォルダ」の「BasicShapeMaterial」を「Materials」フォルダにDrag&Drop > [Copy Here]を選択*


「Materials」フォルダに「BasicShapeMaterial」がコピーされます。
名前を「M_SampleMaterial」に変更します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-component/2022-01-27-10-49-25.png)

「Meshes」フォルダの「SM_SampleCube」をダブルクリックしてStaticMesh Editorを開きます。
![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-component/2022-01-27-10-49-57.png)

StaticMesh Editorの[Detil]パネルでMaterialを「M_SampleMaterial」に設定します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-component/2022-01-27-10-50-12.png)

Cubeの質感が、「M_SampleMaterial」で設定している白い色に変わります。[Compile]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-component/2022-01-27-10-51-29.png)

Content Browserの「SM_SampleCube」のサムネイルも「M_SampleCube」の質感が反映されました。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-component/2022-01-27-10-51-43.png)

### StaticMeshComponentを追加する

「Component（コンポーネント）」を追加します。
UnrealEngineのComponentは「Actor（俳優）」の「Component（部品、構成要素）」といった意味です。レベルに配置できるBlueprintの構成要素を組み込みます。

「BP_SampleActor」をダブルクリックしてBlueprint Editorを開きます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-component/2022-01-27-10-52-40.png)

「Component」は「Viewport」タブで確認しながら、「Component」パネルからコンポーネント追加・設定します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-component/2022-01-27-10-52-57.png)

[Static Mesh Component]を追加します。
[Component]パネルの[Add]ボタンから[Static Mesh]を選択します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-component/2022-01-27-10-53-12.png)

[Component]パネルに[StaticMesh]が追加されます。
[StaticMesh]Componentの[Detail]パネルから先ほど準備した「SM_SampleCube」を設定します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-component/2022-01-27-10-53-24.png)

[Detail]パネルの[StaticMesh]のリストをクリックし、「SM_SampleCube」を検索して選択します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-component/2022-01-27-10-53-46.png)

Viewportタブに「SM_SampleCube」が表示されます。
[Compile]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-component/2022-01-27-10-54-00.png)

Level Editorに戻り、「BP_SampleActor」をDrag＆Dropします。
Viewportで確認したStaticMeshComponentが表示されます。
コントローラーのアイコンが表示されているActorの水色の矢印の先に移動させます。
コントローラーのアイコンはPlayerStartというPlayした時にプレイヤーの開始位置になります。水色の矢印はPlay開始時にプレイヤーの向いている方向です。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-component/2022-01-27-10-54-13.png)

[Play]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-component/2022-01-27-10-54-27.png)

SM_SampleMeshが表示されます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-component/2022-01-27-10-55-04.png)

### ArrowComponentを追加する
「Cube」は前後左右が分からないので、方向を表示する「ArrowComponent」を追加します。

「BP_SampleActor」をダブルクリックしてBlueprint Editorを開きます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-component/2022-01-27-10-55-26.png)

[Component]パネルの[Add]ボタンをクリックし、[Arrow]で検索し、[Arrow]を選択します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-component/2022-01-27-10-56-43.png)

Viewportタブを確認すると、赤い矢印が表示されます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-component/2022-01-27-10-56-56.png)

Cube内に埋もれているので、矢印が確認しやすいように移動します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-component/2022-01-27-10-57-09.png)

### ArrowComponentをStaticMeshComponentにアタッチする
StaticMeshComponentを移動させた時に、ArrowComponentを一緒に移動できるように設定します。
図のようなStaticMeshComponentとArrowComponentが同じ階層にある場合、StaticMeshComponentを移動させるとStaticMeshComponentのみが移動します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-component/2022-01-27-10-57-30.png)

[ArrowComponent]を[StaticMeshComponent]にDrag&Dropします。
「[ArrowComponent]を[StaticMeshComponent]にAttach（取り付ける）する」と言います。
（他には、ArrowComponentをStaticMeshComponentの子にする）

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-component/2022-01-27-10-57-48.png)

ComponentをAttachすると親子関係ができます。
親である[StaticMeshComponent]を移動すると、子である[ArrowComponent]が一緒に移動します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-component/2022-01-27-10-58-09.png)

子である[ArrowComponent]を移動しても、親である[StaticMeshComponent]は移動しません。
親は子に影響を及ぼしますが、子は親に影響しません。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-component/2022-01-27-10-58-35.png)

ComponentのAttach（親子関係）が把握できたので、[ArrowComponent]と[StaticMeshComponent]の位置を元に戻します。
[Compile]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-component/2022-01-27-10-58-54.png)

LevelEditorのViewportに配置した「BP_SampleActor」を確認します。
[ArrowComponent]が表示されているので、[Cube]の向きが確認できます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-component/2022-01-27-10-59-14.png)

[Play]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-component/2022-01-27-10-59-29.png)

[ArrowComponent]はPlayすると表示されません。
[ArrowComponent]は配置した時に方向を確認するために使用するComponentです。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-component/2022-01-27-10-59-51.png)

### PointLightComponentを追加する

Cubeの前方にLight追加することで、[Play]ボタンを押した後にもCubeの前方がわかるようにします。

「BP_SampleActor」をダブルクリックしてBlueprint Editorを開きます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-component/2022-01-27-11-00-19.png)

[StaticMesh]を選択し、[Add]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-component/2022-01-27-11-00-37.png)


[Component]パネルの[Add]ボタンをクリックし、[Point]で検索し、[Point Light]を選択します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-component/2022-01-27-11-00-58.png)

[StaticMesh]を選択した状態で、Componentを追加すると、子としてComponentを追加できます。最初から構成が決まっているのであれば、選択してからComponentを追加するとAttachする手間が省けます。
[PointLight]を[Arrow]の前方に移動します。
[Compile]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-component/2022-01-27-11-01-09.png)

LevelEditorのViewportで[Arrow]の前方が明るくなりました。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-component/2022-01-27-11-01-24.png)

[Play]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-component/2022-01-27-11-01-38.png)

[Play]してからでもArrowの矢印が向いている方が明るいので、前方がどちらかが分かります。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-component/2022-01-27-11-01-56.png)

### すべて保存する

Blueprint側の説明はここまでになります。
[Content Browser]から[Save All]ボタンをクリックし、[Save Selected]ボタンをクリックしてプロジェクトの変更のあったアセットをすべて保存します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-component/2022-01-27-11-02-08.png)

