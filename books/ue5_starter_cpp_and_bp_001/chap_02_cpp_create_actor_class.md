---
title: "【C++】Actorクラスを作成する"
free: false
---

## 【C++】Actorクラスを作成する

### C++でBlueprintを再現すること

C++でクラス（親クラス：Actor）を作成できます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp_create_actor_class/2022-02-07-06-57-33.png)

### C++のクラス（親クラス：Actor）を追加する

C++のクラスを新規作成します。

メニューから作成する方法と、[Content Drawer]から作成する方法があります。

・[Tools]メニューから[New C++ Class…]を選択する
・[Content Drawer]の[C++ Classes]を選択すると右クリックやAddボタンのメニューが変わる。[New C++ Class…]を選択する。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp_create_actor_class/2022-02-07-06-36-23.png)

親クラスを選択します。
[Actor]を選択して、[Next >]をクリックします。

![](https://storage.googleapis.com/zenn-user-upload/199eda59b081-20220110.png)

Class TypeとClass名を設定して、[Create Class]をクリックします。

| Property   | Value         |
| ---------- | ------------- |
| Class Type | Public        |
| Name       | CPPHelloWorld |

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp_create_actor_class/2022-02-07-06-38-53.png)

[Content Drawer]の[C++ Classes]フォルダ側に作成したC++のクラスが追加されます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp_create_actor_class/2022-02-07-06-45-29.png)

Visual Studio側を確認します。

プロジェクトに変更があったので、確認のダイアログが表示されます。
[Reload All]ボタンをクリックすると変更が反映されます。（以後、この工程は省略します。）

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp_create_actor_class/2022-02-07-06-44-18.png)

[Solution Explorer]にソースコードが追加されています。
[Solution Explorer]はUnreal Engineの[Content Drawer]のようにVisual StudioのSolutionを管理する機能です。

- Publicフォルダ：「CPPHelloWorld.h」（ヘッダーファイル）
- Privateフォルダ：「CPPHelloWorld.cpp」（C++ファイル）

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp_create_actor_class/2022-02-07-06-49-01.png)

**CPPHelloWorld.h（ヘッダーファイル）**
ヘッダーファイルは関数の宣言や変数の定義を書いていきます。

```cpp
// Fill out your copyright notice in the Description page of Project Settings.

#pragma once

#include "CoreMinimal.h"
#include "GameFramework/Actor.h"
#include "CPPHelloWorld.generated.h"

UCLASS()
class CPP_BP_API ACPPHelloWorld : public AActor
{
	GENERATED_BODY()
	
public:	
	// Sets default values for this actor's properties
	ACPPHelloWorld();

protected:
	// Called when the game starts or when spawned
	virtual void BeginPlay() override;

public:	
	// Called every frame
	virtual void Tick(float DeltaTime) override;

};
```

**CPPHelloWorld.cpp（C++ファイル）**
C++ファイルはヘッダーファイルで宣言した関数の処理を定義します。

```cpp
// Fill out your copyright notice in the Description page of Project Settings.


#include "CPPHelloWorld.h"

// Sets default values
ACPPHelloWorld::ACPPHelloWorld()
{
 	// Set this actor to call Tick() every frame.  You can turn this off to improve performance if you don't need it.
	PrimaryActorTick.bCanEverTick = true;

}

// Called when the game starts or when spawned
void ACPPHelloWorld::BeginPlay()
{
	Super::BeginPlay();
	
}

// Called every frame
void ACPPHelloWorld::Tick(float DeltaTime)
{
	Super::Tick(DeltaTime);

}
```

### すべて保存

C++側の説明は以上になります。

Visual StudioのSolutionをすべて保存しましょう。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp_create_actor_class/2022-02-07-06-53-51.png)


## コーディング規約

C++側にはファイル名の命名規則といったものは用意されていません。

**「コーディング規約」**

という、こういう風にソースコードを書いてね。と定められているルールがあります。
コチラもチーム開発でルールが決まっていないのであれば、参考にするとソースコードのばらつきが無くなります。

https://docs.unrealengine.com/4.27/ja/ProductionPipelines/DevelopmentSetup/CodingStandard/

GitHubで少し情報が古いですが、いい書き方、悪い書き方をまとめている方がいました。

https://github.com/DaedalicEntertainment/unreal-coding-conventions
