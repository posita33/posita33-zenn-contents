---
title: "【C++】Enumeration（列挙型）"
free: false
---

## 【C++】Enumeration（列挙型）

### C++でBlueprintを再現すること

Enumeration（列挙型）をC++で作成します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-enumeration/2022-01-24-13-08-54.png)

Switch文をint32から作成したEnumeration（列挙型）に変更します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-enumeration/2022-01-24-13-02-15.png)

### 編集するActorクラスを作成する

プロジェクトを閉じていたら、プロジェクトを開き、「Chapter_2_Enumeration」を開きます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-enumeration/2022-01-24-13-20-53.png)

[Tools]メニューから[New C++ Class]を開きます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-enumeration/2022-01-24-15-48-29.png)

親クラスに[Actor]を選択します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-enumeration/2022-01-24-16-00-18.png)

ClassTypeとClass名を設定します。

| Property   | Value                    |
| ---------- | ------------------------ |
| Class Type | Public                   |
| Name       | CPPFlowControlSwitchEnum |

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-enumeration/2022-01-24-16-03-05.png)

Solution Explorerから今回編集する2つのファイルを開きます。

- CPPFlowControlSwitchEnum.h
- CPPFlowControlSwitchEnum.cpp

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-enumeration/2022-01-24-17-19-58.png)

開いたファイルを学習する初期状態に修正します。

```cpp:CPPFlowControlSwitchEnum.h

// Fill out your copyright notice in the Description page of Project Settings.

#pragma once

#include "CoreMinimal.h"
#include "GameFramework/Actor.h"
#include "CPPFlowControlSwitchEnum.generated.h"

UCLASS()
class CPP_BP_API ACPPFlowControlSwitchEnum : public AActor
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

```cpp:CPPFlowControlSwitchEnum.cpp
// Fill out your copyright notice in the Description page of Project Settings.


#include "CPPFlowControlSwitchEnum.h"
#include "Kismet/KismetSystemLibrary.h"

// Called when the game starts or when spawned
void ACPPFlowControlSwitchEnum::BeginPlay()
{
	Super::BeginPlay();

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

### C++でEnumeration（列挙型）「ECPPCalcType」を作成する

C++でEnumeration（列挙型）を作成します。

[Tools]メニューから[New C++ Class]を開きます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-enumeration/2022-01-24-15-48-29.png)

親クラスに「None」を選択します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-enumeration/2022-01-24-16-56-11.png)

ClassTypeとClass名を設定します。

| Property   | Value       |
| ---------- | ----------- |
| Class Type | Public      |
| Name       | CPPCalcType |

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-enumeration/2022-01-24-21-28-59.png)

「CPPCalcType.h」のみ使用するので、「CPPCalcType.cpp」は削除します。
Solution Explorerから「CPPCalcType.cpp」をRemoveします。
Solution ExplorerからRemoveしても、ファイルは残っているので、Explorerから「CPPCalcType.cpp」を削除します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-enumeration/2022-01-24-17-25-56.png)

「CPPCalcType.h」にEnumeration（列挙型）を作成します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-enumeration/2022-01-24-17-38-48.png)


C++のEnumeration（列挙型）の書き方は以下のようになります。

```cpp:CPPCalcType.h
// Fill out your copyright notice in the Description page of Project Settings.

#pragma once

#include "CoreMinimal.h"
#include "CPPCalcType.generated.h"

UENUM(BlueprintType)
enum class ECPPCalcType : uint8
{
	Add,
	Subtract,
	Multiply,
	Divide
};

```

Solution Explorerから編集する2つのファイルを開きます。

- CPPFlowControlSwitchEnum.h
- CPPFlowControlSwitchEnum.cpp

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-enumeration/2022-01-24-17-19-58.png)

「CPPFlowControlSwitchEnum.h」を編集します。

- include文に「CPPCalcType.h」を追加する
- 変数[CalcType]のVariableTypeを[int32]から[ECPPCalcType]に変更する。
- 変数[CalcType]の値をECPPCalcType::Subtractに設定する。

```cpp:CPPFlowControlSwitchEnum.h

#include "CoreMinimal.h"
#include "CPPCalcType.h" // 追加
#include "CPPFlowControlSwitchEnum.generated.h"


	int32 CalcType = 1;
		↓    
	ECPPCalcType CalcType = ECPPCalcType::Subtract;

```

Enumeration（列挙型）を使用したswitch文の書き方は以下のようになります。

```cpp:.cpp
switch (CalcType)
{
    case ECPPCalcType::Add:
    {
        // Add(足し算)の処理
        break;
    }
    case ECPPCalcType::Subtract:
    {
        // Subtract(引き算)の処理
        break;
    }
    case ECPPCalcType::Multiply:
    {
        // Multiply(掛け算)の処理
        break;
    }
    case ECPPCalcType::Divide:
    {
        // Divide(割り算)の処理(int > float)
    }
}

```

「CPPFlowControlSwitchEnum.cpp」のswitch文を「ECPPCalcType」を使用した書き方に変更します。

```cpp:CPPFlowControlSwitchEnum.cpp

// Fill out your copyright notice in the Description page of Project Settings.


#include "CPPFlowControlSwitchEnum.h"
#include "Kismet/KismetSystemLibrary.h"

// Called when the game starts or when spawned
void ACPPFlowControlSwitchEnum::BeginPlay()
{
	Super::BeginPlay();

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
			case ECPPCalcType::Add:
			{
				// Add(足し算)の処理
				int32 ResultAdd = CalcVarA + CalcVarB;
				FString StrResultAdd = FString::Printf(TEXT("%d"), ResultAdd);
				UKismetSystemLibrary::PrintString(this, StrResultAdd, true, true, FColor::Red, Duration);
				break;
			}
			case ECPPCalcType::Subtract:
			{
				// Subtract(引き算)の処理
				int32 ResultSubtract = CalcVarA - CalcVarB;
				FString StrResultSubtract = FString::Printf(TEXT("%d"), ResultSubtract);
				UKismetSystemLibrary::PrintString(this, StrResultSubtract, true, true, FColor::Yellow, Duration);
				break;
			}
			case ECPPCalcType::Multiply:
			{
				// Multiply(掛け算)の処理
				int32 ResultMultiply = CalcVarA * CalcVarB;
				FString StrResultMultiply = FString::Printf(TEXT("%d"), ResultMultiply);
				UKismetSystemLibrary::PrintString(this, StrResultMultiply, true, true, FColor::Green, Duration);
				break;
			}
			case ECPPCalcType::Divide:
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

Ctrl + Sでファイルを保存し、Compileを行います。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-enumeration/2022-01-24-18-30-30.png)

「CPPFlowControlSwitchEnum」をViewportにDrag&Dropします。
PrintStringの出力結果が分かりづらくなるので、「BP_FlowControl_SwitchEnum」を削除します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-enumeration/2022-01-24-18-29-04.png)

Level Editorの[Play]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-enumeration/2022-01-24-18-31-04.png)

変数[CalcType]の値が[ECPPCalcType::Subtract]なので、引き算の出力結果が表示されます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-enumeration/2022-01-24-18-32-27.png)

### C++で作成したEnumeration（列挙型）をBlueprintで使用する

C++で作成したEnumeration（列挙型）を使用できます。
C++で作成したEnumeration「ECPPCalcType」をBlueprintで使用します。

「BP_FLowControl_SwitchEnum」を開きます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-enumeration/2022-01-24-18-39-04.png)


VariableTypeにEnumeration「ECPPCalcType」を設定した変数[CPPCalcType]を変数に追加します。

| VariableName | VariableType | Category     | DefaultValue |
| ------------ | ------------ | ------------ | ------------ |
| CPPCalcType  | ECPPCalcType | Flow Control | Subtract     |

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-enumeration/2022-01-24-18-42-01.png)

列挙型のDefaultValueですが、列挙定数が足りていない場合はプロジェクトを再起動してください。（UE5 EAしか起こらない？）

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-enumeration/2022-01-24-18-45-20.png)

追加した変数[CPPCalcType]でSwitchノードを作成してみます。
Bluerpintで作成したEnumeration[ECalcType]と同じOutputの実行ピンが表示されました。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-enumeration/2022-01-24-18-49-32.png)

### C++で作成したEnumeration（列挙型）のDisplayNameを設定する

SwitchノードのOutputの実行ピンに列挙定数の名前が使われていました。
C++では列挙定数名とは別に「DisplayName」を設定してOutputの実行ピンの名称を変更できます。

```cpp:CPPCalcType.h

// Fill out your copyright notice in the Description page of Project Settings.

#pragma once

#include "CoreMinimal.h"
#include "CPPCalcType.generated.h"

UENUM(BlueprintType)
enum class ECPPCalcType : uint8
{
	Add       UMETA(DisplayName = "Addition"),
	Subtract  UMETA(DisplayName = "Subtraction"),
	Multiply  UMETA(DisplayName = "Multiplicatation"),
	Divide    UMETA(DisplayName = "Division"),
};

```

Ctrl + Sでファイルを保存し、Compileを行います。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-enumeration/2022-01-24-18-30-30.png)

「CPPCalcType.h」を変更してCompileすると、変数[CPPCalcType]に設定していたVariableTypeが「HOTRELOADED ECPPCalcType 0」というVariableTypeになってしまいます。
VariableTypeを[ECPPCalcType]に再設定します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-enumeration/2022-01-24-18-58-51.png)

Switchノードを再度作成すると、[Switch]ノードの実行ピンの名称がDisplay Nameで設定した名称に変更されています。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-enumeration/2022-01-24-18-56-00.png)

### すべて保存

C++側の説明は以上になります。
プロジェクトをすべて保存しましょう。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-enumeration/2022-01-24-22-38-39.png)

Visual StudioのSolutionもすべて保存しましょう。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-flow_control_switch/2022-01-23-21-46-14.png)

## 参照URL

https://www.youtube.com/watch?v=aHHTXIqUUxY

https://papersloth.hatenablog.com/entry/2017/07/07/005225
