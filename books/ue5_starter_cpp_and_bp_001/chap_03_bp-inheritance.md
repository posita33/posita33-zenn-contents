---
title: "【BP】継承"
free: false
---

## 継承

### 継承について

派生クラスは基底クラスのデータメンバーやメンバ関数を含めることができました。
BlueprintでもC++と同様の構成で基底クラスと派生クラスを作成して処理を確認します。

```mermaid
classDiagram
    CPPClassBase <|-- CPPClassChild 
    BP_ClassBase <|-- BP_ClassChild 
	class CPPClassBase {
		# void BeginPlay()
    	+ void CallParentFunc()
		+ int VarParentNum
	}
	class CPPClassChild {
		# void BeginPlay()
		+ void CallChildFunc()
		+ int VarChildNum
	}
	class BP_ClassBase {
		# void BeginPlay()
    	+ void CallParentFunc()
		+ int VarParentNum
	}
	class BP_ClassChild {
		# void BeginPlay()
		+ void CallChildFunc()
		+ int VarChildNum
	}
```

## Blueprintの継承

それではBlueprintで基底クラスと派生クラスを作成してみます。

### 基底クラスの作成

基底クラスのBlueprintを作成します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_bp-inheritance/2022-08-02-06-04-36.png)

親クラスに[Actor]を選択します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_bp-inheritance/2022-08-02-06-06-16.png)

名前を「BP_ClassBase」に設定します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_bp-inheritance/2022-08-02-06-07-36.png)

変数を追加します。

| VariableName | VariableType | DefaultValue |
| ------------ | ------------ | ------------ |
| VarParentNum | Integer      | 20           |

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_bp-inheritance/2022-08-02-06-12-34.png)

関数「CallParentFunc」を追加し、処理を実装します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_bp-inheritance/2022-08-02-06-16-27.png)

「Event Begin Play」で「CallParentFunc」を呼び出します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_bp-inheritance/2022-08-02-06-23-52.png)

「StaticMesh」Componentを追加します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_bp-inheritance/2022-08-02-06-57-10.png)

「StaticMesh」ComponentのStaticMeshに「Cube」を設定します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_bp-inheritance/2022-08-02-07-53-47.png)

Materialには2章で作成したマテリアルを設定します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_bp-inheritance/2022-08-02-07-55-02.png)

[Compile]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_bp-inheritance/2022-08-02-06-34-02.png)

「BP_ClassBase」をViewportに配置します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_bp-inheritance/2022-08-02-08-01-44.png)

Level Editorの[Play]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_constructor_destructor/2022-07-24-15-50-06.png)

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_bp-inheritance/2022-08-02-08-04-21.png)

### 派生クラスの作成

派生クラスを作成します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_bp-inheritance/2022-08-03-06-12-58.png)

親クラスに[BP_ClassBase]を選択します。
継承したいクラスを指定する場合は、[All Classes]からクラス名を検索して選択し、[Select]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_bp-inheritance/2022-08-03-06-15-28.png)

名前を「BP_ClassChild」に設定します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_bp-inheritance/2022-08-03-06-17-52.png)

Blueprintの派生クラスは基底クラスを「右クリック」 > 「Create Child Blueprint Class」 でも作成できます。
同フォルダ内に派生クラスを作るのであれば、コチラの手順の方が早いです。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_bp-inheritance/2022-08-03-06-11-31.png)

変数を追加します。

| VariableName | VariableType | DefaultValue |
| ------------ | ------------ | ------------ |
| VarChildNum  | Integer      | 200          |

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_bp-inheritance/2022-08-03-06-27-49.png)

関数[CallChildFunc]を追加し、処理を実装します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_bp-inheritance/2022-08-03-06-30-41.png)

Begin Playで[CallChildFunc]を呼び出します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_bp-inheritance/2022-08-03-06-32-24.png)

Componentの[StaticMesh]のStaticMeshプロパティに[Sphere]を設定します。
Componentは基底クラスで追加したStaticMeshが派生クラスに継承されているので、派生クラスを作った際に追加されています。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_bp-inheritance/2022-08-03-06-35-10.png)

[Compile]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_bp-inheritance/2022-08-02-06-34-02.png)

「BP_ClassChild」Viewportに配置します。
「BP_ClassBase」を削除します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_bp-inheritance/2022-08-03-07-10-53.png)

Level Editorの[Play]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_constructor_destructor/2022-07-24-15-50-06.png)

基底クラスの関数[CallParentFunc]が呼ばれた後に、関数[CallChildFunc]が呼ばました。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_bp-inheritance/2022-08-03-07-12-07.png)

この時の処理の順序は以下のようになります。
BlueprintもC++の「Super」同様に基底クラスの同じ名前の関数を呼び出すノードが用意されています。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_bp-inheritance/2022-08-05-08-08-09.png)

C++の時と同じ順序で処理をしています。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_bp-inheritance/2022-08-06-17-06-21.png)

### 基底クラスのメンバ関数呼び出し

派生クラスは基底クラスの持つメンバ関数を呼び出すことができます。
Parentノードの接続を外し、基底クラスのメンバ関数「CallParentFunc」を呼び出してから、メンバ関数「CallChildFunc」を呼び出すように修正します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_bp-inheritance/2022-08-06-17-15-23.png)

[Compile]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_bp-inheritance/2022-08-02-06-34-02.png)

Level Editorの[Play]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_constructor_destructor/2022-07-24-15-50-06.png)

基底クラスのメンバ関数「CallParentFunc」を呼びだせることが確認できました。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_bp-inheritance/2022-08-06-17-22-47.png)

### 基底クラスのデータメンバの変更

基底クラスのデータメンバを変更します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_bp-inheritance/2022-08-06-17-52-25.png)

[Compile]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_bp-inheritance/2022-08-02-06-34-02.png)

Level Editorの[Play]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_constructor_destructor/2022-07-24-15-50-06.png)

基底クラスのデータメンバの値を変更できました。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_bp-inheritance/2022-08-06-17-54-49.png)

Blueprintでは基底クラスのデータメンバのDefault値をUIで変更できます。
[ClassDefault]ボタンをクリックすると、[Details]パネルに変数の一覧が表示されます。
基底クラスのデータメンバである[VarParentNum]のDefault値を変更します。
Default値の変更を確認するためにSetノードの接続を外します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_bp-inheritance/2022-08-06-17-57-22.png)

[Compile]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_bp-inheritance/2022-08-02-06-34-02.png)

Level Editorの[Play]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_constructor_destructor/2022-07-24-15-50-06.png)

[Class Default]で変更したDefault値が反映されました。
Blueprintでは基底クラスで宣言したデータメンバの値を派生クラスでUIから変更できるので非常に分かりやすいです。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_bp-inheritance/2022-08-06-18-02-00.png)

### 基底クラスからは派生クラスで定義したデータメンバ、メンバ関数は使用できない

基底クラス「BP_ClassBase」を開きます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_bp-inheritance/2022-08-06-18-10-21.png)

派生クラスのデータメンバ「VarChildNum」を検索しますが、検索欄には見つかりません。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_bp-inheritance/2022-08-06-18-12-40.png)

派生クラスのメンバ関数「CallChildFunc」を検索しますが、検索欄には見つかりません。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_bp-inheritance/2022-08-06-18-09-48.png)

派生クラスでは基底クラスのデータメンバ、メンバ関数を使用できます。
基底クラスでは派生クラスのデータメンバ、メンバ関数を使用できません。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_bp-inheritance/2022-08-06-18-17-59.png)
