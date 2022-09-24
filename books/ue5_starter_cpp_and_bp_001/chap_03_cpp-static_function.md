---
title: "【C++】静的メンバ関数"
free: false
---

## 静的メンバ関数

### 静的メンバ関数について

静的メンバ変数はメモリ割り当て方法が変わります。
静的メンバ関数は静的メンバ変数にアクセスできるメンバ関数です。


### 静的メンバ関数を変更する静的メンバ関数を追加する

「CPPStatic」に静的メンバ関数を追加します。

```cpp:CPPStatic.h
// Fill out your copyright notice in the Description page of Project Settings.

#pragma once

#include "CoreMinimal.h"
#include "GameFramework/Actor.h"
#include "CPPStatic.generated.h"

UCLASS()
class CPP_BP_API ACPPStatic : public AActor
{
	GENERATED_BODY()
	
public:
	
	// staticメンバ関数
	static void SetPoint(int myPoint);

	// staticメンバ変数
	static int staticPoint;

	// 通常のメンバ変数
	int normalPoint;
};

```

```cpp:CPPParentVirtual.cpp
// Fill out your copyright notice in the Description page of Project Settings.


#include "CPPStatic.h"

void ACPPStatic::SetPoint(int myPoint)
{
	staticPoint = myPoint;
}

```

### 静的メンバ関数の動作確認をする


```cpp:CPPStaticTest.cpp
// Fill out your copyright notice in the Description page of Project Settings.


#include "CPPStaticTest.h"
#include "CPPStatic.h"
#include "Kismet/KismetSystemLibrary.h"

int ACPPStatic::staticPoint = 400;

// Called when the game starts or when spawned
void ACPPStaticTest::BeginPlay()
{
	Super::BeginPlay();

	// CPPStaticを生成する
	ACPPStatic* staticActorA = GetWorld()->SpawnActor<ACPPStatic>(ACPPStatic::StaticClass());
	// メンバ変数を設定する
	staticActorA->normalPoint = 100;

	// CPPStaticを生成する
	ACPPStatic* staticActorB = GetWorld()->SpawnActor<ACPPStatic>(ACPPStatic::StaticClass());
	// メンバ変数を設定する
	staticActorB->normalPoint = 200;

	// 静的メンバ関数を呼び出す
	ACPPStatic::SetPoint(500);
	staticActorA->SetPoint(600);

	UKismetSystemLibrary::PrintString(this, FString::Printf(TEXT("staticActorA staticPoint : %d, normalPoint : %d"), ACPPStatic::staticPoint, staticActorA->normalPoint), true, true, FColor::Cyan, 10.f);

	UKismetSystemLibrary::PrintString(this, FString::Printf(TEXT("staticActorB staticPoint : %d, normalPoint : %d"), staticActorB->staticPoint, staticActorB->normalPoint), true, true, FColor::Red, 10.f);

}

```

ソースコードを保存して、Compileを実行します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_constructor_destructor/2022-07-24-15-49-43.png)

Level Editorの[Play]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_constructor_destructor/2022-07-24-15-50-06.png)

静的メンバ関数から静的メンバ変数を変更できました。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_cpp-static_variable_and_function/2022-09-23-23-28-32.png)

