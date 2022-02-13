---
title: "【C++】Array（配列）"
free: false
---

## 【C++】Event Dispatcher

### C++でBlueprintを再現すること

変数をArray（配列）に変更します。
Array（配列）の設定方法や取得について解説します。
![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-array/2022-01-29-22-59-46.png)

Array（配列）の取得でよく使用する2つの方法について解説します。

- Array（配列）をランダムに取得する。
- Array（配列）を剰余（％）を使用して順番に取得する。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-array/2022-01-30-11-58-55.png)

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-array/2022-01-30-07-50-57.png)

### 編集するActorクラスを作成する

プロジェクトを閉じていたら、プロジェクトを開き、「Chapter_2_Array」を開きます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-array/2022-02-13-19-07-25.png)

[Tools]メニューから[New C++ Class]を開きます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-array/2022-01-30-18-54-20.png)

親クラスに[Actor]を選択します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-array/2022-01-30-18-52-05.png)

ClassTypeとClass名を設定します。

| Property   | Value    |
| ---------- | -------- |
| Class Type | Public   |
| Name       | CPPArray |

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-array/2022-01-30-18-56-26.png)

Solution Explorerから今回編集する2つのファイルを開きます。

- CPPArray.h
- CPPArray.cpp

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-array/2022-02-13-19-11-31.png)

開いたファイルを学習する初期状態に修正します。

```cpp:CPPArray.h
// Fill out your copyright notice in the Description page of Project Settings.

#pragma once

#include "CoreMinimal.h"
#include "GameFramework/Actor.h"
#include "CPPCalcType.h"
#include "CPPArray.generated.h"

UCLASS()
class CPP_BP_API ACPPArray : public AActor
{
	GENERATED_BODY()

public:
	ACPPArray();

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

```cpp:CPPArray.cpp
// Fill out your copyright notice in the Description page of Project Settings.


#include "CPPArray.h"
#include "Kismet/KismetSystemLibrary.h"
#include "Kismet/GameplayStatics.h"

ACPPArray::ACPPArray()
{
	// Event Dispathcer[OnPrintHello]にCustom Event[PrintHello]をバインドする
	OnPrintHello.AddDynamic(this, &ACPPArray::PrintHello);
}

int32 ACPPArray::Sum(int32 A, int32 B)
{
	return A + B;
}

// Called when the game starts or when spawned
void ACPPArray::BeginPlay()
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

void ACPPArray::PrintCalcResult(const ECPPCalcType Type, const int32 A, const int32 B, const float PrintDuration)
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

void ACPPArray::SetupInput()
{
	// 入力を有効にする
	EnableInput(UGameplayStatics::GetPlayerController(GetWorld(), 0));

	// HキーのPressedとReleasedをバインドする
	InputComponent->BindKey(EKeys::H, IE_Pressed, this, &ACPPArray::PressedH);

	// ActionMappingsに設定したActionをバインドする
	InputComponent->BindAction("ActionPrintCalcResult", IE_Pressed, this, &ACPPArray::PressedActionPrintCalcResult);
}

void ACPPArray::PressedH()
{
	// Event Dispathcer[OnPrintHello]をコールする
	OnPrintHello.Broadcast();
}

void ACPPArray::PressedActionPrintCalcResult()
{
	// 計算結果を出力する処理
	PrintCalcResult(CalcType, CalcVarA, CalcVarB, Duration);
}

void ACPPArray::PrintHello()
{
	// Hello World!を出力する処理
	UKismetSystemLibrary::PrintString(this, Message, true, true, TextColor, Duration);
}
```

### 変数[Message]を配列の変数[Messages]に変更してDefaultValueを設定する

変数[Message]を配列の変数[Messages]に変更してDefaultValueを設定しました。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-array/2022-01-30-21-40-54.png)

C++で再現すると以下のようになります。

```cpp:CPPArray.h
FString Message = "C++ Hello World!";
		↓
TArray<FString> Messages = { TEXT("C++ Hello World!"), TEXT("你好 世界!"), TEXT("Bonjour le monde!"), TEXT("Hallo Welt!"), TEXT("こんにちは世界!")};
```

TArrayの<>内にVariableTypeを設定すると、VariableTypeの配列を宣言することになります。
Default Valueを設定するには{}内に","（カンマ）区切りで値を設定します。

```cpp
// 配列の初期化
TArray<(VariableType)> VariableName = { [0], [1], [2] };
```

### 変数[Messages]から値を取得する

変数[Messages]から値を取得しました。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-array/2022-01-30-21-44-56.png)

C++で再現すると以下のようになります。

```cpp:CPPArray.cpp PrintHello()
void ACPPArray::PrintHello()
{
	// Hello World!を出力する処理
	UKismetSystemLibrary::PrintString(this, Messages[4], true, true, TextColor, Duration);
}
```

C++の配列のGetは配列の変数の後ろに[]を入力し、[]内に取得したいIndexNoの数値を入力します。

```cpp
// 配列の値を取得する
ArrayVariable[IndexNo]
```

ソースコードを保存して、Compileを実行します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-array/2022-02-13-19-15-30.png)

「ACPPArray」をViewportにDrag&Dropします。
PrintStringの出力結果が分かりづらくなるので、「BP_Array」を削除します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-array/2022-02-13-19-17-32.png)

Level Editorの[Play]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-event_dispatcher/2022-01-29-00-54-14.png)

[H]キーをPressすると、変数[Messages]の[4]を取得するので、日本語の文字列が表示されました。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-array/2022-01-30-21-56-40.png)

TEXT("こんにちは世界!")を"こんにちは世界!"に変えてみます。

```cpp:CPPArray.h
TArray<FString> Messages = { TEXT("C++ Hello World!"), TEXT("你好 世界!"), TEXT("Bonjour le monde!"), TEXT("Hallo Welt!"), TEXT("こんにちは世界!")};
    ↓
TArray<FString> Messages = { "C++ Hello World!", "你好 世界!", "Bonjour le monde!", "Hallo Welt!", "こんにちは世界!" };
```

ソースコードを保存して、Compileを実行します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-array/2022-02-13-19-15-30.png)

Level Editorの[Play]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-event_dispatcher/2022-01-29-00-54-14.png)

”?????????????????????!”と文字化けして出力されてしまいました。
これはUnreaEngineとテキストの文字コードが違うので起こってしまった現象です。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-array/2022-01-30-21-59-06.png)

TEXTマクロで文字列をUnrealEngineが使用している文字コードに文字列を変換してくれます。日本語のような文字列（2バイト文字）を扱いたい時にはTEXTマクロを使用してFStringの変数に値を代入してください。

```cpp
// 文字化けする
FString str = "文字列";

// 文字化けをしない
FString str = TEXT("文字列");
```

### 変数[Messages]からランダムに値を取得する

変数[Messages]からランダムに値を取得しました。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-array/2022-01-30-22-07-15.png)

C++で再現すると以下のようになります。

```cpp:CPPArray.cpp PrintHello()
void ACPPArray::PrintHello()
{
	int32 randomIndex = FMath::RandRange(0, Messages.Num() - 1);

	// 1行で書くなら 
	// Messages[FMath::RandRange(0, Messages.Num() - 1)]

	// Hello World!を出力する処理
	UKismetSystemLibrary::PrintString(this, Messages[randomIndex], true, true, TextColor, Duration);
}
```

ランダムな範囲を取得するにはRandRange関数を使用します。

```cpp
// ランダムな範囲を取得する
FMath::RandRange(Min, Max)
```

配列の値をランダムに取得できました。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-array/2022-01-30-22-15-16.png)

Blueprintの処理はノードを複数つないでいますが、C++では1行で処理を書けます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-array/2022-01-30-22-18-34.png)

### 変数[CalcType]を配列の変数[CalcTypes]に変更する

剰余（％）を使用して、順番に配列を取得しました。

変数[CalcType]を配列の変数[CalcTypes]に変更します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-array/2022-02-13-19-23-56.png)

C++で再現すると以下のようになります。

```cpp:CPPArray.h
ECPPCalcType CalcType = ECPPCalcType::Add;
    ↓
TArray<ECPPCalcType> CalcTypes = { ECPPCalcType::Add, ECPPCalcType::Subtract, ECPPCalcType::Multiply, ECPPCalcType::Divide };
```

### 変数[CalcTypes]の値を順番に取得して出力する

変数[CalcTypes]の値を順番に取得して出力します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-array/2022-01-30-22-54-44.png)

配列のIndexNoを保持する変数を「CPPArray.h」に追加します。

```cpp:CPPArray.h
private:
    int32 TypeIndex = 0;
```

C++で再現すると以下のようになります。

```cpp:ACPPArray.cpp PressedActionPrintCalcResult()
void ACPPArray::PressedActionPrintCalcResult()
{
	// 計算結果を出力する処理
	PrintCalcResult(CalcTypes[TypeIndex], CalcVarA, CalcVarB, Duration);

	TypeIndex++;
	TypeIndex = TypeIndex % CalcTypes.Num();
}
```

ソースコードを保存して、Compileを実行します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-array/2022-02-13-19-15-30.png)

Level Editorの[Play]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-event_dispatcher/2022-01-29-00-54-14.png)

[C]キーをPressすると、変数[CalcTypes]の値を順番（[0:Add]> [1:Subtract] > [2:Multiply] > [3:Divide] > [0:Add] > 繰り返し）に出力します。

実行回数が配列数を越えるように実行した時の変数[TypeIndex]の値を表にしました。
[[3]:Divide]実行後、[[0]：Add]に戻って繰り返します。

| 実行回数 | Get時のTypeIndexの値 | CalcTypeResultのType | TypeIndex ++ | Length ％ TypeIndex | 最終的なTypeIndexの値 |
|------|------------------|---------------------|--------------|------------------|-----------------|
| 1    | 0                | [0]：Add             | 1            | 4%1              | 1               |
| 2    | 1                | [1]：Subtract        | 2            | 4%2              | 2               |
| 3    | 2                | [2]：Multiply        | 3            | 4%3              | 3               |
| 4    | 3                | [3]：Divide          | 4            | 4%4              | 0               |
| 5    | 0                | [0]：Add             | 1            | 4%1              | 1               |

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-array/2022-01-30-22-47-18.png)

BlueprintとC++の処理の対応図です。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-array/2022-01-30-22-53-50.png)

### すべて保存

C++側の説明は以上になります。
プロジェクトをすべて保存しましょう。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-array/2022-02-13-19-27-28.png)

Visual StudioのSolutionもすべて保存しましょう。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-flow_control_switch/2022-01-23-21-46-14.png)

## 参照URL 

https://docs.unrealengine.com/4.27/ja/ProgrammingAndScripting/ProgrammingWithCPP/UnrealArchitecture/TArrays/


## ソースコードとプロジェクト

ここまでのソースコードとプロジェクトファイルをGitHubからダウンロードできます。

https://github.com/posita33/UE5Starter-CPPAndBP_Projects/tree/main/Resources/Chapter_02/Array

**CPPArray.h**

https://github.com/posita33/UE5Starter-CPPAndBP_Projects/blob/main/Resources/Chapter_02/Array/Source_end/CPP_BP/Public/CPPArray.h

**CPPArray.cpp**

https://github.com/posita33/UE5Starter-CPPAndBP_Projects/blob/main/Resources/Chapter_02/Array/Source_end/CPP_BP/Private/CPPArray.cpp
