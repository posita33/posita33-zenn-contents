---
title: "【CPP】Structure（構造体）"
free: false
---

## 【C++】Structure（構造体）

### C++でBlueprintを再現すること

BlueprintのStructure（構造体）を使用した処理をC++で再現します。
Structure（構造体）は異なるVariableTypeの変数を1つにまとめられます。
Array（配列）との違いは、Array（配列）は1つのVariableTypeしか持てませんが、Structure（構造体）は異なるVariableTypeの変数を持つことができます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-structure/2022-02-05-15-00-04.png)

C++の構造体の作り方について知ることができます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-structure/2022-02-06-17-55-37.png)

PrintCalcResultのInputをStructer（構造体）に変更することでより処理が見やすくなります。
C++では参照渡しをConst宣言できるので安全に処理が軽くなります。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-structure/2022-02-06-18-16-25.png)

### 編集するActorクラスを作成する

プロジェクトを閉じていたら、プロジェクトを開き、「Chapter_2_Structure」を開きます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-structure/2022-02-13-22-08-25.png)

[Tools]メニューから[New C++ Class]を開きます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-structure/2022-02-06-12-16-08.png)

親クラスに[Actor]を選択します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-structure/2022-02-23-08-44-41.png)

ClassTypeとClass名を設定します。

| Property   | Value        |
| ---------- | ------------ |
| Class Type | Public       |
| Name       | CPPStructure |

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-structure/2022-02-06-13-06-19.png)

Solution Explorerから今回編集する2つのファイルを開きます。

- CPPStructure.h
- CPPStructure.cpp

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-structure/2022-02-13-22-10-36.png)

開いたファイルを学習する初期状態に修正します。

```cpp:CPPStructure.h
// Fill out your copyright notice in the Description page of Project Settings.

#pragma once

#include "CoreMinimal.h"
#include "GameFramework/Actor.h"
#include "CPPCalcType.h"
#include "CPPStructure.generated.h"

UCLASS()
class CPP_BP_API ACPPStructure : public AActor
{
	GENERATED_BODY()

public:
	ACPPStructure();

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

```cpp:CPPStructure.cpp
// Fill out your copyright notice in the Description page of Project Settings.


#include "CPPStructure.h"
#include "Kismet/KismetSystemLibrary.h"
#include "Kismet/GameplayStatics.h"

ACPPStructure::ACPPStructure()
{
	// Event Dispathcer[OnPrintHello]にCustom Event[PrintHello]をバインドする
	OnPrintHello.AddDynamic(this, &ACPPStructure::PrintHello);
}

int32 ACPPStructure::Sum(int32 A, int32 B)
{
	return A + B;
}

// Called when the game starts or when spawned
void ACPPStructure::BeginPlay()
{
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

void ACPPStructure::PrintCalcResult(const ECPPCalcType Type, const int32 A, const int32 B, const float PrintDuration)
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

void ACPPStructure::SetupInput()
{
	// 入力を有効にする
	EnableInput(UGameplayStatics::GetPlayerController(GetWorld(), 0));

	// HキーのPressedとReleasedをバインドする
	InputComponent->BindKey(EKeys::H, IE_Pressed, this, &ACPPStructure::PressedH);

	// ActionMappingsに設定したActionをバインドする
	InputComponent->BindAction("ActionPrintCalcResult", IE_Pressed, this, &ACPPStructure::PressedActionPrintCalcResult);
}

void ACPPStructure::PressedH()
{
	// Event Dispathcer[OnPrintHello]をコールする
	OnPrintHello.Broadcast();
}

void ACPPStructure::PressedActionPrintCalcResult()
{
	// 計算結果を出力する処理
	PrintCalcResult(CalcTypes[TypeIndex], CalcVarA, CalcVarB, Duration);

	TypeIndex++;
	TypeIndex = TypeIndex % CalcTypes.Num();
}

void ACPPStructure::PrintHello()
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

### Structure（構造体）「FCPPCalcInfo」を作成する

Structure（構造体）「FCPPCalcInfo」を作成します。

[Tools]メニューから[New C++ Class]を開きます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-structure/2022-02-06-12-16-08.png)

親クラスに[None]を選択します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-structure/2022-02-06-12-21-05.png)

ClassTypeとClass名を設定します。

| Property   | Value       |
| ---------- | ----------- |
| Class Type | Public      |
| Name       | CPPCalcInfo |

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-structure/2022-02-06-12-25-36.png)

「CPPCalcInfo.h」のみ使用するので、「CPPCalcInfo.cpp」は削除します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-structure/2022-02-13-22-21-56.png)

「CPPCalcInfo.h」を開きます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-structure/2022-02-13-22-22-59.png)

Unreal Engineのc++でStructure（構造体）を宣言する時は以下のように書きます。

```cpp
// Fill out your copyright notice in the Description page of Project Settings.

#pragma once

#include "CoreMinimal.h"
#include "(構造体名).generated.h"

USTRUCT(BlueprintType)
struct F(構造体名)
{
	GENERATED_BODY()

	変数宣言
};
```

BluerintのStructure（構造体）「FBPCalcInfo」をC++で再現します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-structure/2022-02-06-17-51-13.png)

C++で再現すると以下のような書き方になります。

```cpp:CPPCalcInfo.h
// Fill out your copyright notice in the Description page of Project Settings.

#pragma once

#include "CoreMinimal.h"
#include "CPPCalcType.h"
#include "CPPCalcInfo.generated.h"

USTRUCT(BlueprintType)
struct FCPPCalcInfo
{
	GENERATED_BODY()

	ECPPCalcType Type = ECPPCalcType::Add;
	int32 NumA = 7;
	int32 NumB = 3;
};
```

### Function「PrintCalcResultArgStructure」を作成する

引数にStructure（構造体）「FBPCalcInfo」を渡すFunction[PrintCalcResultArgStructure]を作成します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-structure/2022-02-06-16-33-12.png)

C++でFunction[PrintCalcResultArgStructure]を宣言します。

| Input/Output | VariableName | VariableType |
| ------------ | ------------ | ------------ |
| Input        | CalcInfo     | FCPPCalcInfo |
| Input        | Duration     | float        |


引数にStructure（構造体）「FCPPCalcInfo」を使用するので、CPPCalcInfo.hをincludeに追加します。

```cpp:CPPStructure.h

#include "CPPCalcInfo.h" // 追加

private：
	// 引数に構造体を使用した計算結果を出力する関数
	void PrintCalcResultArgStructure(const FCPPCalcInfo& CalcInfo, const float PrintDuration);
```

Function[PrintCalcResultArgStructure]のBlueprintの処理です。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-structure/2022-02-06-16-34-50.png)

Structure（構造体）「FCPPCalcInfo」のメンバー変数にアクセスするには[構造体変数.メンバー変数名]と書きます。

```cpp
void ACPPStructure::PrintCalcResultArgStructure(const FCPPCalcInfo& CalcInfo, const float PrintDuration)
{
	// 構造体変数名.メンバー変数名
	CalcInfo.Type
	CalcInfo.NumA
	CalcInfo.NumB
}
```

Function[PrintCalcResultArgStructure]の処理を以下のように書きます。

```cpp:CPPStructure.cpp PrintCalcResultArgStructure()
void ACPPStructure::PrintCalcResultArgStructure(const FCPPCalcInfo& CalcInfo, const float PrintDuration)
{
	switch (CalcInfo.Type)
	{
		case ECPPCalcType::Add:
		{
			// Add(足し算)の処理
			// 値渡し
			int32 ResultAdd = Sum(CalcInfo.NumA, CalcInfo.NumB);
			FString StrResultAdd = FString::Printf(TEXT("%d"), ResultAdd);
			UKismetSystemLibrary::PrintString(this, StrResultAdd, true, true, FColor::Red, PrintDuration);
			break;
		}
		case ECPPCalcType::Subtract:
		{
			// Subtract(引き算)の処理
			int32 ResultSubtract = CalcInfo.NumA - CalcInfo.NumB;
			FString StrResultSubtract = FString::Printf(TEXT("%d"), ResultSubtract);
			UKismetSystemLibrary::PrintString(this, StrResultSubtract, true, true, FColor::Yellow, PrintDuration);
			break;
		}
		case ECPPCalcType::Multiply:
		{
			// Multiply(掛け算)の処理
			int32 ResultMultiply = CalcInfo.NumA * CalcInfo.NumB;
			FString StrResultMultiply = FString::Printf(TEXT("%d"), ResultMultiply);
			UKismetSystemLibrary::PrintString(this, StrResultMultiply, true, true, FColor::Green, PrintDuration);
			break;
		}
		case ECPPCalcType::Divide:
		{
			// Divide(割り算)の処理(int > float)
			float ResultDivide = (float)CalcInfo.NumA / (float)CalcInfo.NumB;
			FString StrResultDivide = FString::Printf(TEXT("%f"), ResultDivide);
			UKismetSystemLibrary::PrintString(this, StrResultDivide, true, true, FColor::Blue, PrintDuration);
			break;
		}
	}
}
```

### Function[PrintCalcResultArgStructure]を使用した処理に編集する

Structure（構造体）の配列をBlueprintと同じになるように、C++でStructure（構造体）の配列を宣言します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-structure/2022-02-06-17-40-02.png)

C++で構造体を初期化するには以下のように書きます。

```cpp
// 構造体の初期化
FCPPCalcInfo CalcInfo = {ECPPCalcType::Add, 7, 3};

// 構造体の配列の初期化
TArray<FCPPCalcInfo> CalcInfos = {{ECPPCalcType::Add, 7, 3}, {ECPPCalcType::Subtract, 7, 3}}
```

「CPPStructure.h」に構造体の配列[CalcInfos]を宣言します。

```cpp:CPPStructure.h
private:
	TArray<FCPPCalcInfo> CalcInfos = { {ECPPCalcType::Add, 7, 3}
	                                 , {ECPPCalcType::Subtract, 7, 3}
	                                 , {ECPPCalcType::Multiply, 7, 3}
	                                 , {ECPPCalcType::Divide, 7, 3} 
	                                 };
```

Blueprintの構造体の配列を取得する処理をC++で再現します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-structure/2022-02-06-17-37-40.png)

C++で処理を再現するには以下のように書きます。

```cpp:CPPStructure.cpp PressedActionPrintCalcResult()
void ACPPStructure::PressedActionPrintCalcResult()
{
	// 構造体を引数に持った計算結果を出力する処理
	PrintCalcResultArgStructure(CalcInfos[TypeIndex], Duration);

	TypeIndex++;
	TypeIndex = TypeIndex % CalcTypes.Num();
}
```

ソースコードを保存して、Compileを実行します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-print_string/2022-02-23-10-58-50.png)

「CPPStructure」をViewportにDrag&Dropします。
PrintStringの出力結果が分かりづらくなるので、「BP_Structure」を削除します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-structure/2022-02-13-22-32-02.png)

Level Editorの[Play]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-print_string/2022-02-23-09-19-08.png)

[C]キーをPressするとStructure（構造体）の配列を順番に処理します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-structure/2022-02-06-17-43-37.png)

### すべて保存

C++側の説明は以上になります。
プロジェクトをすべて保存しましょう。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-structure/2022-02-13-22-33-37.png)

Visual StudioのSolutionもすべて保存しましょう。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-structure/2022-02-04-05-15-24.png)

## 参照URL

https://www.youtube.com/watch?v=F9zvOW4cm28

https://docs.microsoft.com/ja-jp/cpp/cpp/initializing-classes-and-structs-without-constructors-cpp?view=msvc-170

## ソースコードとプロジェクト

ここまでのソースコードとプロジェクトファイルをGitHubからダウンロードできます。

https://github.com/posita33/UE5Starter-CPPAndBP_Projects/tree/main/Resources/Chapter_02/Structure

**CPPCalcInfo.h**

https://github.com/posita33/UE5Starter-CPPAndBP_Projects/blob/main/Resources/Chapter_02/Structure/Source_end/CPP_BP/Public/CPPCalcInfo.h

**CPPStructure.h**

https://github.com/posita33/UE5Starter-CPPAndBP_Projects/blob/main/Resources/Chapter_02/Structure/Source_end/CPP_BP/Public/CPPStructure.h

**CPPStructure.cpp**

https://github.com/posita33/UE5Starter-CPPAndBP_Projects/blob/main/Resources/Chapter_02/Structure/Source_end/CPP_BP/Private/CPPStructure.cpp