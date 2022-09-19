---
title: "【CPP】仮想関数とオーバーライド"
free: false
---

## 仮想関数とオーバーライド

### 基底クラスのメンバ関数を再定義する

基底クラスのメンバ関数は、派生クラスで定義し直せました。
派生クラスを基底クラスで生成した時に、通常であれば再定義前のメンバ関数が呼ばれます。
仮想関数は再定義した後のメンバ関数を呼べるようにします。
メンバ変数を設定するSetPointを仮想関数で再定義して動作確認します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_cpp-virtual_function_override/2022-09-19-17-02-28.png)

### 基底クラス「CPPParentVirtual」を作成する

基底クラス「CPPParentVirtual」を作成します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_cpp-redefinition_of_function/2022-09-10-18-27-18.png)

親クラスに[Actor]を選択します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_cpp-redefinition_of_function/2022-09-10-18-29-04.png)

ClassTypeとClass名を設定します。

| Property   | Value            |
| ---------- | ---------------- |
| Class Type | Public           |
| Name       | CPPParentVirtual |

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_cpp-virtual_function_override/2022-09-18-15-02-17.png)

```cpp:CPPParentVirtual.h
// Fill out your copyright notice in the Description page of Project Settings.

#pragma once

#include "CoreMinimal.h"
#include "GameFramework/Actor.h"
#include "CPPParentVirtual.generated.h"

UCLASS()
class CPP_BP_API ACPPParentVirtual : public AActor
{
	GENERATED_BODY()

protected:
	// Called when the game starts or when spawned
	virtual void BeginPlay() override;

	int point;

public:
	// PointのSetterとGetter
	virtual void SetPoint(int myPoint);
	int GetPoint();

};

```

```cpp:CPPParentVirtual.cpp
// Fill out your copyright notice in the Description page of Project Settings.


#include "CPPParentVirtual.h"

// Called when the game starts or when spawned
void ACPPParentVirtual::BeginPlay()
{
	Super::BeginPlay();
	
}

void ACPPParentVirtual::SetPoint(int myPoint)
{
	point = myPoint;
}

int ACPPParentVirtual::GetPoint()
{
	return point;
}
```

### 派生クラス「CPPChildVirtual」を作成する

派生クラス「CPPChildVirtual」を作成します。

基底クラス「CPPParentVirtual」右クリック > [Create C++ class derived from CPPParentVirtual]を選択

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_cpp-virtual_function_override/2022-09-18-15-17-42.png)

ClassTypeとClass名を設定します。

| Property   | Value           |
| ---------- | --------------- |
| Class Type | Public          |
| Name       | CPPChildVirtual |

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_cpp-virtual_function_override/2022-09-18-15-20-13.png)

```cpp:CPPChildVirtual.h
// Fill out your copyright notice in the Description page of Project Settings.

#pragma once

#include "CoreMinimal.h"
#include "CPPParentVirtual.h"
#include "CPPChildVirtual.generated.h"

/**
 * 
 */
UCLASS()
class CPP_BP_API ACPPChildVirtual : public ACPPParentVirtual
{
	GENERATED_BODY()

public:
	void SetPoint(int myPoint);

};

```

```cpp:CPPChildVirtual.cpp
// Fill out your copyright notice in the Description page of Project Settings.


#include "CPPChildVirtual.h"

void ACPPChildVirtual::SetPoint(int myPoint)
{
	// 基底クラスのSetPointをmyPointの値を変更して呼び出す
	ACPPParentVirtual::SetPoint(myPoint - 30);
}

```

### VirtualをつけたSetPoint動作を確認するテストクラスを作成する

派生クラス「CPPChildRedefinition」と派生クラス「CPPChildVirtual」をそれぞれ基底クラスで生成して、メンバ関数SetPointの動作確認するためのテストクラス「CPPVirtualTest」を作成します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_cpp-redefinition_of_function/2022-09-17-22-19-28.png)

親クラスに[Actor]を選択します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_cpp-virtual_function_override/2022-09-19-16-30-51.png)


ClassTypeとClass名を設定します。

| Property   | Value          |
| ---------- | -------------- |
| Class Type | Public         |
| Name       | CPPVirtualTest |

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_cpp-virtual_function_override/2022-09-19-16-33-56.png)

```cpp:CPPVirtualTest.h
// Fill out your copyright notice in the Description page of Project Settings.

#pragma once

#include "CoreMinimal.h"
#include "GameFramework/Actor.h"
#include "CPPVirtualTest.generated.h"

UCLASS()
class CPP_BP_API ACPPVirtualTest : public AActor
{
	GENERATED_BODY()
	
protected:
	// Called when the game starts or when spawned
	virtual void BeginPlay() override;

};

```

```cpp:CPPVirtualTest.cpp
// Fill out your copyright notice in the Description page of Project Settings.


#include "CPPVirtualTest.h"
#include "CPPParentVirtual.h"
#include "CPPChildVirtual.h"
#include "CPPParentRedefinition.h"
#include "CPPChildRedefinition.h"
#include "Kismet/KismetSystemLibrary.h"

// Called when the game starts or when spawned
void ACPPVirtualTest::BeginPlay()
{
	Super::BeginPlay();
	
	// CPPChildRedefinitionを生成する
	ACPPParentRedefinition* redefinitionActor = GetWorld()->SpawnActor<ACPPChildRedefinition>(ACPPChildRedefinition::StaticClass());
	// SetPointを呼び出す
	redefinitionActor->SetPoint(100);
	// GetPointの値を出力する
	UKismetSystemLibrary::PrintString(this, FString::Printf(TEXT("Redefinition Point : %d"), redefinitionActor->GetPoint()), true, true, FColor::Cyan, 10.f);

	// CPPChildVirtualを生成する
	ACPPParentVirtual* virautalActor = GetWorld()->SpawnActor<ACPPChildVirtual>(ACPPChildVirtual::StaticClass());
	// SetPointを呼び出す
	virautalActor->SetPoint(100);
	// GetPointの値を出力する
	UKismetSystemLibrary::PrintString(this, FString::Printf(TEXT("Virtual Point : %d"), virautalActor->GetPoint()), true, true, FColor::Red, 10.f);

}

```

ソースコードを保存して、Compileを実行します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_constructor_destructor/2022-07-24-15-49-43.png)

「CPPVirtualTest」をViewportにDrag&Dropします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_cpp-virtual_function_override/2022-09-19-16-47-37.png)

Level Editorの[Play]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_constructor_destructor/2022-07-24-15-50-06.png)

メンバ変数を設定するSetPointを派生クラスで再定義することができました。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_cpp-virtual_function_override/2022-09-19-16-52-07.png)

図にするとこのような仕組みになります。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_cpp-virtual_function_override/2022-09-19-17-02-28.png)

### 仮想関数にfinalを付ける

仮想関数に「final」を付けるとオーバーライドできなくなります。
CPPParentVirtual.hの仮想関数にfinalを付けてコンパイルします。

```cpp:CPPParentVirtual.h
public:
	virtual void SetPoint(int myPoint) final;
```

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_cpp-virtual_function_override/2022-09-19-17-13-23.png)

派生クラス「CPPChildVirtual」でSetPointが再定義できなくてエラーになります。

```
\CPP_BP\Source\CPP_BP\Public\CPPChildVirtual.h(18): error C3248: 'ACPPParentVirtual::SetPoint': function declared as 'final' cannot be overridden by 'ACPPChildVirtual::SetPoint'
\CPP_BP\Source\CPP_BP\Public\CPPParentVirtual.h(22): note: see declaration of 'ACPPParentVirtual::SetPoint'
```

### 派生クラスでoverrideを付けて仮想関数かチェックする

派生クラスでメンバ関数の最後に「override」をつけると仮想関数かどうかをチェックできます。

基底クラスで「Virtual」を付けていて、派生クラスで「override」を付けてコンパイルします。

```cpp:CPPParentVirtual.h
public:
	virtual void SetPoint(int myPoint);
```

```cpp:CPPParentVirtual.h
public:
	void SetPoint(int myPoint) override;
```

コンパイルに成功します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_constructor_destructor/2022-07-24-15-49-43.png)

基底クラスから「Virtual」を外して、派生クラスで「override」を付けてコンパイルします。

```cpp:CPPParentVirtual.h
public:
	void SetPoint(int myPoint);
```

```cpp:CPPParentVirtual.h
public:
	void SetPoint(int myPoint) override;
```

コンパイルに失敗します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_03_cpp-virtual_function_override/2022-09-19-17-13-23.png)

```cpp
\CPP_BP\Source\CPP_BP\Public\CPPChildVirtual.h(18): error C3668: 'ACPPChildVirtual::SetPoint': method with override specifier 'override' did not override any base class methods
```