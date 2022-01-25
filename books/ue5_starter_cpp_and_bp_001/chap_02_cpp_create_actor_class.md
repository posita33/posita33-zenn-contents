---
title: "2.2.CPP クラス(親クラス：Actor)を作成する"
free: false
---

## C++のクラス（親クラス：Actor）を追加する
C++のクラスを新規作成します。
メニューから作成する方法と、コンテンツブラウザから作成する方法があります。
・[Tools]メニューから[New C++ Class…]を選択する
・コンテンツブラウザの[C++ Classes]を選択すると右クリックやAddボタンのメニューが変わる。[New C++ Class…]を選択する
![](https://storage.googleapis.com/zenn-user-upload/9dca4066fbd6-20220110.png)

親クラスを選択します。
[Actor]を選択して、[Next >]をクリックします。
![](https://storage.googleapis.com/zenn-user-upload/199eda59b081-20220110.png)

Class TypeとClass名を設定して、[Create Class]をクリックします。

|Property|Value|
|---|---|
|Class Type|Public|
|Name|CPPSampleActor|
![](https://storage.googleapis.com/zenn-user-upload/59f94540abb6-20220110.png)

コンテンツブラウザのC++ Classesフォルダ側に作成したC++のクラスが追加されます。
![](https://storage.googleapis.com/zenn-user-upload/a41809c2a4f3-20220110.png)

Visual Studio側を確認します。
Solution Explorerにソースコードが追加されています。
Publicフォルダ：「CPPSampleActor.h」（ヘッダーファイル）
Privateフォルダ：「CPPSampleActor.cpp」（C++ファイル）

![](https://storage.googleapis.com/zenn-user-upload/7a257183e84d-20220110.png)

**CPPSampleActor.h（ヘッダーファイル）**
ヘッダーファイルは関数の宣言や変数の定義を書いていきます。

```cpp
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

protected:
	// Called when the game starts or when spawned
	virtual void BeginPlay() override;

public:	
	// Called every frame
	virtual void Tick(float DeltaTime) override;

};
```

**CPPSampleActor.cpp（C++ファイル）**
C++ファイルはヘッダーファイルで宣言した関数の処理を実装します。

```cpp
// Fill out your copyright notice in the Description page of Project Settings.


#include "CPPSampleActor.h"

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
	
}

// Called every frame
void ACPPSampleActor::Tick(float DeltaTime)
{
	Super::Tick(DeltaTime);

}
```

## コーディング規約
C++側にはファイル名の命名規則といったものは用意されていないのですが、

**「コーディング規約」**

という、こういう風にソースコードを書いてね。と定められているルールがあります。
コチラもチーム開発でルールが決まっていないのであれば、参考にするとソースコードのばらつきが無くなります。
https://docs.unrealengine.com/4.27/ja/ProductionPipelines/DevelopmentSetup/CodingStandard/

GitHubで少し情報が古いですが、いい書き方、悪い書き方をまとめている方がいました。
https://github.com/DaedalicEntertainment/unreal-coding-conventions

