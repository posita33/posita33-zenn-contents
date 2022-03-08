---
title: "【BP】Componentを追加する"
free: false
---

## 【Blueprint】Componentを追加する

### 今回できること

BlueprintにComponentを追加し、Viewportタブで追加したComponentを組み立てます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-component/2022-02-11-19-11-21.png)

### 学習用の新規レベル「Chapter_2_Component」を作成する

学習用に新規レベルを作成します。
[File]から[New Level…]を選択します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-02-23-11-21-55.png)

[Basic]を選択し、[Create]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-print_string/2022-03-09-06-14-25.png)

[File]メニューからCurrent Levelを保存します。
ショートカット「Ctrl + S」でも保存できます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-variable/2022-02-23-11-24-39.png)

「Maps」フォルダを選択し、Nameに「Chapter_2_Component」を入力し、[Save]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-component/2022-02-23-16-36-44.png)
*Mapsフォルダを選択 > Name：Chapeter_2_Component > Saveボタンクリック*

### Engine ContentからStaticMeshとMaterialをコピーする

「Engine Content」に入っているStaticMeshをプロジェクトフォルダにコピーして使用します。

[Content Browser]の[Settings]ボタンをクリックし、[Show Engine Content]を有効にします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-component/2022-02-23-16-10-28.png)
*[Content Browser]の[Settings]ボタンをクリック > [Show Engine Content]を有効*

[Show Engine Content]を有効にすると[Content Browser]が表示されます。
「Engine Content」から「StaticMesh」と「Material」をコピーするので、「CPP_BP」に「Materials」「Meshes」フォルダを作成します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-component/2022-02-23-16-12-14.png)

「Engine Content」の「BasicShaps」フォルダに移動します。
「BasicShaps」フォルダには、PlaceActorからDrag&DropでViewportに追加できるプリミティブのメッシュが格納されています。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-component/2022-02-23-16-15-18.png)

[Engine Content]を直接変更してしまうと、他のプロジェクトでEngine Contentを使用している箇所にも影響してしまいます。
[Engine Content]のStaticMesh「Cube」を先ほど作成した「Meshes」フォルダにコピーします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-component/2022-02-23-16-16-41.png)

CubeをMeshewフォルダにDrag&Drop > [Copy Here]を選択
「Meshes」フォルダに「Cube」がコピーされました。
名前を「SM_SampleCube」に変更します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-component/2022-02-23-16-18-17.png)

「SM_SampleCube」の質感を設定するためのMaterial「BasicShapeMaterial」を「Materials」フォルダにコピーします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-component/2022-02-23-16-19-46.png)
*「BasicShapesフォルダ」の「BasicShapeMaterial」を「Materials」フォルダにDrag&Drop > [Copy Here]を選択*

「Materials」フォルダに「BasicShapeMaterial」がコピーされます。
名前を「M_SampleMaterial」に変更します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-component/2022-02-23-16-21-33.png)

「Meshes」フォルダの「SM_SampleCube」をダブルクリックしてStaticMesh Editorを開きます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-component/2022-02-23-16-22-20.png)

StaticMesh Editorの[Detil]パネルでMaterialを「M_SampleMaterial」に設定します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-component/2022-02-23-16-24-29.png)

Cubeの質感が、「M_SampleMaterial」で設定している白い色に変わります。[Compile]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-component/2022-02-23-16-25-40.png)

Content Browserの「SM_SampleCube」のサムネイルも「M_SampleCube」の質感が反映されました。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-component/2022-02-23-16-26-52.png)

### Blueprintを複製する

「BP_Variable」を複製（Ctrl + D）して、「BP_Component」を作成します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-component/2022-03-02-06-03-35.png)

### StaticMeshComponentを追加する

「Component（コンポーネント）」を追加します。
UnrealEngineのComponentは「Actor（俳優）」の「Component（部品、構成要素）」といった意味です。レベルに配置できるBlueprintの構成要素を組み込みます。

「BP_Component」をダブルクリックしてBlueprint Editorを開きます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-component/2022-02-23-16-30-50.png)

「Component」は「Viewport」タブで確認しながら、「Component」パネルからコンポーネント追加・設定します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-component/2022-02-23-16-32-39.png)

[Static Mesh Component]を追加します。
[Component]パネルの[Add]ボタンから[Static Mesh]を選択します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-component/2022-02-23-16-33-58.png)

[Component]パネルに[StaticMesh]が追加されます。
[StaticMesh]Componentの[Detail]パネルから先ほど準備した「SM_SampleCube」を設定します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-component/2022-02-11-18-28-18.png)

[Detail]パネルの[StaticMesh]のリストをクリックし、「SM_SampleCube」を検索して選択します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-component/2022-02-11-18-30-29.png)

Viewportタブに「SM_SampleCube」が表示されます。
[Compile]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-component/2022-02-11-18-32-22.png)

Level Editorに戻り、「BP_Component」をDrag＆Dropします。
Viewportで確認したStaticMeshComponentが表示されます。
コントローラーのアイコンが表示されているActorの水色の矢印の先に移動させます。
コントローラーのアイコンはPlayerStartというPlayした時にプレイヤーの開始位置になります。水色の矢印はPlay開始時にプレイヤーの向いている方向です。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-component/2022-02-23-16-38-42.png)

[Play]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-print_string/2022-02-23-09-19-08.png)

StaticMeshComponentに設定したSM_SampleCubeが表示されます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-component/2022-02-23-16-40-05.png)

### ArrowComponentを追加する

「Cube」は前後左右が分からないので、方向を表示する「ArrowComponent」を追加します。

「BP_Component」をダブルクリックしてBlueprint Editorを開きます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-component/2022-02-23-16-40-46.png)

[Component]パネルの[Add]ボタンをクリックし、[Arrow]で検索し、[Arrow]を選択します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-component/2022-02-11-18-41-50.png)

Viewportタブを確認すると、赤い矢印が表示されます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-component/2022-02-11-18-43-54.png)

Cube内に埋もれているので、矢印が確認しやすいように移動します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-component/2022-02-11-18-45-14.png)

### ArrowComponentをStaticMeshComponentにアタッチする

StaticMeshComponentを移動させた時に、ArrowComponentを一緒に移動できるように設定します。
図のようなStaticMeshComponentとArrowComponentが同じ階層にある場合、StaticMeshComponentを移動させるとStaticMeshComponentのみが移動します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-component/2022-02-11-18-46-53.png)

[ArrowComponent]を[StaticMeshComponent]にDrag&Dropします。
「[ArrowComponent]を[StaticMeshComponent]にAttach（取り付ける）する」と言います。
（他には、ArrowComponentをStaticMeshComponentの子にする）

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-component/2022-02-11-18-48-33.png)

ComponentをAttachすると親子関係ができます。
親である[StaticMeshComponent]を移動すると、子である[ArrowComponent]が一緒に移動します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-component/2022-02-11-18-50-34.png)

子である[ArrowComponent]を移動しても、親である[StaticMeshComponent]は移動しません。
親は子に影響を及ぼしますが、子は親に影響しません。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-component/2022-02-11-18-51-59.png)

ComponentのAttach（親子関係）が把握できたので、[ArrowComponent]と[StaticMeshComponent]の位置を元に戻します。
[Compile]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-component/2022-02-11-18-53-22.png)

LevelEditorのViewportに配置した「BP_Component」を確認します。
[ArrowComponent]が表示されているので、[Cube]の向きが確認できます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-component/2022-01-27-10-59-14.png)

[Play]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-print_string/2022-02-23-09-19-08.png)

[ArrowComponent]はPlayすると表示されません。
[ArrowComponent]は配置した時に方向を確認するために使用するComponentです。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-component/2022-02-23-16-43-22.png)

### PointLightComponentを追加する

Cubeの前方にLight追加することで、[Play]ボタンを押した後にもCubeの前方がわかるようにします。

「BP_Component」をダブルクリックしてBlueprint Editorを開きます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-component/2022-02-23-16-40-46.png)

[StaticMesh]を選択し、[Add]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-component/2022-02-11-19-00-28.png)

[Component]パネルの[Add]ボタンをクリックし、[Point]で検索し、[Point Light]を選択します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-component/2022-02-11-19-03-28.png)

[StaticMesh]を選択した状態で、Componentを追加すると、子としてComponentを追加できます。最初から構成が決まっているのであれば、選択してからComponentを追加するとAttachする手間が省けます。
[PointLight]を[Arrow]の前方に移動します。
[Compile]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-component/2022-02-11-19-05-39.png)

LevelEditorのViewportで[Arrow]の前方が明るくなりました。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-component/2022-01-27-11-01-24.png)

[Play]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-print_string/2022-02-23-09-19-08.png)

[Play]してからでもArrowの矢印が向いている方が明るいので、前方がどちらかが分かります。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-component/2022-02-23-16-45-33.png)

### すべて保存する

Blueprint側の説明はここまでになります。
[Content Browser]から[Save All]ボタンをクリックし、[Save Selected]ボタンをクリックしてプロジェクトの変更のあったアセットをすべて保存します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-component/2022-02-23-16-46-33.png)
