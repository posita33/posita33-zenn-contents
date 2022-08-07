---
title: "【C++ & BP】継承"
free: false
---

## 継承

### 継承について

BlueprintとC++で別々に基底クラスと派生クラスを作成しました。

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

「C++で作成した基底クラスをBPのクラスで継承する方法」や「継承先を変更する方法」について説明します。

```mermaid
classDiagram
    CPPClassBase <|-- CPPClassChild 
    CPPClassBase <|-- BP_ClassChild 
    CPPClassBase <|-- BP_CPPClassChild 
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
	class BP_CPPClassChild {
		# void BeginPlay()
	}
```

### C++の基底クラスからBlueprintの派生クラスを作成する

C++の基底クラスからBlueprintの派生クラスを作成します。

ContentsBrowserの基底クラス「CPPClassBase」を右クリック > [Create Blueprint Class based on CPPClassBase]を選択します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_cpp-bp-inheritance/2022-08-07-11-05-25.png)

Nameにクラス名「BP_ClassChild」を設定します。
作成するフォルダを選択し、[Create Blueprint Class]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_cpp-bp-inheritance/2022-08-07-11-07-48.png)

指定したフォルダに基底クラス「CPPClassBase」を継承したBlueprintが作成されます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_cpp-bp-inheritance/2022-08-07-11-20-44.png)

基底クラスに設定しているクラスはBlueprintEditorの右上に表示されます。
また「Class Settings」のParent Classプロパティで確認できます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_cpp-bp-inheritance/2022-08-07-16-33-10.png)

:::message
Blueprintの作成時に親クラスを選択する際にClass名を検索 > Class名を選択 > Select でもC++で作成したクラスを基底クラスに設定できます。
![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_cpp-bp-inheritance/2022-08-07-16-11-21.png)

:::

### 基底クラスのBeginPlayを呼び出す

BeginPlayノードを右クリック > [Add call to parent function]を選択します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_cpp-bp-inheritance/2022-08-07-16-23-35.png)

[Parent：BeginPlay]ノードが追加されるので、接続します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_cpp-bp-inheritance/2022-08-07-16-24-28.png)

[Compile]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_cpp-bp-inheritance/2022-08-07-16-25-45.png)

「BP_CPPClassChild」をViewportに配置します。
「BP_ClassChild」がある場合は削除します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_cpp-bp-inheritance/2022-08-07-16-28-00.png)

Level Editorの[Play]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_constructor_destructor/2022-07-24-15-50-06.png)

C++の基底クラスのBeginPlayが呼ばれました。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_cpp-bp-inheritance/2022-08-07-16-30-12.png)

呼ばれた処理の順序は以下の図になります。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_cpp-bp-inheritance/2022-08-07-16-40-13.png)

[Parent：BeginPlay]ノードの接続を解除します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_cpp-bp-inheritance/2022-08-07-22-54-25.png)

[Compile]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_cpp-bp-inheritance/2022-08-07-16-25-45.png)

Level Editorの[Play]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_constructor_destructor/2022-07-24-15-50-06.png)

C++の基底クラスのBeginPlayが呼ばれました。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_cpp-bp-inheritance/2022-08-07-22-55-02.png)

C++の基底クラスを継承した際には、[Parent：BeginPlay]ノードを接続しなくても基底クラスのBeginPlayが呼ばれます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_cpp-bp-inheritance/2022-08-07-22-57-55.png)

### 基底クラスのメンバ関数を呼び出す

基底クラスのメンバ関数「CallParentFunc」を呼び出します。

「Call Parent Func」で検索しても検索欄に見つかりません。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_cpp-bp-inheritance/2022-08-07-16-46-48.png)

ヘッダファイルのメンバ関数を宣言している一行上に「UFUNCTION」の設定を追加します。

```cpp:CPPClassBase.h
	// 親クラスのメンバ関数
	UFUNCTION(BlueprintCallable, Category=CPP_And_Blueprint)
	void CallParentFunc();
```

ソースコードを保存して、Compileを実行します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_constructor_destructor/2022-07-24-15-49-43.png)

[CallParentFunc]を検索すると一覧に見つかるようになります。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_cpp-bp-inheritance/2022-08-07-16-56-00.png)

[Parent：BeginPlay]ノードの接続を外し、[CallParentFunc]に接続します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_cpp-bp-inheritance/2022-08-07-16-57-59.png)

[Compile]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_cpp-bp-inheritance/2022-08-07-16-25-45.png)

Level Editorの[Play]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_constructor_destructor/2022-07-24-15-50-06.png)

CallParentFuncが呼ばれました。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_cpp-bp-inheritance/2022-08-07-17-17-52.png)

しかし、実際にはBlueprint側のCallParentFuncが呼ばれておらず、C++の基底クラスのBeginPlayのCallParentFuncが呼ばれています。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_cpp-bp-inheritance/2022-08-07-23-09-52.png)


### 基底クラスのデータメンバを変更する

基底クラスのデータメンバ「VarParentNum」を変更します。

基底クラスのデータメンバ「VarParentNum」を検索しても見つかりません。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_cpp-bp-inheritance/2022-08-07-17-24-40.png)

C++の基底クラス「CPPClassBase」のデータメンバの一行上に「UPROPERTY」の設定を追加します。

```cpp:CPPClassBase.h
	// 親クラスのデータメンバ
	UPROPERTY(EditAnywhere, BlueprintReadWrite, Category=Default)
	int VarParentNum = 10;
```

ここからBeginPlayの処理が影響してきます。
この時のBeginPlayの処理は以下になります。

```cpp:CPPClassBase.cpp
// Called when the game starts or when spawned
void ACPPClassBase::BeginPlay()
{
	// 自分のメンバ関数を呼び出す
	CallParentFunc();
}
```

ソースコードを保存して、Compileを実行します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_constructor_destructor/2022-07-24-15-49-43.png)

基底クラスのデータメンバ[VarParentNum]のDefault値を変更したり、Set関数が呼び出せるようになります。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_cpp-bp-inheritance/2022-08-07-17-55-28.png)

基底クラスのデータメンバ[VarParentNum]値を変更してから「CallParentFunc」を呼び出し、値が変更されたことを確認します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_cpp-bp-inheritance/2022-08-07-17-57-57.png)

[Compile]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_cpp-bp-inheritance/2022-08-07-16-25-45.png)

Level Editorの[Play]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_constructor_destructor/2022-07-24-15-50-06.png)

しかし、Setで設定した値が反映されていません。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_cpp-bp-inheritance/2022-08-07-21-54-11.png)

基底クラスのBeginPlayを「Super::BeginPlay()」だけを呼び出すようにします。

```cpp:CPPClassBase.cpp
void ACPPClassBase::BeginPlay()
{
	Super::BeginPlay();

	// 自分のメンバ関数を呼び出す
	// CallParentFunc();
}
```

ソースコードを保存して、Compileを実行します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_constructor_destructor/2022-07-24-15-49-43.png)

Level Editorの[Play]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_constructor_destructor/2022-07-24-15-50-06.png)

今回はSetで設定した値が反映されました。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_cpp-bp-inheritance/2022-08-07-21-58-33.png)

基底クラスのBeginPlayで[CallParentFunc]を呼び出すようにします。

```cpp:CPPClassBase.cpp
void ACPPClassBase::BeginPlay()
{
	Super::BeginPlay();

	// 自分のメンバ関数を呼び出す
	CallParentFunc();
}
```

ソースコードを保存して、Compileを実行します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_constructor_destructor/2022-07-24-15-49-43.png)

Level Editorの[Play]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_constructor_destructor/2022-07-24-15-50-06.png)

BlueprintとC++の両方で[CallParentFunc]が呼ばれました。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_cpp-bp-inheritance/2022-08-07-22-00-26.png)

呼ばれた順番が分からないので、以下のようにCallParentFuncが呼ばれた後に設定を変更して、間にPrintStringを挟みます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_cpp-bp-inheritance/2022-08-07-22-00-54.png)

結果は、派生クラスのBeginePlayの処理が終わった後に、基底クラスのBeginPlayが呼ばれました。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_cpp-bp-inheritance/2022-08-07-22-02-02.png)

以下の図のような処理順序になります。
C++の基底クラスを継承した際には、派生クラスの処理が終わった後に、基底クラスの処理が呼ばれます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_cpp-bp-inheritance/2022-08-07-22-03-31.png)

:::message
派生クラスの処理が上手く動かない時は、一度、基底クラスのBeginPlayでSuperだけを呼び出す状態でコンパイルをかけると動くようになるかもしれません。

```cpp:CPPClassBase.cpp
void ACPPClassBase::BeginPlay()
{
	Super::BeginPlay();

	// 自分のメンバ関数を呼び出す
	// CallParentFunc();
}
```
:::

### 継承した変数を表示する

Blueprintで継承したクラスの変数は表示されません。
しかし、継承したクラスの変数を表示することができます。
[My Blueprint]パネルの設定ボタンをクリック > [Show Inheited Variables]を選択します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_cpp-bp-inheritance/2022-08-07-22-25-17.png)

継承先の変数がVariablesカテゴリ内に表示されます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_cpp-bp-inheritance/2022-08-07-22-26-11.png)


### 継承先を変更する

Blueprint同士で継承していたClassを

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

継承先をC++の基底クラスに変更します。

```mermaid
classDiagram
    CPPClassBase <|-- CPPClassChild 
    CPPClassBase <|-- BP_ClassChild 
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

「BP_ClassBase」を継承している「BP_ClassChild」の継承先をC++の基底クラス「CPPClassBase」に変更します。
「BP_ClassChild」を開きます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_cpp-bp-inheritance/2022-08-07-22-30-57.png)

[Class Settings]ボタンをクリックし、Parent Classを[CPPClassBase]に変更します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_cpp-bp-inheritance/2022-08-07-23-26-59.png)

[Reparent Blueprint]が表示されるので、[Reparent]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_cpp-bp-inheritance/2022-08-07-22-33-52.png)

BeginPlayの処理を以下のように実装します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_cpp-bp-inheritance/2022-08-07-22-34-51.png)

「BP_CPPClassChild」を削除し、「BP_ClassChild」をViewportにDrag&Dropします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_cpp-bp-inheritance/2022-08-07-22-36-03.png)

基底クラスが変更され、C++の基底クラスの処理が呼ばれるようになりました。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_cpp-bp-inheritance/2022-08-07-22-37-32.png)

Blueprintの基底クラスを継承した時と、C++の基底クラスを継承した時では処理が変わることを把握しておきましょう。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_cpp-bp-inheritance/2022-08-07-22-43-09.png)


### 参照URL

https://docs.unrealengine.com/5.0/ja/cpp-and-blueprints-example/
