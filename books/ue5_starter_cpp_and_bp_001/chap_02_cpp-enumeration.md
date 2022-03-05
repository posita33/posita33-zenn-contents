---
title: "【C++】Enumeration（列挙型）"
free: false
---

## 【C++】Enumeration（列挙型）

### C++でBlueprintを再現すること

Enumeration（列挙型）をC++で作成します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-enumeration/2022-03-05-16-38-04.png)

Switch文をint32から作成したEnumeration（列挙型）に変更します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-enumeration/2022-01-24-13-02-15.png)

### 編集するActorクラスを作成する

プロジェクトを閉じていたら、プロジェクトを開き、「Chapter_2_Enumeration」を開きます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-enumeration/2022-03-05-16-39-06.png)

[Tools]メニューから[New C++ Class]を開きます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-enumeration/2022-03-05-16-39-55.png)

親クラスに[Actor]を選択します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-enumeration/2022-02-23-08-38-35.png)

ClassTypeとClass名を設定します。

| Property   | Value                    |
| ---------- | ------------------------ |
| Class Type | Public                   |
| Name       | CPPFlowControlSwitchEnum |

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-enumeration/2022-03-05-16-41-39.png)

Solution Explorerから今回編集する2つのファイルを開きます。

- CPPFlowControlSwitchEnum.h
- CPPFlowControlSwitchEnum.cpp

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-enumeration/2022-02-13-16-19-30.png)

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

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-enumeration/2022-03-05-16-39-55.png)

親クラスに「None」を選択します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-enumeration/2022-03-05-16-46-20.png)

ClassTypeとClass名を設定します。

| Property   | Value       |
| ---------- | ----------- |
| Class Type | Public      |
| Name       | CPPCalcType |

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-enumeration/2022-03-05-16-48-05.png)

「CPPCalcType.h」のみ使用するので、「CPPCalcType.cpp」は削除します。
Solution Explorerから「CPPCalcType.cpp」をRemoveします。
Solution ExplorerからRemoveしても、ファイルは残っているので、Explorerから「CPPCalcType.cpp」を削除します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-enumeration/2022-02-13-16-25-32.png)

「CPPCalcType.h」にEnumeration（列挙型）を作成します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-enumeration/2022-02-13-16-26-33.png)

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

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-enumeration/2022-02-13-16-19-30.png)

「CPPFlowControlSwitchEnum.h」を編集します。

- include文に「CPPCalcType.h」を追加する
- 変数[CalcType]のVariableTypeを[int32]から[ECPPCalcType]に変更する。
- 変数[CalcType]の値をECPPCalcType::Subtractに設定する。

```cpp:CPPFlowControlSwitchEnum.h

#include "CoreMinimal.h"
#include "CPPCalcType.h" // 追加
#include "GameFramework/Actor.h"
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

ソースコードを保存して、Compileを実行します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-print_string/2022-02-23-10-58-50.png)

「CPPFlowControlSwitchEnum」をViewportにDrag&Dropします。
PrintStringの出力結果が分かりづらくなるので、「BP_FlowControl_SwitchEnum」を削除します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-enumeration/2022-03-05-16-54-57.png)

Level Editorの[Play]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-print_string/2022-02-23-09-19-08.png)

変数[CalcType]の値が[ECPPCalcType::Subtract]なので、引き算の出力結果が表示されます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-enumeration/2022-03-05-16-55-41.png)

### C++で作成したEnumeration（列挙型）をBlueprintで使用する

C++で作成したEnumeration（列挙型）を使用できます。
C++で作成したEnumeration「ECPPCalcType」をBlueprintで使用します。

「BP_FLowControl_SwitchEnum」を開きます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-enumeration/2022-03-05-16-57-05.png)


VariableTypeにEnumeration「ECPPCalcType」を設定した変数[CPPCalcType]を変数に追加します。

| VariableName | VariableType | Category     | DefaultValue |
| ------------ | ------------ | ------------ | ------------ |
| CPPCalcType  | ECPPCalcType | Flow Control | Subtract     |

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-enumeration/2022-02-13-16-37-51.png)

列挙型のDefaultValueですが、列挙定数が足りていない場合はプロジェクトを再起動してください。（UE5 EAしか起こらない？）

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-enumeration/2022-01-24-18-45-20.png)

追加した変数[CPPCalcType]でSwitchノードを作成してみます。
Bluerpintで作成したEnumeration[EBPCalcType]と同じOutputの実行ピンが表示されました。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-enumeration/2022-02-13-16-39-37.png)

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

ソースコードを保存して、Compileを実行します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-print_string/2022-02-23-10-58-50.png)

「CPPCalcType.h」を変更してCompileすると、変数[CPPCalcType]に設定していたVariableTypeが「LIVECODING ECPPCalcType 0」というVariableTypeになってしまいます。
VariableTypeを[ECPPCalcType]に再設定します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-enumeration/2022-03-05-17-05-02.png)

Switchノードを再度作成すると、[Switch]ノードの実行ピンの名称がDisplay Nameで設定した名称に変更されています。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-enumeration/2022-02-13-16-45-33.png)

### すべて保存

C++側の説明は以上になります。
プロジェクトをすべて保存しましょう。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-enumeration/2022-03-05-17-07-25.png)

Visual StudioのSolutionもすべて保存しましょう。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-flow_control_switch/2022-01-23-21-46-14.png)

## 参照URL

https://www.youtube.com/watch?v=aHHTXIqUUxY

https://papersloth.hatenablog.com/entry/2017/07/07/005225


## ソースコードとプロジェクト

ここまでのソースコードとプロジェクトファイルをGitHubからダウンロードできます。

https://github.com/posita33/UE5Starter-CPPAndBP_Projects/tree/main/Resources/Chapter_02/Enumeration

**CPPCalcType.h**

https://github.com/posita33/UE5Starter-CPPAndBP_Projects/blob/main/Resources/Chapter_02/Enumeration/Source_end/CPP_BP/Public/CPPCalcType.h

**CPPFlowControlSwitchEnum.h**

https://github.com/posita33/UE5Starter-CPPAndBP_Projects/blob/main/Resources/Chapter_02/Enumeration/Source_end/CPP_BP/Public/CPPFlowControlSwitchEnum.h

**CPPFlowControlSwitchEnum.cpp**

https://github.com/posita33/UE5Starter-CPPAndBP_Projects/blob/main/Resources/Chapter_02/Enumeration/Source_end/CPP_BP/Private/CPPFlowControlSwitchEnum.cpp
