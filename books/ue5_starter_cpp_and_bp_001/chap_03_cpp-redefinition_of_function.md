---
title: "【CPP】メンバ関数の再定義"
free: false
---

## メンバ関数の再定義

### 基底クラスのメンバ関数を再定義する

基底クラスのメンバ関数は、派生クラスで定義し直せます。
メンバ変数を設定するSetPointを派生クラスで再定義します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_cpp-redefinition_of_function/2022-09-17-23-54-22.png)

### 基底クラス「CPPParentRedefinition」を作成する

基底クラス「CPPParentRedefinition」を作成します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_cpp-redefinition_of_function/2022-09-10-18-27-18.png)

親クラスに[Actor]を選択します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_cpp-redefinition_of_function/2022-09-10-18-29-04.png)

ClassTypeとClass名を設定します。

| Property   | Value        |
| ---------- | ------------ |
| Class Type | Public       |
| Name       | CPPParentRedefinition |

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_cpp-redefinition_of_function/2022-09-10-18-32-28.png)

```cpp:CPPParentRedefinition.h
// Fill out your copyright notice in the Description page of Project Settings.

#pragma once

#include "CoreMinimal.h"
#include "GameFramework/Actor.h"
#include "CPPParentRedefinition.generated.h"

UCLASS()
class CPP_BP_API ACPPParentRedefinition : public AActor
{
	GENERATED_BODY()
	
protected:
	// Called when the game starts or when spawned
	virtual void BeginPlay() override;

	int point;

public:
	// PointのSetterとGetter
	void SetPoint(int myPoint);
	int GetPoint();

};

```

```cpp:CPPParentRedefinition.cpp
// Fill out your copyright notice in the Description page of Project Settings.


#include "CPPParentRedefinition.h"

// Called when the game starts or when spawned
void ACPPParentRedefinition::BeginPlay()
{
	Super::BeginPlay();
	
}

void ACPPParentRedefinition::SetPoint(int myPoint)
{
	point = myPoint;
}

int ACPPParentRedefinition::GetPoint()
{
	return point;
}

```

### 派生クラス「CPPChildRedefinition」を作成する

派生クラス「CPPChildRedefinition」を作成します。

基底クラス「CPPParentRedefinition」右クリック > [Create C++ class derived from CPPParentRedefinition]を選択

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_cpp-redefinition_of_function/2022-09-10-18-58-06.png)

ClassTypeとClass名を設定します。

| Property   | Value        |
| ---------- | ------------ |
| Class Type | Public       |
| Name       | CPPChildRedefinition |

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_cpp-redefinition_of_function/2022-09-10-19-03-34.png)

```cpp:CPPChildRedefinition.h
// Fill out your copyright notice in the Description page of Project Settings.

#pragma once

#include "CoreMinimal.h"
#include "CPPParentRedefinition.h"
#include "CPPChildRedefinition.generated.h"

/**
 * 
 */
UCLASS()
class CPP_BP_API ACPPChildRedefinition : public ACPPParentRedefinition
{
	GENERATED_BODY()

public:
	void SetPoint(int myPoint);
	
};

```

```cpp:CPPChildRedefinition.cpp
// Fill out your copyright notice in the Description page of Project Settings.


#include "CPPChildRedefinition.h"

void ACPPChildRedefinition::SetPoint(int myPoint)
{
	// 基底クラスのSetPointをmyPointの値を変更して呼び出す
	ACPPParentRedefinition::SetPoint(myPoint - 30);
}

```

### 基底クラスと派生クラスを呼び出すテストクラスを作成する

基底クラス「CPPParentRedefinition」と派生クラス「CPPChildRedefinition」を生成して、メンバ関数の動作確認するためのテストクラス「CPPRedefinitionTest」を作成します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_cpp-redefinition_of_function/2022-09-17-22-19-28.png)

親クラスに[Actor]を選択します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_cpp-virtual_function_override/2022-09-19-16-30-51.png)

ClassTypeとClass名を設定します。

| Property   | Value        |
| ---------- | ------------ |
| Class Type | Public       |
| Name       | CPPRedefinitionTest |

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_cpp-redefinition_of_function/2022-09-17-22-22-42.png)


```cpp:CPPRedefinitionTest.h
// Fill out your copyright notice in the Description page of Project Settings.

#pragma once

#include "CoreMinimal.h"
#include "GameFramework/Actor.h"
#include "CPPRedefinitionTest.generated.h"

UCLASS()
class CPP_BP_API ACPPRedefinitionTest : public AActor
{
	GENERATED_BODY()
	
protected:
	// Called when the game starts or when spawned
	virtual void BeginPlay() override;

};

```

```cpp:CPPRedefinitionTest.cpp
// Fill out your copyright notice in the Description page of Project Settings.


#include "CPPRedefinitionTest.h"
#include "CPPParentRedefinition.h"
#include "CPPChildRedefinition.h"
#include "Kismet/KismetSystemLibrary.h"

// Called when the game starts or when spawned
void ACPPRedefinitionTest::BeginPlay()
{
	Super::BeginPlay();

	// 親クラスを生成する
	ACPPParentRedefinition* parentActor = GetWorld()->SpawnActor<ACPPParentRedefinition>(ACPPParentRedefinition::StaticClass());
	// SetPointを呼び出す
	parentActor->SetPoint(100);
	// GetPointの値を出力する
	UKismetSystemLibrary::PrintString(this, FString::Printf(TEXT("Parent Point : %d"), parentActor->GetPoint()), true, true, FColor::Cyan, 10.f);

	// 子クラスを生成する
	ACPPChildRedefinition* childActor = GetWorld()->SpawnActor<ACPPChildRedefinition>(ACPPChildRedefinition::StaticClass());
	// SetPointを呼び出す
	childActor->SetPoint(100);
	// GetPointの値を出力する
	UKismetSystemLibrary::PrintString(this, FString::Printf(TEXT("Child Point : %d"), childActor->GetPoint()), true, true, FColor::Red, 10.f);

}

```

ソースコードを保存して、Compileを実行します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_constructor_destructor/2022-07-24-15-49-43.png)

「CPPRedefinitionTest」をViewportにDrag&Dropします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_cpp-redefinition_of_function/2022-09-17-23-19-45.png)

Level Editorの[Play]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_constructor_destructor/2022-07-24-15-50-06.png)

メンバ変数を設定するSetPointを派生クラスで再定義することができました。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_cpp-redefinition_of_function/2022-09-17-23-40-51.png)

図にするとこのような仕組みになります。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_cpp-redefinition_of_function/2022-09-17-23-54-22.png)