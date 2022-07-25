---
title: "ConstructorとDestructor"
free: false
---

## Constructor

### Constructorについて

Constructorはオブジェクトを生成する際に呼び出されるメンバ関数です。
Constructorはデータメンバーの初期化を行うために使用します。

UnrealEngineのActorを継承したクラスではメンバ変数の初期化やコンポーネントの追加を行います。

https://zenn.dev/posita33/books/ue5_starter_cpp_and_bp_001/viewer/chap_02_cpp-component

### Constructorでメンバ変数とコンポーネントを追加する

[Tools]メニューから[New C++ Class]を開きます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_constructor_destructor/2022-07-24-15-03-39.png)

親クラスに[Actor]を選択します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_constructor_destructor/2022-07-24-15-04-49.png)

ClassTypeとClass名を設定します。

| Property   | Value          |
| ---------- | -------------- |
| Class Type | Public         |
| Name       | CPPConstructor |

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_constructor_destructor/2022-07-24-15-09-43.png)

ConstructorでComponentにCubeのStaticMeshを追加し、メンバ変数を初期化する処理を実装します。

```cpp:CPPConstructor.h
// Fill out your copyright notice in the Description page of Project Settings.

#pragma once

#include "CoreMinimal.h"
#include "GameFramework/Actor.h"
#include "CPPConstructor.generated.h"

UCLASS()
class CPP_BP_API ACPPConstructor : public AActor
{
	GENERATED_BODY()
	
public:	
	// Sets default values for this actor's properties
	ACPPConstructor();

protected:
	// Called when the game starts or when spawned
	virtual void BeginPlay() override;

public:
	// Scene Component
	UPROPERTY(EditAnywhere)
	USceneComponent* DefaultSceneRoot;

	// StaticMesh Component
	UPROPERTY(EditAnywhere)
	UStaticMeshComponent* StaticMesh;

private:

	// HP
	int hp = 0;

};
```

```cpp:CPPConstructor.cpp
// Fill out your copyright notice in the Description page of Project Settings.


#include "CPPConstructor.h"
#include "Kismet/KismetSystemLibrary.h"

// Sets default values
ACPPConstructor::ACPPConstructor()
{
	// メンバ変数を初期化する
	hp = 100;

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

// Called when the game starts or when spawned
void ACPPConstructor::BeginPlay()
{
	Super::BeginPlay();

	// Constructorで初期化した変数をPrintStringで出力する
	UKismetSystemLibrary::PrintString(this, FString::Printf(TEXT("%d"), hp), true, true, FColor::Cyan, 2.f);
}

```

このソースコードの中でConstructorの宣言は以下のように設定します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_constructor_destructor/2022-07-24-16-00-15.png)

ソースコードを保存して、Compileを実行します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_constructor_destructor/2022-07-24-15-49-43.png)

「CPPConstructor」をViewportにDrag&Dropします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_constructor_destructor/2022-07-24-15-47-19.png)

Level Editorの[Play]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_constructor_destructor/2022-07-24-15-50-06.png)

PrintStringでメンバ変数「hp」を出力した結果はConstructorで設定した値になります。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_constructor_destructor/2022-07-24-15-56-41.png)

BeginPlayよりConstructorの方が早く呼ばれるので、headerファイルで設定したDefault ValueがConstructorで上書きされます。その後にBeginPlayが呼ばれます。

Actorのイベントの呼ばれる順序は以下の公式ドキュメントで説明されています。

https://docs.unrealengine.com/4.27/ja/ProgrammingAndScripting/ProgrammingWithCPP/UnrealArchitecture/Actors/ActorLifecycle/

## Destructor

オブジェクトを破棄する時に呼び出されるメンバ関数がDestructorです。
Destructorはリソースの解放を行うために使用します。
**デストラクタは宣言しなくても自動的に呼ばれます。**

```cpp:CPPConstructor.h
UCLASS()
class CPP_BP_API ACPPConstructor : public AActor
{
	GENERATED_BODY()
	
public:	
	// Sets default values for this actor's properties
	ACPPConstructor();

	// Destructor
	~ACPPConstructor();
```
Destructorが呼ばれた時にPrintStringで文字を出力する処理を実装します。

```cpp:CPPConstructor.c
ACPPConstructor::~ACPPConstructor()
{
	// DestructorでPrintString
	UKismetSystemLibrary::PrintString(this, TEXT("Destructor Class destroyed"), true, true, FColor::Cyan, 2.f);
}
```

LevelBlueprintにDキーが押された時に配置したCPPConstructorのActorを削除する処理を実装します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_constructor_destructor/2022-07-24-16-26-43.png)

「Get All Actors Of Class」ノードでViewportに配置された「CPPConstructor」を取得します。
取得したActorクラスから「Destroy Actor」を呼ぶことでActorを破棄できます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_constructor_destructor/2022-07-26-06-20-50.png)

ソースコードを保存して、Compileを実行します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_constructor_destructor/2022-07-24-15-49-43.png)

Level Editorの[Play]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_constructor_destructor/2022-07-24-15-50-06.png)

プレイ中に「D」キーを入力することでアクタが削除されます。
しかし、PrintStringの文字は出力されません。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_constructor_destructor/2022-07-26-06-27-51.png)

Output Logを開くとDestructorでPrintStringに渡した文字列情報が出力されています。
Dキーで削除した時に直ぐに呼ばれた時に、出力されるのではなく少し時間が経ってから出力されます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_constructor_destructor/2022-07-26-06-30-30.png)

Destroyが呼ばれた時にフラグが立って、次のガーベジコレクションでメモリを解放する時に呼ばれるためです。

> 次のガーベジ コレクション サイクルでメモリを解放するために、アクタは RF_PendingKill とマーク付けされます。また手動で保留中のキルをチェックせずに、よりクリーンな FWeakObjectPtr<AActor> の使用を考慮してください。

https://docs.unrealengine.com/5.0/ja/unreal-engine-actor-lifecycle/

https://ja.wikipedia.org/wiki/%E3%82%AC%E3%83%99%E3%83%BC%E3%82%B8%E3%82%B3%E3%83%AC%E3%82%AF%E3%82%B7%E3%83%A7%E3%83%B3

## Actorクラスの終了処理はEndPlayで実装する

Actorクラスを継承したクラスで終了処理はDestructorで書くより、EndPlayで実装します。
ヘッダファイルにEndPlayを宣言します。

```cpp:CPPConstructor.h
UCLASS()
class CPP_BP_API ACPPConstructor : public AActor
{
	GENERATED_BODY()
	
protected:
	// Called when the game starts or when spawned
	virtual void BeginPlay() override;

	virtual void EndPlay(const EEndPlayReason::Type EndPlayReason) override;
```

EndPlayに処理を実装します。

```cpp:CPPConstructor.cpp
void ACPPConstructor::EndPlay(const EEndPlayReason::Type EndPlayReason)
{
	// EndPlayでPrintString
	UKismetSystemLibrary::PrintString(this, TEXT("EndPlay Class destroyed"), true, true, FColor::Cyan, 2.f);
}
```

ソースコードを保存して、Compileを実行します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_constructor_destructor/2022-07-24-15-49-43.png)

Level Editorの[Play]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_constructor_destructor/2022-07-24-15-50-06.png)

プレイ中に「D」キーを入力し、アクタが削除された時に、PrintStringの文字が出力されます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_constructor_destructor/2022-07-26-07-05-43.png)

UnraelEngineでは通常のC++と同じ処理も実装出来ますが、UnrealEngineが用意しているUOBjectクラスやActorクラスを継承する際にはまとめて処理を行うように設計されているので処理の呼び方を意識して使用する必要があります。

「::~」でEnginソースを含めたプロジェクトを全検索すると使用方法を確認できます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_constructor_destructor/2022-07-26-07-17-35.png)

## Blueprintの終了処理

親クラスが「Actor」のBlueprint「BP_Constructor」を作成します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_constructor_destructor/2022-07-26-07-26-49.png)

「Event End Play」、「Event Destroyed」ノードにそれぞれPrintStringを呼び出すように実装します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_constructor_destructor/2022-07-26-07-28-34.png)

BP_ConstructorをViewportに配置します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_constructor_destructor/2022-07-26-07-30-27.png)



LevelBlueprintにDキーが押された時に配置したBPConstructorのActorも削除する処理を実装します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_constructor_destructor/2022-07-24-16-26-43.png)

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_constructor_destructor/2022-07-26-07-32-52.png)

Level Editorの[Play]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_constructor_destructor/2022-07-24-15-50-06.png)

「D」キーを入力した時にBlueprintの終了処理が実行されます。
「EndPlay」-> 「Destroyed」の順番に呼ばれていることが分かります。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_constructor_destructor/2022-07-26-07-34-19.png)

## レベル遷移時に呼ばれる

Destroyノードで破棄する時以外にも、レベルを遷移する際にActorの終了処理が呼ばれます。

レベルブループリントに「1」キーを押した時に、レベル遷移する処理を実装します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_constructor_destructor/2022-07-26-07-38-16.png)

Level Editorの[Play]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_constructor_destructor/2022-07-24-15-50-06.png)

1キーを入力するとBlueprintとC++のActorクラスの終了処理が呼ばれます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_constructor_destructor/2022-07-26-07-40-13.png)

EndPlayが呼ばれる場所です。

>・Destroy の明示的な呼出し
・Play in Editor を終了
・レベル移行 (シームレスな移動またはマップのロード)
・アクタを含むストリーミング レベルをアンロード
・アクタのライフタイムの期限が終了
・アプリケーションをシャットダウン (全アクタを破壊)

公式ドキュメントを一度目を通しておくことをおススメします。

https://docs.unrealengine.com/5.0/ja/unreal-engine-actor-lifecycle/


## ソースコード

https://github.com/posita33/UE5Starter-CPPAndBP_Projects/blob/main/Resources/Chapter_03/ConstructorAndDestructor/Public/CPPConstructor.h

https://github.com/posita33/UE5Starter-CPPAndBP_Projects/blob/main/Resources/Chapter_03/ConstructorAndDestructor/Private/CPPConstructor.cpp
