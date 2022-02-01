---
title: "【C++】Flow Control（Loop）"
free: false
---

## 【C++】Function（関数）

### C++でBlueprintを再現すること

Blueprintの3種類のLoopノードをC++で再現する

- For Loop
- For Each Loop
- While Loop

[For Loop]と[For Earch Loop]にはBreak付きのノードが用意されています。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-flow_control_loop/2022-01-31-15-40-34.png)

3つのLoopで同じ結果になる処理を紹介します。

- For Loop
- For Each Loop
- While Loop

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-flow_control_loop/2022-01-31-15-40-54.png)

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-flow_control_loop/2022-01-31-15-41-03.png)

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-flow_control_loop/2022-01-31-15-41-14.png)

### 編集するActorクラスを作成する

プロジェクトを閉じていたら、プロジェクトを開き、「Chapter_2_FlowControl_Loop」を開きます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-flow_control_loop/2022-02-01-05-40-05.png)

[Tools]メニューから[New C++ Class]を開きます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-flow_control_loop/2022-02-01-05-41-06.png)

親クラスに[Actor]を選択します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-input_event/2022-01-28-06-15-50.png)

ClassTypeとClass名を設定します。

| Property   | Value              |
| ---------- | ------------------ |
| Class Type | Public             |
| Name       | CPPFlowControlLoop |

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-flow_control_loop/2022-02-01-05-43-31.png)

Solution Explorerから今回編集する2つのファイルを開きます。

- CPPFlowControlLoop.h
- CPPFlowControlLoop.cpp

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-flow_control_loop/2022-02-01-05-56-39.png)

開いたファイルを学習する初期状態に修正します。

```cpp:CPPFlowControlLoop.h
// Fill out your copyright notice in the Description page of Project Settings.

#pragma once

#include "CoreMinimal.h"
#include "GameFramework/Actor.h"
#include "CPPCalcType.h"
#include "CPPFlowControlLoop.generated.h"

UCLASS()
class CPP_BP_API ACPPFlowControlLoop : public AActor
{
	GENERATED_BODY()

public:
	ACPPFlowControlLoop();

	// Event Dispatcher[OnPrintHello]
	DECLARE_DYNAMIC_MULTICAST_DELEGATE(FPrintHelloDelegate);

	UPROPERTY(BlueprintAssignable, Category = "CPP_BP")
	FPrintHelloDelegate OnPrintHello;

	// Custom Event[PrintHello] 
	UFUNCTION()
	void PrintHello();

	int32 Sum(int32 A, int32 B);

	// Action Mappingsに設定したActionを処理する関数
	void PressedActionPrintCalcResult();

protected:
	// Called when the game starts or when spawned
	virtual void BeginPlay() override;

private:
	TArray<FString> Messages = { TEXT("C++ Hello World!"), TEXT("你好 世界!"), TEXT("Bonjour le monde!"), TEXT("Hallo Welt!"), TEXT("こんにちは世界!") };
	//TArray<FString> Messages = { "C++ Hello World!", "你好 世界!", "Bonjour le monde!", "Hallo Welt!", "こんにちは世界!" };

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
	int32 TypeIndex = 0;
	TArray<ECPPCalcType> CalcTypes = { ECPPCalcType::Add, ECPPCalcType::Subtract, ECPPCalcType::Multiply, ECPPCalcType::Divide };

	// Input設定
	void SetupInput();

	// Input Eventを処理する関数
	void PressedH();

};
```

```cpp:CPPFlowControlLoop.cpp
// Fill out your copyright notice in the Description page of Project Settings.


#include "CPPFlowControlLoop.h"
#include "Kismet/KismetSystemLibrary.h"
#include "Kismet/GameplayStatics.h"

ACPPFlowControlLoop::ACPPFlowControlLoop()
{
	// Event Dispathcer[OnPrintHello]にCustom Event[PrintHello]をバインドする
	OnPrintHello.AddDynamic(this, &ACPPFlowControlLoop::PrintHello);
}

int32 ACPPFlowControlLoop::Sum(int32 A, int32 B)
{
	return A + B;
}

// Called when the game starts or when spawned
void ACPPFlowControlLoop::BeginPlay()
{
	Super::BeginPlay();

	SetupInput();

	if (IsPrintHello)
	{
		// Hello World!を出力する処理
		PrintHello();
	}
	else
	{
		// 計算結果を出力する処理
		PressedActionPrintCalcResult();
	}
}

void ACPPFlowControlLoop::PrintCalcResult(const ECPPCalcType Type, const int32 A, const int32 B, const float PrintDuration)
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
		}
	}
}

void ACPPFlowControlLoop::SetupInput()
{
	// 入力を有効にする
	EnableInput(UGameplayStatics::GetPlayerController(GetWorld(), 0));

	// HキーのPressedとReleasedをバインドする
	InputComponent->BindKey(EKeys::H, IE_Pressed, this, &ACPPFlowControlLoop::PressedH);

	// ActionMappingsに設定したActionをバインドする
	InputComponent->BindAction("ActionPrintCalcResult", IE_Pressed, this, &ACPPFlowControlLoop::PressedActionPrintCalcResult);
}

void ACPPFlowControlLoop::PressedH()
{
	// Event Dispathcer[OnPrintHello]をコールする
	OnPrintHello.Broadcast();
}

void ACPPFlowControlLoop::PressedActionPrintCalcResult()
{
	// 計算結果を出力する処理
	PrintCalcResult(CalcTypes[TypeIndex], CalcVarA, CalcVarB, Duration);

	TypeIndex++;
	TypeIndex = TypeIndex % CalcTypes.Num();
}

void ACPPFlowControlLoop::PrintHello()
{
	int32 randomIndex = FMath::RandRange(0, Messages.Num() - 1);

	// 1行で書くなら 
	// Messages[FMath::RandRange(0, Messages.Num() - 1)]

	// Hello World!を出力する処理
	UKismetSystemLibrary::PrintString(this, Messages[randomIndex], true, true, TextColor, Duration);
}
```

### For LoopノードでPrintStringを繰り返し呼び出す

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-flow_control_loop/2022-02-01-05-46-26.png)


```cpp
for (int i = 0; i <= 4; i++)
{
    // 繰り返し処理
}
// 完了後の処理
```

```cpp
int32 FirstIndex = 0;
int32 LastIndex = 4;

// for loop
for (int32 index = FirstIndex; index <= LastIndex; index++)
{
    // Loop Body
}
// Completed
```

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-flow_control_loop/2022-02-01-06-55-02.png)


```cpp:ACPPFlowControlLoop.cpp PrintHello()
void ACPPFlowControlLoop::PrintHello()
{
	int32 FirstIndex = 0;
	int32 LastIndex = 4;

	// for loop
	for (int32 index = FirstIndex; index <= LastIndex; index++)
	{
		// indexの値を出力する
		UKismetSystemLibrary::PrintString(this, FString::Printf(TEXT("%d"), index), true, true, TextColor, Duration);
	}
	// CompletedをPrintStringで出力する
	UKismetSystemLibrary::PrintString(this, TEXT("Completed"), true, true, FColor::Cyan, Duration);
}
```

Ctrl + Sでファイルを保存し、Compileを行います。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-flow_control_loop/2022-02-01-06-08-33.png)

「ACPPFlowControlLoop」をViewportにDrag&Dropします。
PrintStringの出力結果が分かりづらくなるので、「BP_FlowControl_Loop」を削除します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-flow_control_loop/2022-02-01-06-11-32.png)

Level Editorの[Play]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-flow_control_loop/2022-02-01-06-12-50.png)


![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-flow_control_loop/2022-02-01-06-43-14.png)

### For Loopノードで配列をすべて出力する

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-flow_control_loop/2022-02-01-05-49-07.png)




```cpp:ACPPFlowControlLoop.cpp PrintHello()
void ACPPFlowControlLoop::PrintHello()
{
	int32 FirstIndex = 0;
	int32 LastIndex = Messages.Num() - 1;

	// for loop
	for (int32 index = FirstIndex; index <= LastIndex; index++)
	{
		// Messagesの値を出力する
		UKismetSystemLibrary::PrintString(this, Messages[index], true, true, TextColor, Duration);
	}
	// CompletedをPrintStringで出力する
	UKismetSystemLibrary::PrintString(this, TEXT("Completed"), true, true, FColor::Cyan, Duration);
}
```

Ctrl + Sでファイルを保存し、Compileを行います。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-flow_control_loop/2022-02-01-06-08-33.png)

Level Editorの[Play]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-flow_control_loop/2022-02-01-06-12-50.png)


![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-flow_control_loop/2022-02-01-07-06-48.png)

### For Loop with BreakノードでLoopを途中で抜ける

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-flow_control_loop/2022-02-01-05-51-31.png)


```cpp
for (int i = 0; i <= 4; i++)
{
	// 繰り返し処理
	if(条件)
	{
		//条件がTrue
		break;
	}
}
// 完了後の処理
```

```cpp
int32 FirstIndex = 0;
int32 LastIndex = 4;

// for loop
for (int32 index = FirstIndex; index <= LastIndex; index++)
{
	// Loop Body
	if(Messages[index].Contains(TEXT("文字列")))
	{
		// 文字列が含まれる場合
		break;
	}
}
// Completed
```

```cpp:CPPFlowControlLoop.cpp PrintHello()
void ACPPFlowControlLoop::PrintHello()
{
	int32 FirstIndex = 0;
	int32 LastIndex = Messages.Num() - 1;

	// for loop
	for (int32 index = FirstIndex; index <= LastIndex; index++)
	{
		// 文字列に"Bonjour"が含まれているか
		if (Messages[index].Contains(TEXT("Bonjour")))
		{
			// TrueならLoopを抜ける
			break;
		}

		// Messagesの値を出力する
		UKismetSystemLibrary::PrintString(this, Messages[index], true, true, TextColor, Duration);
	}
	// CompletedをPrintStringで出力する
	UKismetSystemLibrary::PrintString(this, TEXT("Completed"), true, true, FColor::Cyan, Duration);
}
```

Ctrl + Sでファイルを保存し、Compileを行います。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-flow_control_loop/2022-02-01-06-08-33.png)

Level Editorの[Play]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-flow_control_loop/2022-02-01-06-12-50.png)


![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-flow_control_loop/2022-02-02-05-58-37.png)

### continue文（C++のみ）

```cpp
for (int i = 0; i <= 4; i++)
{
	// 繰り返し処理
	if(条件)
	{
		//条件がTrue
		continue;
	}
}
// 完了後の処理
```

```cpp:CPPFlowControlLoop.cpp PrintHello()
void ACPPFlowControlLoop::PrintHello()
{
	int32 FirstIndex = 0;
	int32 LastIndex = Messages.Num() - 1;

	// for loop
	for (int32 index = FirstIndex; index <= LastIndex; index++)
	{
		// 文字列に"Bonjour"が含まれているか
		if (Messages[index].Contains(TEXT("Bonjour")))
		{
			// TrueならLoopを続ける
			continue;
		}

		// Messagesの値を出力する
		UKismetSystemLibrary::PrintString(this, Messages[index], true, true, TextColor, Duration);
	}
	// CompletedをPrintStringで出力する
	UKismetSystemLibrary::PrintString(this, TEXT("Completed"), true, true, FColor::Cyan, Duration);
}
```

Ctrl + Sでファイルを保存し、Compileを行います。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-flow_control_loop/2022-02-01-06-08-33.png)

Level Editorの[Play]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-flow_control_loop/2022-02-01-06-12-50.png)


![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-flow_control_loop/2022-02-02-05-55-59.png)


### Foreach Loop with Breakノードで配列をすべて出力する

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-flow_control_loop/2022-02-01-05-53-20.png)


```cpp
TArray<FString> Strs;

for (FString Str : Strs)
{
	// Index[0]～Index[LastIndex]までLoopする
}
// 完了後の処理
```

```cpp:CPPFlowControlLoop.cpp PrintHello()
void ACPPFlowControlLoop::PrintHello()
{
	// C++版のFor Each Loop with Break
	for (FString Message : Messages)
	{
		// 文字列に"Bonjour"が含まれているか
		if (Message.Contains(TEXT("Bonjour")))
		{
			// TrueならLoopを続ける
			break;
		}
		// Messagesの値を出力する
		UKismetSystemLibrary::PrintString(this, Message, true, true, TextColor, Duration);
	}
	// CompletedをPrintStringで出力する
	UKismetSystemLibrary::PrintString(this, TEXT("Completed"), true, true, FColor::Cyan, Duration);
}
```

Ctrl + Sでファイルを保存し、Compileを行います。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-flow_control_loop/2022-02-01-06-08-33.png)

Level Editorの[Play]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-flow_control_loop/2022-02-01-06-12-50.png)

### While loopノード

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-flow_control_loop/2022-02-01-05-53-46.png)


While Loopは無限ループになりやすいので、ループを抜ける処理を必ず用意します。

```cpp
while (whileの条件)
{
	// 繰り返し処理
	if(条件)
	{
		//条件がTrue
		whileの条件 = false;
	}
	else
	{
		処理
	}
}
// 完了後の処理
```

```cpp:PPFlowControlLoop.cpp PrintHello()
void ACPPFlowControlLoop::PrintHello()
{
	bool NotBonjour = true;
	int32 HelloIndex = 0;

	while (NotBonjour)
	{
		// 文字列に"Bonjour"が含まれているか
		if (Messages[HelloIndex].Contains(TEXT("Bonjour")))
		{
			// While Loopの条件をfalseに設定する
			NotBonjour = false;
		}
		else
		{
			// Messagesの値を出力する
			UKismetSystemLibrary::PrintString(this, Messages[HelloIndex], true, true, TextColor, Duration);
		}
		// HelloIndexをインクリメント
		HelloIndex++;
	}

	// CompletedをPrintStringで出力する
	UKismetSystemLibrary::PrintString(this, TEXT("Completed"), true, true, FColor::Cyan, Duration);
}
```

Ctrl + Sでファイルを保存し、Compileを行います。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-flow_control_loop/2022-02-01-06-08-33.png)

Level Editorの[Play]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-flow_control_loop/2022-02-01-06-12-50.png)


![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-flow_control_loop/2022-02-02-06-34-19.png)

### すべて保存

C++側の説明は以上になります。
プロジェクトをすべて保存しましょう。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-event_dispatcher/2022-01-29-01-17-54.png)

Visual StudioのSolutionもすべて保存しましょう。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-flow_control_switch/2022-01-23-21-46-14.png)

## 参照URL

https://docs.unrealengine.com/4.26/ja/ProgrammingAndScripting/ProgrammingWithCPP/UnrealArchitecture/TArrays/

https://www.unrealengine.com/ja/blog/ranged-based-for-loops
