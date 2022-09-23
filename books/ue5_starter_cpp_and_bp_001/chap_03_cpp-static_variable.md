---
title: "【CPP】静的メンバ変数"
free: false
---

## 静的メンバ変数

### 静的メンバ変数について

C++ではクラスに静的メンバ変数と静的メンバ関数を定義できます。
通常のメンバ変数と静的メンバ変数の違いはメモリ割り当て方法が変わります。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_cpp-static_variable/2022-09-24-00-16-00.png)

### 静的メンバ変数を持つクラスを作成する

静的メンバ変数を持つクラス「CPPStatic」を作成します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_cpp-redefinition_of_function/2022-09-10-18-27-18.png)

親クラスに[Actor]を選択します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_cpp-redefinition_of_function/2022-09-10-18-29-04.png)

ClassTypeとClass名を設定します。

| Property   | Value     |
| ---------- | --------- |
| Class Type | Public    |
| Name       | CPPStatic |

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_cpp-static_variable_and_function/2022-09-23-14-48-15.png)

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
	// 静的メンバ変数
	static int staticPoint;

	// 通常のメンバ変数
	int normalPoint;
};

```

```cpp:CPPParentVirtual.cpp
// Fill out your copyright notice in the Description page of Project Settings.


#include "CPPStatic.h"


```

### 静的メンバ変数の動作確認するクラスを作成する

静的メンバ変数を動作確認する「CPPStaticTest」を作成します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_cpp-redefinition_of_function/2022-09-10-18-27-18.png)

親クラスに[Actor]を選択します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_cpp-redefinition_of_function/2022-09-10-18-29-04.png)

ClassTypeとClass名を設定します。

| Property   | Value         |
| ---------- | ------------- |
| Class Type | Public        |
| Name       | CPPStaticTest |

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_cpp-static_variable_and_function/2022-09-23-15-14-47.png)

```cpp:CPPStaticTest.h
// Fill out your copyright notice in the Description page of Project Settings.

#pragma once

#include "CoreMinimal.h"
#include "GameFramework/Actor.h"
#include "CPPStaticTest.generated.h"

UCLASS()
class CPP_BP_API ACPPStaticTest : public AActor
{
	GENERATED_BODY()

protected:
	// Called when the game starts or when spawned
	virtual void BeginPlay() override;

};

```

```cpp:CPPStaticTest.cpp
// Fill out your copyright notice in the Description page of Project Settings.


#include "CPPStaticTest.h"
#include "CPPStatic.h"
#include "Kismet/KismetSystemLibrary.h"

// Satic変数を初期化する
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

	UKismetSystemLibrary::PrintString(this, FString::Printf(TEXT("staticActorA staticPoint : %d, normalPoint : %d"), ACPPStatic::staticPoint, staticActorA->normalPoint), true, true, FColor::Cyan, 10.f);

	UKismetSystemLibrary::PrintString(this, FString::Printf(TEXT("staticActorB staticPoint : %d, normalPoint : %d"), staticActorB->staticPoint, staticActorB->normalPoint), true, true, FColor::Red, 10.f);

}

```

ソースコードを保存して、Compileを実行します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_constructor_destructor/2022-07-24-15-49-43.png)

「CPPStaticTest」をViewportにDrag&Dropします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_cpp-static_variable_and_function/2022-09-23-23-26-28.png)

Level Editorの[Play]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_constructor_destructor/2022-07-24-15-50-06.png)

静的メンバ変数は複数のオブジェクトで共通のメモリ領域を持っているので、クラス間で同じ値を参照できます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_cpp-static_variable/2022-09-24-00-00-35.png)

静的メンバ変数の使用方法をまとめました。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_cpp-static_variable/2022-09-24-00-06-55.png)

静的メンバ変数は複数のオブジェクトで共通のメモリ領域を持ちます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_cpp-static_variable/2022-09-24-00-16-34.png)
