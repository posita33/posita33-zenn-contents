---
title: "【C++】インターフェース"
free: false
---

## インタフェース

### インタフェースについて

Interface クラスは関連性のない一連のクラスが共通の関数を確実に実装するために役立ちます。
UnrealEngineはAActorから派生したりするので、共通の機能を持つ必要が発生した時にインタフェースを使用することが勧められています。

### インタフェースを作成する

インタフェースを作成します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_cpp-Interface/2022-09-24-09-48-48.png)

親クラスに[UnrealInterface]を選択します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_cpp-Interface/2022-09-24-10-20-26.png)

ClassTypeとClass名を設定します。

| Property   | Value        |
| ---------- | ------------ |
| Class Type | Public       |
| Name       | CPPInterface |

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_cpp-Interface/2022-09-24-10-21-42.png)

```cpp:CPPInterface.h
// Fill out your copyright notice in the Description page of Project Settings.

#pragma once

#include "CoreMinimal.h"
#include "UObject/Interface.h"
#include "CPPInterface.generated.h"

// This class does not need to be modified.
UINTERFACE(MinimalAPI)
class UCPPInterface : public UInterface
{
	GENERATED_BODY()
};

/**
 * 
 */
class CPP_BP_API ICPPInterface
{
	GENERATED_BODY()

	// Add interface functions to this class. This is the class that will be inherited to implement this interface.
public:
	
	// 引数と戻り値がないメンバ関数
	virtual void PrintHello();

	// 引数と戻り値があるメンバ関数
	virtual int Add(int A, int B);
};

```

```cpp:CPPInterface.cpp
// Fill out your copyright notice in the Description page of Project Settings.


#include "CPPInterface.h"
#include "Kismet/KismetSystemLibrary.h"

// Add default functionality here for any ICPPInterface functions that are not pure virtual.

void ICPPInterface::PrintHello()
{
	UKismetSystemLibrary::PrintString(NULL, FString::Printf(TEXT("Hello")), true, true, FColor::Cyan, 10.f);
}

int ICPPInterface::Add(int A, int B)
{
	return A+B;
}

```

### インタフェースを実装するクラスを作成する

インターフェースを実装するクラスを作成します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_cpp-Interface/2022-09-24-10-31-00.png)

親クラスに[Actor]を選択します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_cpp-redefinition_of_function/2022-09-10-18-29-04.png)

ClassTypeとClass名を設定します。

| Property   | Value            |
| ---------- | ---------------- |
| Class Type | Public           |
| Name       | CPPInterfaceTest |

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_cpp-Interface/2022-09-24-10-31-38.png)

ソースコードを保存して、Compileを実行します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_constructor_destructor/2022-07-24-15-49-43.png)

Level Editorの[Play]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_constructor_destructor/2022-07-24-15-50-06.png)

```cpp:CPPInterfaceTest.h
// Fill out your copyright notice in the Description page of Project Settings.

#pragma once

#include "CoreMinimal.h"
#include "GameFramework/Actor.h"
#include "CPPInterface.h"
#include "CPPInterfaceTest.generated.h"

UCLASS()
class CPP_BP_API ACPPInterfaceTest : public AActor, public ICPPInterface
{
	GENERATED_BODY()
	
protected:
	// Called when the game starts or when spawned
	virtual void BeginPlay() override;

};

```

```cpp:CPPInterfaceTest.cpp
// Fill out your copyright notice in the Description page of Project Settings.


#include "CPPInterfaceTest.h"
#include "Kismet/KismetSystemLibrary.h"

// Called when the game starts or when spawned
void ACPPInterfaceTest::BeginPlay()
{
	Super::BeginPlay();

	PrintHello();
	
	UKismetSystemLibrary::PrintString(this, FString::Printf(TEXT("Add(1+2)= %d"), Add(1,2)), true, true, FColor::Cyan, 10.f);

}

```

ソースコードを保存して、Compileを実行します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_constructor_destructor/2022-07-24-15-49-43.png)

「CPPInterfaceTest」をViewportにDrag&Dropします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_cpp-Interface/2022-09-24-21-51-27.png)

Level Editorの[Play]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_constructor_destructor/2022-07-24-15-50-06.png)

インターフェースで実装したメンバ関数を呼び出せました。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_cpp-Interface/2022-09-24-21-55-10.png)

### メンバ関数をオーバーライドする

インターフェースのメンバ関数をオーバライドして処理を変更します。

```cpp:CPPInterfaceTest.h
// Fill out your copyright notice in the Description page of Project Settings.

#pragma once

#include "CoreMinimal.h"
#include "GameFramework/Actor.h"
#include "CPPInterface.h"
#include "CPPInterfaceTest.generated.h"

UCLASS()
class CPP_BP_API ACPPInterfaceTest : public AActor, public ICPPInterface
{
	GENERATED_BODY()
	
protected:
	// Called when the game starts or when spawned
	virtual void BeginPlay() override;

public:
	// 引数と戻り値がないメンバ関数
	virtual void PrintHello() override;

	// 引数と戻り値があるメンバ関数
	virtual int Add(int A, int B) override;

};

```

```cpp:CPPInterfaceTest.cpp
// Fill out your copyright notice in the Description page of Project Settings.


#include "CPPInterfaceTest.h"
#include "Kismet/KismetSystemLibrary.h"

// Called when the game starts or when spawned
void ACPPInterfaceTest::BeginPlay()
{
	Super::BeginPlay();

	PrintHello();
	
	UKismetSystemLibrary::PrintString(this, FString::Printf(TEXT("Add(1+2+1+2)= %d"), Add(1,2)), true, true, FColor::Cyan, 10.f);

}

void ACPPInterfaceTest::PrintHello()
{
	UKismetSystemLibrary::PrintString(this, FString::Printf(TEXT("Hello World!")), true, true, FColor::Cyan, 10.f);
}

int ACPPInterfaceTest::Add(int A, int B)
{
	return A + B + A + B;
}

```

ソースコードを保存して、Compileを実行します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_constructor_destructor/2022-07-24-15-49-43.png)

Level Editorの[Play]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_constructor_destructor/2022-07-24-15-50-06.png)

インターフェースを実装したクラス側でメンバ関数の処理を変更できました。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_cpp-Interface/2022-09-24-22-04-16.png)

### 参照URL

https://docs.unrealengine.com/4.27/ja/ProgrammingAndScripting/GameplayArchitecture/Interfaces/