---
title: "【CPP】 Variable(変数)"
emoji: "🐷"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["unrealengine", "ue5", "ue4", "blueprint"]
published: false
---

## 【C++】変数を作成して取得・設定する

### C++でBlueprintを再現すること
【要執筆】。

### Visual Studioを開いて、CPPSampleActor.cppを表示する
プロジェクトを閉じていたら、プロジェクトを開き、「Chapter_2_4_Variable」を開きます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-variable/2022-01-27-08-32-57.png)

[Tools]メニューからVisual Studioを開きます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-variable/2022-01-27-08-33-18.png)

Solution Explorerから「CPPSampleActor.cpp」をダブルクリックして開きます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-variable/2022-01-27-08-33-33.png)

前回書いたPrintString関数の引数をBlueprintと同じように変数化します。
C++では関数の引数がBlueprintのInputピンになります。
関数の引数については、関数の項目で詳しく説明します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-variable/2022-01-27-08-33-47.png)

### PrintString関数で文字列を出力するための変数を作成する

変数「Message」を作成して、Print StringのIn Stringに接続する内容をC++で実装します。
Event BeginePlayノードに該当するBeginPlay関数を編集します。

```cpp:CPPSampleActor.cpp
void ACPPSampleActor::BeginPlay()
{
	Super::BeginPlay();

	FString Message= "C++ Hello World!";

	// PrintStringノードと同じ処理
	// UKismetSystemLibraryクラスのPrintString関数を呼び出す
	UKismetSystemLibrary::PrintString(this, Message, true, true, FColor::Cyan, 2.f);
}
```

C++の変数の作成は図のようになります。
プログラミング言語では「変数を作成する」ではなく、「変数を宣言する」と言い方が適切です。

**変数の宣言**
https://wa3.i-3-i.info/word18069.html

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-variable/2022-01-27-08-36-09.png)

Blueprintプリントでは変数の設定をDetailパネルで編集できます。
Variable Name、Variable Type、Default Valueというラベルが書かれているので親切です。
C++は**「文法を理解している」という暗黙の了解**で記述することになります。**文法を理解すれば大丈夫です**。一緒に頑張りましょう。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-variable/2022-01-27-08-36-56.png)

作成した変数名[Message]をPrint String関数のIn Stringにあたる、左から2番目の引数に変数名[Message]を記入します。
引数は","（カンマ）区切りです。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-variable/2022-01-27-08-37-19.png)

Blueprintは変数[Message]のGetノードからPrintStringノードの[In String]ピンに接続しました。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-variable/2022-01-27-08-37-32.png)

ソースコードを編集したので、Compileを行います。
編集したファイルを保存します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-variable/2022-01-27-08-37-56.png)
*File > Save (編集したファイル)*

Build > Build Solutionか、Level Editorの右下のアイコンでComileを行います。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-variable/2022-01-27-08-38-30.png)

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-variable/2022-01-27-08-38-43.png)

BlueprintではCompile > 保存でした。
C++は保存されたファイルに対してCompileを行います。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-variable/2022-01-27-08-39-06.png)

編集したC++のActorクラスをLevelEditorのViewportにDrag&Dropします。
World Outlinerに追加したActorクラス名が表示されることを確認します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-variable/2022-01-27-08-40-47.png)

Level Editorの[Play]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-variable/2022-01-27-08-39-22.png)



変数「Message」に設定した文字列が表示されました。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-variable/2022-01-27-08-39-34.png)


**【Column】 String型ではなくUnrealEngine独自のFStringクラス**

int（整数）型やfloat（浮動小数点）型のVariable TypeにはFが付かないのに、String型にはVariable Typeを**FString**とFを最初に付けて宣言します。

int,floatはPrimitive（プリミティブ）型といってUnrealEngine以外のC++でも共通の変数の型です。

https://wa3.i-3-i.info/word15876.html

UnrealEngineのString型は
Engine\Source\Runtime\Core\Public\Misc\CString.hで定義されている「FString」クラスを使用します。

F（型名）のVariable TypeはUnrealEngine独自の変数の型です。
UnrealEngine以外でC++を書く際には、FStringが存在しないので気を付けてください。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-variable/2022-01-27-08-41-24.png)

FStringクラスでは文字列を操作するための便利な関数が用意されています。

https://docs.unrealengine.com/4.27/en-US/ProgrammingAndScripting/ProgrammingWithCPP/UnrealArchitecture/StringHandling/FString/

### 変数Durationをヘッダファイルに定義してSetter/Getterを作成してPrintString関数で使用する

次のBlueprintを再現します。
- PrintString関数のDurationピンに変数[Duration]のGetノードを設定します。
- PrintString関数の実行前にSetノードで変数の値を変更します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-variable/2022-01-27-08-42-21.png)

ヘッダファイルに変数を宣言する。
変数[Message]はBeginPlay関数内に変数を宣言しました。
今回の変数[Duration]はヘッダファイル[CPPSampleActor.h]に変数を宣言します。
SolutionExplorerの「CPPSampleActor.h」を開きます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-variable/2022-01-27-08-42-34.png)

CPPSampleActor.h

```cpp:CPPSampleActor.h
// Fill out your copyright notice in the Description page of Project Settings.

#pragma once

#include "CoreMinimal.h"
#include "GameFramework/Actor.h"
#include "CPPSampleActor.generated.h"

UCLASS()
class CPP_BP_API ACPPSampleActor : public AActor
{
	GENERATED_BODY()
	
public:	
	// Sets default values for this actor's properties
	ACPPSampleActor();

	// PrintString関数のDurationに設定する変数
	float Duration = 10.0f;

protected:
	// Called when the game starts or when spawned
	virtual void BeginPlay() override;

public:	
	// Called every frame
	virtual void Tick(float DeltaTime) override;

};
```

変数[Duration]を宣言した箇所だけ抽出しました。

Variable Name：Durationa
Variable Type：float
Default Value：10.0f

```cpp
	// PrintString関数のDurationに設定する変数
	float Duration = 10.0f;
```

**【Column】数値の最後に文字は接尾語**
10.0fの”f”はfloatの接尾語です。[10.0]と書いてもCompileは成功します。

> 値の終わりに接尾語を付けることで、その値の型を指定できます。
> 浮動小数点用の接尾語としてFとLがあります。Fはfloat、Lはlong double、省略した場合はdoubleと解釈されます

https://atmarkit.itmedia.co.jp/ait/articles/1002/10/news122_3.html


次は処理を書きます。
処理を書く前にBlueprintの処理を確認します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-variable/2022-01-27-08-45-01.png)

Solution Explorerから「CPPSampleActor.cpp」をダブルクリックして開き、BeginPlay関数に処理を実装します。

```cpp:CPPSampleActor.cpp BeginPlay()
void ACPPSampleActor::BeginPlay()
{
	Super::BeginPlay();

	FString Message = "C++ Hello World!";

	Duration = 3.0f;

	// PrintStringノードと同じ処理
	// UKismetSystemLibraryクラスのPrintString関数を呼び出す
	UKismetSystemLibrary::PrintString(this, Message, true, true, FColor::Cyan, Duration);
}
```
C++とBlueprintの処理を対応させた図です。

**Setノード**
Duration = 3.0f;
**Getノード**
DurationをPrintString関数の引数に記述する。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-variable/2022-01-27-08-46-10.png)

Ctrl + Sでファイルを保存し、Compileを行います。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-variable/2022-01-27-08-46-26.png)

Level Editorの[Play]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-variable/2022-01-27-08-46-39.png)

文字が変数[Duration]に設定した[3.0f](3秒間)表示されます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-variable/2022-01-27-08-46-49.png)

### 変数を定数化（const）して値を変更できなくする（ReadOnly：読み取り専用を再現）

Blueprintで変数の[Blueprint Read Only]を有効にして、読み取り専用にしたのでCompileでSetノードがErrorになりました。
C++で読み取り専用の変数を再現します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-variable/2022-01-27-08-47-20.png)

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-variable/2022-01-27-08-47-27.png)


「CPPSampleActor.h」に宣言したDurationの先頭に「const」を追加します。

```cpp:CPPSampleActor.h
private:
	// PrintString関数のDurationに設定する変数
	const float Duration = 10.0f;
```
const修飾子は変数の型の前に宣言します。

```cpp
const VariableType VariableName = DefaultValue; 
```


const 修飾子を変数に設定すると、一度設定したDefault Valueから変更することが出来なくなります。

> C++ 言語には、定数を表現するための const 修飾子が用意されています。ここでは const 修飾子のさまざまな使い方について説明します。
const 修飾子を使う目的は、コンパイラによる最適化を促進するためと、プログラムの意味をより明確にすることです。
変数の宣言に const をつけることで、その変数の値が書き換えられないようにできます。

[引用元：C++の基礎 : const 修飾子](http://www.s-cradle.com/developer/sophiaframework/tutorial/Cpp/const.html)

Ctrl＋Sでファイルを保存し、[Build]メニューから[Build Solution]を選択してCompileします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-variable/2022-01-27-09-23-16.png)

Blueprintの時と同じようにCompileがエラーになります。
[Output]ウィンドウのErrorメッセージをダブルクリックします。
エラー箇所に移動すると、変数[Duration]の値を変更している箇所がエラーと判定されています。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-variable/2022-01-27-09-23-34.png)

変数[Duration]に値を設定している行を削除します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-variable/2022-01-27-09-24-34.png)

Ctrl＋Sでファイルを保存し、[Build]メニューから[Build Solution]を選択してCompileします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-variable/2022-01-27-09-24-45.png)

今度はCompileが成功しました。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-variable/2022-01-27-09-25-30.png)

Level Editorの[Play]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-variable/2022-01-27-09-24-57.png)

const修飾子を一緒に宣言したことで、変数に設定したDefault Valueが約束されます。値を変更したくない変数にはconst修飾子を宣言することで、読み取り専用の変数として使用できます。
const修飾子は関数で大活躍します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-variable/2022-01-27-09-25-44.png)

https://zenn.dev/posita33/articles/a0ee3a45e5cdb2


### VariableTypeを別の型（floatからFString）に変換する

Blueprintで**Variable TypeをFloatからStringに変換するノード**を使いました。
C++で**Variable TypeをFloatからStringに変換するノード**を再現します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-variable/2022-01-27-09-27-31.png)

Solution Explorerから「CPPSampleActor.cpp」をダブルクリックして開き、BeginPlay関数に処理を実装します。
確認しやすいようにPrintString関数を複数行にしました。

```cpp:CPPSampleActor.cpp
#include "CPPSampleActor.h"
#include "Kismet/KismetSystemLibrary.h"
#include "Kismet/KismetStringLibrary.h" // 追加
```

```cpp:CPPSampleActor.cpp
void ACPPSampleActor::BeginPlay()
{
	Super::BeginPlay();

	FString Message = "C++ Hello World!";

	// PrintStringノードと同じ処理
	// UKismetSystemLibraryクラスのPrintString関数を呼び出す
	UKismetSystemLibrary::PrintString(
		this
		, UKismetStringLibrary::Conv_FloatToString(Duration) // DurationをfloatからFStringに変換する
		, true
		, true
		, FColor::Cyan
		, Duration);
}
```

Variable TypeをFloatからStringに変換するノードは、UKismetStringLibraryクラスのConv_FloatToString関数を使用します。

```cpp
UKismetStringLibrary::Conv_FloatToString(Duration) // DurationをfloatからFStringに変換する
```

UKismetStringLibraryクラスのConv_FloatToString関数はKismetStringLibrary.hで宣言されているので、KismetStringLibrary.hを使用するために#include文を追加します。

```cpp
#include "Kismet/KismetStringLibrary.h" // 追加
```

Ctrl + Sでファイルを保存し、Compileを行います。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-variable/2022-01-27-09-29-46.png)

Level Editorの[Play]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-variable/2022-01-27-09-30-36.png)

変数[Duration]の値が文字列として画面に表示されます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-variable/2022-01-27-09-30-00.png)

https://zenn.dev/posita33/articles/8dd51074f1915a

### PrintStringのTextColorを変数化

最後にPrint StringのTextColorを変数化して、PrintString関数のTextColorにGetノードを接続処理をC++で再現します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-variable/2022-01-27-09-31-06.png)

PrintStringのTextColorに使用されるVariable TypeはLinearColorです。
C++でVariable Typeを宣言する時は[**FLinearColor**]になります。
「**CPPSampleActor.h**」に変数[**TextColor**]を宣言します。

```cpp:CPPSampleActor.h
	// PrintString関数のDurationに設定する変数
	const float Duration = 10.0f;

	// PrintString関数のTextColorに設定する変数
	const FLinearColor TextColor = FLinearColor(0.0, 0.66, 1.0);
```

「CPPSampleActor.cpp」のPrintString関数に変数[TextColor]を使用するように記入します。
In Stringには変数[Message]を使用するように戻します。

```cpp:CPPSampleActor.cpp
// Called when the game starts or when spawned
void ACPPSampleActor::BeginPlay()
{
	Super::BeginPlay();

	FString Message = "C++ Hello World!";

	// PrintStringノードと同じ処理
	// UKismetSystemLibraryクラスのPrintString関数を呼び出す
	UKismetSystemLibrary::PrintString(
		this
		, Message // Messageに戻す
		, true
		, true
		, TextColor// Textのカラー情報に変数TextColorを設定
		, Duration);
}
```

Ctrl + Sでファイルを保存し、Compileを行います。
![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-variable/2022-01-27-09-33-44.png)

Level Editorの[Play]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-variable/2022-01-27-09-33-57.png)

TextColorが変更されました。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-variable/2022-01-27-09-34-09.png)

https://zenn.dev/posita33/articles/41737b3be89aa4

### C++とBlueprintの比較画像

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-variable/2022-01-27-09-35-00.png)


## 最終的なソースコード

```cpp:CPPSampleActor.h
#include "CoreMinimal.h"
#include "GameFramework/Actor.h"
#include "CPPSampleActor.generated.h"

UCLASS()
class CPP_BP_API ACPPSampleActor : public AActor
{
	GENERATED_BODY()
	
public:	
	// Sets default values for this actor's properties
	ACPPSampleActor();

	// PrintString関数のDurationに設定する変数
	const float Duration = 10.0f;

	// PrintString関数のTextColorに設定する変数
	const FLinearColor TextColor = FColor(255, 255, 255);

protected:
	// Called when the game starts or when spawned
	virtual void BeginPlay() override;

public:	
	// Called every frame
	virtual void Tick(float DeltaTime) override;
};
```

```cpp:CPPSampleActor.h
// Fill out your copyright notice in the Description page of Project Settings.


#include "CPPSampleActor.h"
#include "Kismet/KismetSystemLibrary.h"
#include "Kismet/KismetStringLibrary.h" // 追加

// Sets default values
ACPPSampleActor::ACPPSampleActor()
{
 	// Set this actor to call Tick() every frame.  You can turn this off to improve performance if you don't need it.
	PrimaryActorTick.bCanEverTick = true;
}

// Called when the game starts or when spawned
void ACPPSampleActor::BeginPlay()
{
	Super::BeginPlay();

	FString Message = "C++ Hello World!";

	// PrintStringノードと同じ処理
	// UKismetSystemLibraryクラスのPrintString関数を呼び出す
	UKismetSystemLibrary::PrintString(
		this
		, Message // Messageに戻す
		, true
		, true
		, TextColor  // Textのカラー情報に変数TextColorを設定
		, Duration);
}

// Called every frame
void ACPPSampleActor::Tick(float DeltaTime)
{
	Super::Tick(DeltaTime);

}
```

