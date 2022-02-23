---
title: "【C++】Componentを追加する"
free: false
---

## 【C++】Componentを追加する

### C++でBlueprintを再現すること

Blueprintで追加したComponentとComponentの親子構成をC++で再現します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-component/2022-01-27-11-15-45.png)

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-component/2022-02-11-22-14-42.png)

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-component/2022-01-27-11-11-38.png)

### 編集するActorクラスを作成する

プロジェクトを閉じていたら、プロジェクトを開き、「Chapter_2_Component」を開きます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-component/2022-02-23-16-49-48.png)

[Tools]メニューから[New C++ Class]を開きます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-component/2022-02-11-20-57-12.png)

親クラスに[Actor]を選択します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-component/2022-02-23-08-42-50.png)

ClassTypeとClass名を設定します。

| Property   | Value        |
| ---------- | ------------ |
| Class Type | Public       |
| Name       | CPPComponent |

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-component/2022-02-23-16-51-33.png)

Solution Explorerから今回編集する2つのファイルを開きます。

- CPPComponent.cpp
- CPPComponent.h

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-component/2022-02-11-21-01-56.png)

開いたファイルを学習する初期状態に修正します。

```cpp:CPPComponent.h
// Fill out your copyright notice in the Description page of Project Settings.

#pragma once

#include "CoreMinimal.h"
#include "GameFramework/Actor.h"
#include "CPPComponent.generated.h"

UCLASS()
class CPP_BP_API ACPPComponent : public AActor
{
	GENERATED_BODY()

protected:
	// Called when the game starts or when spawned
	virtual void BeginPlay() override;

private:
	// PrintString関数のDurationに設定する変数
	const float Duration = 10.0f;

	// PrintString関数のTextColorに設定する変数
	const FLinearColor TextColor = FLinearColor(0.0, 0.66, 1.0);

};
```

```cpp:CPPComponent.cpp
// Fill out your copyright notice in the Description page of Project Settings.


#include "CPPComponent.h"
#include "Kismet/KismetSystemLibrary.h"

// Called when the game starts or when spawned
void ACPPComponent::BeginPlay()
{
	FString Message = "C++ Hello World!";

	// PrintStringノードと同じ処理
	// UKismetSystemLibraryクラスのPrintString関数を呼び出す
	UKismetSystemLibrary::PrintString(this, Message, true, true, TextColor, Duration);
}
```

### SceneComponentをRootComponentに設定する

Componentの一番上の階層のことをSceneRootと呼びます。
Actorを親クラスにしたBlueprintには最初RootComponentにSceneComponentが設定されています。
SceneComponentは階層のグループを作成したりする、Transform情報だけ持つコンポーネントです。
C++でRootComponentにSceneComponentを設定する処理を実装します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-component/2022-02-11-21-12-12.png)

「CPPComponent.hのpublic」に変数を追加します。

- VariableType：USceneComponent*
- VariableName：DefaultSceneRoot

USceneComponent*の「`*`」はポインタです。
「USceneComponentのポインタ型」というのが正式な名称です。
ポインタについては別の機会で説明します。

```cpp:CPPComponent.h
public:
	// Scene Component
	UPROPERTY(EditAnywhere)
	USceneComponent* DefaultSceneRoot;
```

```cpp
UPROPERTY(EditAnywhere)
```

UPROPERTYはプロパティ指定子というUnreal独自のプロパティです。
変数をどのように使用するか、設定するかを宣言します。

> プロパティを宣言する時、Property Specifiers を宣言に追加して、Unreal Engine および Unreal Editor の各部で、プロパティがどのように動作するのかを制御できます。

[引用元：プロパティ指定子](https://docs.unrealengine.com/4.27/ja/ProgrammingAndScripting/GameplayArchitecture/Properties/Specifiers/)

[EditAnyWhere]はDetailパネルで値を編集できるようにする設定です。

**「CPPComponent.cpp」ACPPComponent関数 （Constractor）**
[SceneComponent：DefaultSceneRoot]を[RootComponent]に設定する処理を実装します。
クラス名::クラス名()はConstructorです。Constructorはクラスを作成する時に呼ばれる関数です。BeginePlay関数より先に呼ばれます。

**Componentの追加や設定はConstructorで行います。**

```cpp:CPPComponent.h
public:
	// Sets default values for this actor's properties
	ACPPComponent();
```

```cpp:CPPComponent.cpp
ACPPComponent::ACPPComponent()
{
	// SceneComponentを作成する
	DefaultSceneRoot = CreateDefaultSubobject<USceneComponent>(TEXT("SceneComponent"));

	// SceneComponentをRootComponentに設定する
	RootComponent = DefaultSceneRoot;
}
```

ソースコードを保存して、Compileを実行します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-print_string/2022-02-23-10-58-50.png)

「CPPComponent」を「BP_Component」の隣に配置します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-component/2022-02-23-16-57-37.png)

C++ではBlueprintのようにEditorで確認することが出来ないので、レベルに配置した「CPPComponent」を選択します。
[Detail]パネルでComponentの構成を確認します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-component/2022-02-23-17-00-47.png)

[Detail]パネルに表示される名称は、VarableName（左）、SubobjectFName（右）、（Inherited）は継承したという意味です。
SubobjectFNameには任意の文字列を設定できます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-component/2022-02-11-21-31-50.png)

### StaticMeshComponentを追加する

次に、[**StaticMeshComponent**]を追加します。
VariableNameは「StaticMesh」に設定します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-component/2022-02-11-21-32-57.png)

StaticMeshComponentのStaticMeshには「SM_SampleActor」を設定します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-component/2022-01-27-11-21-33.png)

「**CPPComponent.hのpublic**」に変数を追加します。

- VariableType：UStaticMeshComponent*
- VariableName：StaticMesh

```cpp:CPPComponent.h
public:
	// StaticMesh Component
	UPROPERTY(EditAnywhere)
	UStaticMeshComponent* StaticMesh;
```

[StaticMeshComponent StaticMesh]を追加します。
変数[StaticMesh]のStaticMeshプロパティに「SM_SampleActor」を設定します。
変数[StaticMesh]は[SceneComponent DefaultSceneRoot]にアタッチします。

```cpp:CPPComponent.cpp
// Sets default values
ACPPComponent::ACPPComponent()
{
	// SceneComponentをRootComponentに設定する。
	DefaultSceneRoot = CreateDefaultSubobject<USceneComponent>(TEXT("SceneComponent"));

	// SceneComponentをRootComponentに設定する
	RootComponent = DefaultSceneRoot;

	// StaticMeshComponentを作成する
	StaticMesh = CreateDefaultSubobject<UStaticMeshComponent>(TEXT("StaticMeshComponent"));

	// StaticMeshをLaodしてStaticMeshComponentのStaticMeshに設定する
	UStaticMesh* Mesh = LoadObject<UStaticMesh>(NULL, TEXT("/Game/CPP_BP/Meshes/SM_SampleCube"), NULL, LOAD_None, NULL);
	StaticMesh->SetStaticMesh(Mesh);

	// StaticMeshComponentをRootComponentにAttachする
	StaticMesh->SetupAttachment(RootComponent);
}
```

StaticMeshComponentからSceneComponentのアタッチはSetupAttachment関数で行っています。

```cpp
(Componentの変数名)->SetupAttachment( (Attachしたい親となるComponentの変数名)　);
```

StaticMeshの読み込み処理はLoadObject関数で行っています。
2番目の引数で[SM_SampleCube]のパス（ファイルまでの場所を表す文字列）をしています。
Pathが分からない時はアセットをマウスオーバーすると、「 Path：/Game/CPP_BP/Meshes 」とSM_SampleCubeが置かれているフォルダまでの文字列書かれています。
「/Game/CPP_BP/Meshes/SM_SampleCube 」とすることで、「SM_SampleCube」の場所を指定できます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-component/2022-02-23-17-08-43.png)

ソースコードを保存して、Compileを実行します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-print_string/2022-02-23-10-58-50.png)

Compileを行うと、変数[DefaultSceneRoot]の子として[StaticMesh]が追加されます。
[StaticMesh]プロパティには「SM_SampleCube」が設定されています。
Viewportには「SM_SampleCube」が表示されます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-component/2022-02-11-21-46-44.png)

### ArrowComponentを追加する

次に、[ArrowComponent]を追加します。
VariableNameは「Arrow」に設定します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-component/2022-02-11-21-47-47.png)

「Arrow」は位置を移動したので、Locationの設定を変更します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-component/2022-01-27-11-24-53.png)

「CPPComponent.h」を編集します。
[ArrowComponent]をC++で宣言する時にはヘッダファイル「ArrowComponent.h」をincludeします。
ArrowComponent.hの親フォルダである[Components]までしかIncludePathが設定されていないので、"Components/ArrowComponent.h"と記述します。

```cpp:CPPComponent.h
#include "Components/ArrowComponent.h" // 追加
```

[ArrowComponent]の変数を宣言します。

- VariableType：UArrowComponent*
- VariableName：Arrow

プロパティ識別子のVisibleAnywhereは、プロパティは表示されるが、設定を変更できないようにする設定です。

```cpp:CPPComponent.h
public:
	// Arrow Component
	UPROPERTY(VisibleAnywhere)
	UArrowComponent* Arrow;
```

「CPPComponent.cpp」ACPPComponent関数 （Constractor）を編集します。
ArrowComponentを作成します。
位置を設定します（SetRelativeLocation関数）。
StaticMeshにArrowをアタッチします。

```cpp:CPPComponent.cpp
// Sets default values
ACPPComponent::ACPPComponent()
{
 	// Set this actor to call Tick() every frame.  You can turn this off to improve performance if you don't need it.
	PrimaryActorTick.bCanEverTick = true;

	// SceneComponentを作成する
	DefaultSceneRoot = CreateDefaultSubobject<USceneComponent>(TEXT("SceneComponent"));

	// SceneComponentをRootComponentに設定する
	RootComponent = DefaultSceneRoot;

	// StaticMeshComponentを作成する
	StaticMesh = CreateDefaultSubobject<UStaticMeshComponent>(TEXT("StaticMeshComponent"));

	// StaticMeshをLaodしてStaticMeshComponentのStaticMeshに設定する
	UStaticMesh* Mesh = LoadObject<UStaticMesh>(NULL, TEXT("/Game/CPP_BP/Meshes/SM_SampleCube"), NULL, LOAD_None, NULL);
	StaticMesh->SetStaticMesh(Mesh);

	// StaticMeshComponentをRootComponentにAttachする
	StaticMesh->SetupAttachment(RootComponent);

	// ArrowComponentを作成する
	Arrow = CreateDefaultSubobject<UArrowComponent>(TEXT("ArrowComponent"));
	
	// ArrowComponentの位置を設定する
	Arrow->SetRelativeLocation(FVector(30.0f, 0.0f, 0.0f));

	// ArrowComponentをStaticMeshComponentにAttachする
	Arrow->SetupAttachment(StaticMesh);
}
```

ソースコードを保存して、Compileを実行します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-print_string/2022-02-23-10-58-50.png)

変数[Arrow]が変数[StaticMesh]の子として追加されました。
Locationも移動した位置が設定されています。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-component/2022-02-11-21-57-33.png)

### PointLightComponentを追加する

最後に、[PointLightComponent]を追加します。
VariableNameは「PointLight」に設定します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-component/2022-01-27-11-27-06.png)

[ArrowComponent]と同様に移動した位置をLocationに設定します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-component/2022-01-27-11-27-31.png)

「CPPComponent.h」を編集します。
PointLightComponentもArrowComponentと同様にヘッダファイルのincludeを追加します。

```cpp:CPPComponent.h
#include "Components/PointLightComponent.h" // 追加
```

[PointLightComponent]の変数を追加します。

|               | Value                 |
| ------------- | --------------------- |
| Variable Name | PointLight            |
| Variable Type | UPointLightComponent* |


```cpp:CPPComponent.h
public:
	// PointLightComponent Component
	UPROPERTY(EditAnywhere)
	UPointLightComponent* PointLight;
```

**「CPPComponent.cpp」ACPPComponent関数**（Constractor）を編集します。
PointLightComponentを作成します。
位置を設定します（SetRelativeLocation関数）。
StaticMeshにPointLightをアタッチします。

```cpp:CPPComponent.cpp
// Sets default values
ACPPComponent::ACPPComponent()
{
 	// Set this actor to call Tick() every frame.  You can turn this off to improve performance if you don't need it.
	PrimaryActorTick.bCanEverTick = true;

	// SceneComponentを作成する
	DefaultSceneRoot = CreateDefaultSubobject<USceneComponent>(TEXT("SceneComponent"));

	// SceneComponentをRootComponentに設定する
	RootComponent = DefaultSceneRoot;

	// StaticMeshComponentを作成する
	StaticMesh = CreateDefaultSubobject<UStaticMeshComponent>(TEXT("StaticMeshComponent"));

	// StaticMeshをLaodしてStaticMeshComponentのStaticMeshに設定する
	UStaticMesh* Mesh = LoadObject<UStaticMesh>(NULL, TEXT("/Game/CPP_BP/Meshes/SM_SampleCube"), NULL, LOAD_None, NULL);
	StaticMesh->SetStaticMesh(Mesh);

	// StaticMeshComponentをRootComponentにAttachする
	StaticMesh->SetupAttachment(RootComponent);

	// ArrowComponentを作成する
	Arrow = CreateDefaultSubobject<UArrowComponent>(TEXT("ArrowComponent"));
	
	// ArrowComponentの位置を設定する
	Arrow->SetRelativeLocation(FVector(30.0f, 0.0f, 0.0f));

	// ArrowComponentをStaticMeshComponentにAttachする
	Arrow->SetupAttachment(StaticMesh);

	// PointLightComponentを作成する
	PointLight = CreateDefaultSubobject<UPointLightComponent>(TEXT("PointLightComponent"));

	// PointLightComponentの位置を設定する
	PointLight->SetRelativeLocation(FVector(130.0f, 0.0f, 0.0f));

	// PointLightComponentをStaticMeshComponentにAttachする
	PointLight->SetupAttachment(StaticMesh);
}
```

ソースコードを保存して、Compileを実行します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-print_string/2022-02-23-10-58-50.png)

[PointLight]が[StaticMesh]の子として追加されました。
Locationも移動した位置に設定されています。
ViewportにPointLightが表示されました。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-component/2022-02-11-22-10-00.png)

[Play]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-print_string/2022-02-23-09-19-08.png)

BlueprintとC++同じ構成のComponentを実装した状態です。
当然ながら同じ動きをします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-component/2022-02-23-17-12-51.png)

### すべて保存する

C++側の説明は以上になります。
プロジェクトをすべて保存しましょう。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-component/2022-02-23-17-13-46.png)

Visual StudioのSolutionもすべて保存しましょう。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-flow_control_switch/2022-01-23-21-46-14.png)

## ソースコードとプロジェクト

ここまでのソースコードとプロジェクトファイルをGitHubからダウンロードできます。

https://github.com/posita33/UE5Starter-CPPAndBP_Projects/tree/main/Resources/Chapter_02/Component

**CPPComponent.h**

https://github.com/posita33/UE5Starter-CPPAndBP_Projects/blob/main/Resources/Chapter_02/Component/Source_end/CPP_BP/Public/CPPComponent.h


**CPPComponent.cpp**

https://github.com/posita33/UE5Starter-CPPAndBP_Projects/blob/main/Resources/Chapter_02/Component/Source_end/CPP_BP/Private/CPPComponent.cpp