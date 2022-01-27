---
title: "【C++】Componentを追加する"
emoji: "🐷"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["cpp", "unrealengine", "ue4", "ue5"]
published: false
---

## 【C++版】Componentを追加する

### C++でBlueprintを再現すること

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-component/2022-01-27-11-11-29.png)

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-component/2022-01-27-11-11-38.png)

### Visual Studioを開いて、編集するファイルを表示する

プロジェクトを閉じていたら、プロジェクトを開き、「Chapter_2_5_Component」を開きます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-component/2022-01-27-11-14-47.png)

ToolsからVisual Studioを開きます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-component/2022-01-27-11-15-07.png)

Solution Explorerから今回編集する2つのファイルを開きます。

- CPPSampleActor.cpp
- CPPSampleActor.h

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-component/2022-01-27-11-15-25.png)

Blueprintで追加したComponentとComponentの親子構成をC++で再現します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-component/2022-01-27-11-15-45.png)

### SceneComponentをRootComponentに設定する

Componentの一番上の階層のことをSceneRootと呼びます。
Actorを親クラスにしたBlueprintには最初RootComponentにSceneComponentが設定されています。
SceneComponentは階層のグループを作成したりする、Transform情報だけ持つコンポーネントです。
C++でRootComponentにSceneComponentを設定する処理を実装します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-component/2022-01-27-11-16-33.png)

「CPPSampleActor.hのpublic」に変数を追加します。

- VariableType：USceneComponent*
- VariableName：DefaultSceneRoot

USceneComponent*の「*」はポインタです。
「USceneComponentのポインタ型」というのが正式な名称です。
ポインタについては別の機会で説明します。

```cpp:CPPSampleActor.h
	// Sceneコンポーネント
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

**「CPPSampleActor.cpp」ACPPSampleActor関数 （Constractor）**
[SceneComponent：DefaultSceneRoot]を[RootComponent]に設定する処理を実装します。
クラス名::クラス名()はConstructorです。Constructorはクラスを作成する時に呼ばれる関数です。BeginePlay関数より先に呼ばれます。

**Componentの追加や設定はConstructorで行います。**

```cpp:.cpp
ACPPSampleActor::ACPPSampleActor()
{
 	// Set this actor to call Tick() every frame.  You can turn this off to improve performance if you don't need it.
	PrimaryActorTick.bCanEverTick = true;

	// SceneComponentを作成する
	DefaultSceneRoot = CreateDefaultSubobject<USceneComponent>(TEXT("SceneComponent"));

	// SceneComponentをRootComponentに設定する
	RootComponent = DefaultSceneRoot;
}
```

Ctrl + Sでファイルを保存し、Compileを行います。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-component/2022-01-27-11-20-00.png)

C++ではBlueprintのようにEditorで確認することが出来ないので、レベルに配置した「CPPSampleActor」を選択します。
[Derail]パネルでComponentの構成を確認します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-component/2022-01-27-11-20-18.png)

Detailパネルに表示される名称は、VarableName（左）、SubobjectFName（右）、（Inherited）は継承したという意味です。
SubobjectFNameには任意の文字列を設定できます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-component/2022-01-27-11-20-40.png)

### StaticMeshComponentを追加する
次に、[**StaticMeshComponent**]を追加します。
VariableNameは「StaticMesh」に設定します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-component/2022-01-27-11-21-04.png)

StaticMeshComponentのStaticMeshには「SM_SampleActor」を設定します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-component/2022-01-27-11-21-33.png)

「**CPPSampleActor.hのpublic**」に変数を追加します。

- VariableType：UStaticMeshComponent*
- VariableName：StaticMesh

```cpp:CPPSampleActor.h
public:
	// StaticMesh Component
	UPROPERTY(EditAnywhere)
	UStaticMeshComponent* StaticMesh;
```

[StaticMeshComponent StaticMesh]を追加します。
変数[StaticMesh]のStaticMeshプロパティに「SM_SampleActor」を設定します。
変数[StaticMesh]は[SceneComponent DefaultSceneRoot]にアタッチします。

```cpp:CPPSampleActor.cpp
// Sets default values
ACPPSampleActor::ACPPSampleActor()
{
 	// Set this actor to call Tick() every frame.  You can turn this off to improve performance if you don't need it.
	PrimaryActorTick.bCanEverTick = true;

	// SceneComponentをRootComponentに設定する。
	DefaultSceneRoot = CreateDefaultSubobject<USceneComponent>(TEXT("SceneComponent"));
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

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-component/2022-01-27-11-23-43.png)


Ctrl + Sでファイルを保存し、Compileを行います。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-component/2022-01-27-11-24-04.png)

Compileを行うと、変数[DefaultSceneRoot]の子として[StaticMesh]が追加されます。
[StaticMesh]プロパティには「SM_SampleCube」が設定されています。
Viewportには「SM_SampleCube」が表示されます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-component/2022-01-27-11-24-20.png)

### ArrowComponentを追加する
次に、[ArrowComponent]を追加します。
VariableNameは「Arrow」に設定します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-component/2022-01-27-11-24-40.png)

「Arrow」は位置を移動したので、Locationの設定を変更します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-component/2022-01-27-11-24-53.png)

「CPPSampleActor.h」を編集します。
[ArrowComponent]をC++で宣言する時にはヘッダファイル「ArrowComponent.h」をincludeします。
ArrowComponent.hの親フォルダである[Component]までしかIncludePathが設定されていないので、"Components/ArrowComponent.h"と記述します。

```cpp
#include "Components/ArrowComponent.h" // 追加
```

[ArrowComponent]の変数を宣言します。

- VariableType：UArrowComponent*
- VariableName：Arrow

プロパティ識別子のVisibleAnywhereは、プロパティは表示されるが、設定を変更できないようにする設定です。

```cpp
public:
	// Arrow Component
	UPROPERTY(VisibleAnywhere)
	UArrowComponent* Arrow;
```

「CPPSampleActor.cpp」ACPPSampleActor関数 （Constractor）を編集します。
ArrowComponentを作成します。
位置を設定します（SetRelativeLocation関数）。
StaticMeshにArrowをアタッチします。

```cpp:CPPSampleActor.cpp
// Sets default values
ACPPSampleActor::ACPPSampleActor()
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
	Arrow->SetRelativeLocation(FVector(30.0f, 0.0f, 0.0f));
	Arrow->SetupAttachment(StaticMesh);
}
```
Ctrl + Sでファイルを保存し、Compileを行います。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-component/2022-01-27-11-26-37.png)

変数[Arrow]が変数[StaticMesh]の子として追加されました。
Locationも移動した位置が設定されています。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-component/2022-01-27-11-26-50.png)

### PointLightComponentを追加する

最後に、[PointLightComponent]を追加します。
VariableNameは「PointLight」に設定します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-component/2022-01-27-11-27-06.png)


[ArrowComponent]と同様に移動した位置をLocationに設定します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-component/2022-01-27-11-27-31.png)

「CPPSampleActor.h」を編集します。
PointLightComponentもArrowComponentと同様にヘッダファイルのincludeを追加します。

```cpp:CPPSampleActor.h
#include "Components/PointLightComponent.h" // 追ぷ
```

[PointLightComponent]の変数を追加します。

- VariableType：UPointLightComponent*
- VariableName：PointLight

```cpp:CPPSampleActor.h
public:
	// PointLightComponent Component
	UPROPERTY(EditAnywhere)
	UPointLightComponent* PointLight;
```

**「CPPSampleActor.cpp」ACPPSampleActor関数 **（Constractor）を編集します。
ArrowComponentを作成します。
位置を設定します（SetRelativeLocation関数）。
StaticMeshにArrowをアタッチします。

```cpp:CPPSampleActor.cpp
// Sets default values
ACPPSampleActor::ACPPSampleActor()
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

Ctrl + Sでファイルを保存し、Compileを行います。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-component/2022-01-27-11-29-25.png)

[PointLight]が[StaticMesh]の子として追加されました。
Locationも移動した位置に設定されています。
ViewportにPointLightが表示されました。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-component/2022-01-27-11-29-35.png)

[Play]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-component/2022-01-27-11-29-45.png)

BlueprintとC++同じ構成のComponentを実装した状態です。
当然ながら同じ動きをします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-component/2022-01-27-11-30-11.png)

### すべて保存

C++側の説明は以上になります。
プロジェクトをすべて保存しましょう。

【要画像差し替え】。
![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-function/2022-01-26-16-00-41.png)

Visual StudioのSolutionもすべて保存しましょう。
![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-flow_control_switch/2022-01-23-21-46-14.png)

### 最終的なソースコード

```cpp:CPPSampleActor.h
// Fill out your copyright notice in the Description page of Project Settings.

#pragma once

#include "CoreMinimal.h"
#include "GameFramework/Actor.h"
#include "Components/ArrowComponent.h" // 追加
#include "Components/PointLightComponent.h" // 追加
#include "CPPSampleActor.generated.h"


UCLASS()
class CPP_BP_API ACPPSampleActor : public AActor
{
	GENERATED_BODY()
	
public:	
	// Sets default values for this actor's properties
	ACPPSampleActor();

	// Scene Component
	UPROPERTY(EditAnywhere)
	USceneComponent* DefaultSceneRoot;

	// StaticMesh Component
	UPROPERTY(EditAnywhere)
	UStaticMeshComponent* StaticMesh;

	// Arrow Component
	UPROPERTY(VisibleAnywhere)
	UArrowComponent* Arrow;

	// PointLightComponent Component
	UPROPERTY(EditAnywhere)
	UPointLightComponent* PointLight;

	// DurationのGet関数
	float GetDuration() { return Duration; }

	// TextColorのGet関数
	FLinearColor GetTextColor() { return TextColor; }

protected:
	// Called when the game starts or when spawned
	virtual void BeginPlay() override;

public:	
	// Called every frame
	virtual void Tick(float DeltaTime) override;

private:
	// PrintString関数のDurationに設定する変数
	const float Duration = 10.0f;

	// PrintString関数のTextColorに設定する変数
	const FLinearColor TextColor = FColor(255, 255, 255);
};
```

```cpp:CPPSampleActor.cpp ACPPSampleActor() （Constructor）
// Sets default values
ACPPSampleActor::ACPPSampleActor()
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

