---
title: "【C++】Flow Control(Switch)"
free: false
---

## 【C++】Function（関数）

### C++でBlueprintを再現すること

BlueprintのSwitchノードをC++で再現します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-flow_control_switch/2022-02-12-21-57-22.png)

### 編集するActorクラスを作成する

プロジェクトを閉じていたら、プロジェクトを開き、
「Chapter_2_FlowControl_Switch」を開きます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-flow_control_switch/2022-03-05-16-01-42.png)

[Tools]メニューから[New C++ Class]を開きます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-flow_control_switch/2022-03-05-16-02-36.png)

親クラスに[Actor]を選択します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-flow_control_switch/2022-03-05-16-04-32.png)

ClassTypeとClass名を設定します。

| Property   | Value                |
| ---------- | -------------------- |
| Class Type | Public               |
| Name       | CPPFlowControlSwitch |

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-flow_control_switch/2022-01-23-18-44-39.png)

Solution Explorerから今回編集する2つのファイルを開きます。

- CPPFlowControlSwitch.h
- CPPFlowControlSwitch.cpp

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-flow_control_switch/2022-02-12-22-00-03.png)

開いたファイルを学習する初期状態に修正します。

```cpp:CPPFlowControlSwitch.h
// Fill out your copyright notice in the Description page of Project Settings.

#pragma once

#include "CoreMinimal.h"
#include "GameFramework/Actor.h"
#include "CPPFlowControlSwitch.generated.h"

UCLASS()
class CPP_BP_API ACPPFlowControlSwitch : public AActor
{
	GENERATED_BODY()

protected:
	// Called when the game starts or when spawned
	virtual void BeginPlay() override;

private:
	// PrintString関数のDurationに設定する変数
	const float Duration = 10.0f;

	// PrintString関数のTextColorに設定する変数
	const FLinearColor TextColor = FColor(255, 255, 255);

	// 計算用の変数
	int32 CalcVarA = 7;
	int32 CalcVarB = 3;

	// Flow Control用の変数
	bool IsPrintHello = false;
	int32 CalcType = 1;
};

```

```cpp:CPPFlowControlSwitch.cpp
// Fill out your copyright notice in the Description page of Project Settings.


#include "CPPFlowControlSwitch.h"
#include "Kismet/KismetSystemLibrary.h"

// Called when the game starts or when spawned
void ACPPFlowControlSwitch::BeginPlay()
{
	FString Message = "C++ Hello World!";

	if (IsPrintHello)
	{
		// PrintStringノードと同じ処理
		// UKismetSystemLibraryクラスのPrintString関数を呼び出す
		UKismetSystemLibrary::PrintString(this, Message, true, true, TextColor, Duration);
	}
	else
	{
		if (CalcType == 0)
		{
			// Add(足し算)の処理
			int32 ResultAdd = CalcVarA + CalcVarB;
			FString StrResultAdd = FString::Printf(TEXT("%d"), ResultAdd);
			UKismetSystemLibrary::PrintString(this, StrResultAdd, true, true, FColor::Red, Duration);
		}
		else if (CalcType == 1)
		{
			// Subtract(引き算)の処理
			int32 ResultSubtract = CalcVarA - CalcVarB;
			FString StrResultSubtract = FString::Printf(TEXT("%d"), ResultSubtract);
			UKismetSystemLibrary::PrintString(this, StrResultSubtract, true, true, FColor::Yellow, Duration);
		}
		else if (CalcType == 2)
		{
			// Multiply(掛け算)の処理
			int32 ResultMultiply = CalcVarA * CalcVarB;
			FString StrResultMultiply = FString::Printf(TEXT("%d"), ResultMultiply);
			UKismetSystemLibrary::PrintString(this, StrResultMultiply, true, true, FColor::Green, Duration);
		}
		else
		{
			// Divide(割り算)の処理(int > float)
			float ResultDivide = (float)CalcVarA / (float)CalcVarB;
			FString StrResultDivide = FString::Printf(TEXT("%f"), ResultDivide);
			UKismetSystemLibrary::PrintString(this, StrResultDivide, true, true, FColor::Blue, Duration);
		}
	}
}

```

### Switch文で数値を分岐する（Switchノード）

Blueprintでは[Branch]ノードを使用して、計算結果の出力結果を切り替えていました。
C++で処理を再現します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-flow_control_switch/2022-01-23-21-23-19.png)


C++ではswitch文を使用します。
switch文の書き方は以下になります。

```cpp
switch(条件)
{
    case 0:
        処理1;
        break;
    case 1:
        処理2;
        break;
    case 2:
        処理3;
        break;
    default:
        条件が1,2,3のいずれにも当てはまらない時の処理;
}

// case内が複数行の場合は、{}で囲む

switch(条件)
{
    case 0:
    {
        処理1-1;
        処理1-2;
        break;
    }
    case 1:
    {
        処理2-1;
        処理2-2;
        break;
    }
    case 2:
    {
        処理3-1;
        処理3-2;
        break;
    }
    default:
    {
        条件が0,1,2のいずれにも当てはまらない時の処理1;
        条件が0,1,2のいずれにも当てはまらない時の処理2;
    }
}

```

変数[CalcType]の値をswitch文で切り替える処理に変更します。

```cpp:CPPFlowControlSwitch.cpp BeginPlay()

void ACPPFlowControlSwitch::BeginPlay()
{
	FString Message = "C++ Hello World!";

	if (IsPrintHello)
	{
		// PrintStringノードと同じ処理
		// UKismetSystemLibraryクラスのPrintString関数を呼び出す
		UKismetSystemLibrary::PrintString(this, Message, true, true, TextColor, Duration);
	}
	else
	{
		switch (CalcType)
		{
			case 0:
			{
				// Add(足し算)の処理
				int32 ResultAdd = CalcVarA + CalcVarB;
				FString StrResultAdd = FString::Printf(TEXT("%d"), ResultAdd);
				UKismetSystemLibrary::PrintString(this, StrResultAdd, true, true, FColor::Red, Duration);
				break;
			}
			case 1:
			{
				// Subtract(引き算)の処理
				int32 ResultSubtract = CalcVarA - CalcVarB;
				FString StrResultSubtract = FString::Printf(TEXT("%d"), ResultSubtract);
				UKismetSystemLibrary::PrintString(this, StrResultSubtract, true, true, FColor::Yellow, Duration);
				break;
			}
			case 2:
			{
				// Multiply(掛け算)の処理
				int32 ResultMultiply = CalcVarA * CalcVarB;
				FString StrResultMultiply = FString::Printf(TEXT("%d"), ResultMultiply);
				UKismetSystemLibrary::PrintString(this, StrResultMultiply, true, true, FColor::Green, Duration);
				break;
			}
			default:
			{
				// Divide(割り算)の処理(int > float)
				float ResultDivide = (float)CalcVarA / (float)CalcVarB;
				FString StrResultDivide = FString::Printf(TEXT("%f"), ResultDivide);
				UKismetSystemLibrary::PrintString(this, StrResultDivide, true, true, FColor::Blue, Duration);
			}
		}
	}
}

```

ソースコードを保存して、Compileを実行します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-print_string/2022-02-23-10-58-50.png)

「CPPFlowControlSwitch」をViewportにDrag&Dropします。
PrintStringの出力結果が分かりづらくなるので、「BP_FlowControl_Switch」を削除します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-flow_control_switch/2022-03-05-16-08-50.png)

Level Editorの[Play]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-print_string/2022-02-23-09-19-08.png)

変数[CalcType]の値が[1]なので、引き算の出力結果が表示されます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-flow_control_switch/2022-03-05-16-09-29.png)

### すべて保存

C++側の説明は以上になります。
プロジェクトをすべて保存しましょう。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-flow_control_switch/2022-03-05-16-10-40.png)

Visual StudioのSolutionもすべて保存しましょう。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-flow_control_switch/2022-01-23-21-46-14.png)

## C++とBlueprintの比較画像

C++とBlueprintの比較画像です。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-flow_control_switch/2022-02-13-15-36-37.png)

## ソースコードとプロジェクト

ここまでのソースコードとプロジェクトファイルをGitHubからダウンロードできます。

https://github.com/posita33/UE5Starter-CPPAndBP_Projects/tree/main/Resources/Chapter_02/FlowControl_Switch

**CPPFlowControlSwitch.h**

https://github.com/posita33/UE5Starter-CPPAndBP_Projects/blob/main/Resources/Chapter_02/FlowControl_Switch/Source_end/CPP_BP/Public/CPPFlowControlSwitch.h

**CPPFlowControlSwitch.cpp**

https://github.com/posita33/UE5Starter-CPPAndBP_Projects/blob/main/Resources/Chapter_02/FlowControl_Switch/Source_end/CPP_BP/Private/CPPFlowControlSwitch.cpp
