---
title: "【C++】Event Dispatcher"
free: false
---

## 【C++】Event Dispatcher

### C++でBlueprintを再現すること

Event Dispatcherを作成します。
作成したEvent DispatcherにCustom EventをBindします。
「H」キーをPressした時に、Event Dispatherを呼び出し、Custom Eventを実行します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-event_dispatcher/2022-01-28-15-52-22.png)

### 編集するActorクラスを作成する

プロジェクトを閉じていたら、プロジェクトを開き、「Chapter_2_EventDispatcher」を開きます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-event_dispatcher/2022-01-28-17-42-00.png)

[Tools]メニューから[New C++ Class]を開きます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-event_dispatcher/2022-01-28-17-46-17.png)

親クラスに[Actor]を選択します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-input_event/2022-01-28-06-15-50.png)

ClassTypeとClass名を設定します。

| Property   | Value              |
| ---------- | ------------------ |
| Class Type | Public             |
| Name       | CPPEventDispatcher |

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-event_dispatcher/2022-01-28-17-51-00.png)

Solution Explorerから今回編集する2つのファイルを開きます。

- CPPEventDispatcher.h
- CPPEventDispatcher.cpp

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-event_dispatcher/2022-01-28-17-52-56.png)

開いたファイルを学習する初期状態に修正します。

```cpp:CPPEventDispatcher.h
// Fill out your copyright notice in the Description page of Project Settings.

#pragma once

#include "CoreMinimal.h"
#include "GameFramework/Actor.h"
#include "CPPCalcType.h"
#include "CPPEventDispatcher.generated.h"

UCLASS()
class CPP_BP_API ACPPEventDispatcher : public AActor
{
	GENERATED_BODY()

public:
	int32 Sum(int32 A, int32 B);

	// Action Mappingsに設定したActionを処理する関数
	void PressedActionPrintCalcResult();

protected:
	// Called when the game starts or when spawned
	virtual void BeginPlay() override;

private:
	FString Message = "C++ Hello World!";

	// 計算結果を出力する関数
	void PrintCalcResult(const ECPPCalcType Type, const int32 A, const int32 B, const float PrintDuration);

	// PrintString関数のDurationに設定する変数
	const float Duration = 10.0f;

	// PrintString関数のTextColorに設定する変数
	const FLinearColor TextColor = FColor(255, 255, 255);

	// 計算用の変数
	int32 CalcVarA = 7;
	int32 CalcVarB = 3;

	// Flow Control用の変数
	bool IsPrintHello = false;
	ECPPCalcType CalcType = ECPPCalcType::Add;

	// Input設定
	void SetupInput();

	// Input Eventを処理する関数
	void PressedH();

};
```

```cpp:CPPEventDispatcher.cpp
// Fill out your copyright notice in the Description page of Project Settings.


#include "CPPEventDispatcher.h"
#include "Kismet/KismetSystemLibrary.h"
#include "Kismet/GameplayStatics.h"

int32 ACPPEventDispatcher::Sum(int32 A, int32 B)
{
	return A + B;
}

// Called when the game starts or when spawned
void ACPPEventDispatcher::BeginPlay()
{
	Super::BeginPlay();

	SetupInput();

	if (IsPrintHello)
	{
		// PrintStringノードと同じ処理
		// UKismetSystemLibraryクラスのPrintString関数を呼び出す
		UKismetSystemLibrary::PrintString(this, Message, true, true, TextColor, Duration);
	}
	else
	{
		// 計算結果を出力する処理
		PrintCalcResult(CalcType, CalcVarA, CalcVarB, Duration);
	}
}

void ACPPEventDispatcher::PrintCalcResult(const ECPPCalcType Type, const int32 A, const int32 B, const float PrintDuration)
{
	switch (Type)
	{
		case ECPPCalcType::Add:
		{
			// Add(足し算)の処理
			// 値渡し
			int32 ResultAdd = Sum(A, B);
			FString StrResultAdd = FString::Printf(TEXT("%d"), ResultAdd);
			UKismetSystemLibrary::PrintString(this, StrResultAdd, true, true, FColor::Red, PrintDuration);
			break;
		}
		case ECPPCalcType::Subtract:
		{
			// Subtract(引き算)の処理
			int32 ResultSubtract = A - B;
			FString StrResultSubtract = FString::Printf(TEXT("%d"), ResultSubtract);
			UKismetSystemLibrary::PrintString(this, StrResultSubtract, true, true, FColor::Yellow, PrintDuration);
			break;
		}
		case ECPPCalcType::Multiply:
		{
			// Multiply(掛け算)の処理
			int32 ResultMultiply = A * B;
			FString StrResultMultiply = FString::Printf(TEXT("%d"), ResultMultiply);
			UKismetSystemLibrary::PrintString(this, StrResultMultiply, true, true, FColor::Green, PrintDuration);
			break;
		}
		case ECPPCalcType::Divide:
		{
			// Divide(割り算)の処理(int > float)
			float ResultDivide = (float)A / (float)B;
			FString StrResultDivide = FString::Printf(TEXT("%f"), ResultDivide);
			UKismetSystemLibrary::PrintString(this, StrResultDivide, true, true, FColor::Blue, PrintDuration);
			break;
		}
	}
}

void ACPPEventDispatcher::SetupInput()
{
	// 入力を有効にする
	EnableInput(UGameplayStatics::GetPlayerController(GetWorld(), 0));

	// HキーのPressedとReleasedをバインドする
	InputComponent->BindKey(EKeys::H, IE_Pressed, this, &ACPPEventDispatcher::PressedH);

	// ActionMappingsに設定したActionをバインドする
	InputComponent->BindAction("ActionPrintCalcResult", IE_Pressed, this, &ACPPEventDispatcher::PressedActionPrintCalcResult);
}

void ACPPEventDispatcher::PressedH()
{
	// Hello World!を出力する処理
	UKismetSystemLibrary::PrintString(this, Message, true, true, TextColor, Duration);
}

void ACPPEventDispatcher::PressedActionPrintCalcResult()
{
	// 計算結果を出力する処理
	PrintCalcResult(CalcType, CalcVarA, CalcVarB, Duration);
}
```
### Event Dispatcher[OnPrintHello]を追加する

Blueprintで[My Blueprint]パネルの[Event Dispatchers]カテゴリーにEvent Dispatcher[OnPrintHello]を追加しました。
C++でEvent Dispatcherを再現します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-event_dispatcher/2022-01-28-23-36-41.png)

C++では以下のようなソースコードになります。

```cpp:ACPPEventDispatcher.h
public:
	// Event Dispatcher[OnPrintHello]
	DECLARE_DYNAMIC_MULTICAST_DELEGATE(FPrintHelloDelegate);

	UPROPERTY(BlueprintAssignable, Category = "CPP_BP")
	FPrintHelloDelegate OnPrintHello;
```

### Event Dispatcher[OnPrintHello]をCustom Event[PrintHello]にバインドする

Event Dispatcher[OnPrintHello]をCustom Event[PrintHello]にバインドする処理をC++で再現します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-event_dispatcher/2022-01-28-23-59-30.png)

「ACPPEventDispatcher.h」にコンストラクタとカスタムイベントにあたる関数[PrintHello]のプロトタイプを宣言します。

```cpp:ACPPEventDispatcher.h
public:
	ACPPEventDispatcher();

	// Custom Event[PrintHello] 
	UFUNCTION()
	void PrintHello();
```

コンストラクタにEvent Dispatcher[OnPrintHello]をCustom Event[PrintHello]にバインドする処理を書きます。
Custom Event[PrintHello]に”Hello World!”を出力するPrintStringを書きます。

```cpp:ACPPEventDispatcher.cpp
ACPPEventDispatcher::ACPPEventDispatcher()
{
	// Event Dispathcer[OnPrintHello]にCustom Event[PrintHello]をバインドする
	OnPrintHello.AddDynamic(this, &ACPPEventDispatcher::PrintHello);
}

void ACPPEventDispatcher::PrintHello()
{
	// Hello World!を出力する処理
	UKismetSystemLibrary::PrintString(this, Message, true, true, TextColor, Duration);
}
```

### 「H」キーのPressedからEventDispatcher「OnPrintHello」を呼び出す

「H」キーのPressedからEvent Dispatcher[OnPrintHello]のCallノードを呼び出す処理をC++で再現します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-event_dispatcher/2022-01-29-00-44-55.png)

Broadcast()がCallノードにあたります。

```cpp:ACPPEventDispatcher.cpp
void ACPPEventDispatcher::PressedH()
{
	// Event Dispathcer[OnPrintHello]をコールする
	OnPrintHello.Broadcast();
}
```

Ctrl + Sでファイルを保存し、Compileを行います。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-event_dispatcher/2022-01-29-00-56-55.png)

「ACPPEventDispatcher」をViewportにDrag&Dropします。
PrintStringの出力結果が分かりづらくなるので、「BP_EventDispatcher」を削除します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-event_dispatcher/2022-01-29-00-53-05.png)

Level Editorの[Play]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-event_dispatcher/2022-01-29-00-54-14.png)

「H」キーをPressすると、「OnPrintHello.Broadcast()」が呼ばれ、バインドしていたCustom Event[PrintHello]が呼ばれます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-event_dispatcher/2022-01-29-00-56-16.png)

BlueprintとC++との処理を対応させた図です。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-event_dispatcher/2022-01-29-01-11-57.png)

### すべて保存

C++側の説明は以上になります。
プロジェクトをすべて保存しましょう。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-event_dispatcher/2022-01-29-01-17-54.png)

Visual StudioのSolutionもすべて保存しましょう。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-flow_control_switch/2022-01-23-21-46-14.png)

## 参照URL

https://docs.unrealengine.com/4.27/ja/ProgrammingAndScripting/ProgrammingWithCPP/UnrealArchitecture/Delegates/

https://forums.unrealengine.com/t/c-event-dispatchers-how-do-we-implement-them/23185
