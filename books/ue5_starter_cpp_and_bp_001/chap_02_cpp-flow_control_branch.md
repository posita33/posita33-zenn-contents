---
title: "【C++】Flow Control（Branch）"
free: false
---

## 【C++】Flow Control（Branch）

### C++でBlueprintのFlow Control（Branch）を再現する

[Branch]ノード処理を切り替える。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-flow_control_branch/2022-01-23-06-39-50.png)

比較演算子ノードで処理を切り替える。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-flow_control_branch/2022-01-23-06-42-05.png)

論理演算子ノードで処理を切り替える。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-flow_control_branch/2022-01-23-06-42-26.png)

複数の選択肢で分岐する。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-flow_control_branch/2022-01-23-06-42-55.png)


### 編集するActorクラスを作成する

プロジェクトを閉じていたら、プロジェクトを開き、「Chapter_2_FlowControl_Branch」を開きます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-flow_control_branch/2022-01-23-06-03-53.png)

[Tools]メニューから[New C++ Class]を開きます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-flow_control_branch/2022-01-23-06-09-39.png)

親クラスに[Actor]を選択します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-flow_control_branch/2022-01-23-06-08-00.png)

ClassTypeとClass名を設定します。

| Property   | Value                |
| ---------- | -------------------- |
| Class Type | Public               |
| Name       | CPPFlowControlBranch |

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-flow_control_branch/2022-01-23-06-12-16.png)

Solution Explorerから今回編集する2つのファイルを開きます。

- CPPFlowControlBranch.h
- CPPFlowControlBranch.cpp

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-flow_control_branch/2022-01-23-06-22-17.png)


開いたファイルを学習する初期状態に修正します。

```h:CPPFlowControlBranch.h
// Fill out your copyright notice in the Description page of Project Settings.

#pragma once

#include "CoreMinimal.h"
#include "GameFramework/Actor.h"
#include "CPPFlowControlBranch.generated.h"

UCLASS()
class CPP_BP_API ACPPFlowControlBranch : public AActor
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
};

```

```cpp:CPPFlowControlBranch.cpp
// Fill out your copyright notice in the Description page of Project Settings.


#include "CPPFlowControlBranch.h"
#include "Kismet/KismetSystemLibrary.h"

// Called when the game starts or when spawned
void ACPPFlowControlBranch::BeginPlay()
{
	Super::BeginPlay();

	FString Message = "C++ Hello World!";

	// PrintStringノードと同じ処理
	// UKismetSystemLibraryクラスのPrintString関数を呼び出す
	UKismetSystemLibrary::PrintString(this, Message, true, true, TextColor, Duration);

	// Add(足し算)の処理
	int32 ResultAdd = CalcVarA + CalcVarB;
	FString StrResultAdd = FString::Printf(TEXT("%d"), ResultAdd);
	UKismetSystemLibrary::PrintString(this, StrResultAdd, true, true, FColor::Red, Duration);

	// Subtract(引き算)の処理
	int32 ResultSubtract = CalcVarA - CalcVarB;
	FString StrResultSubtract = FString::Printf(TEXT("%d"), ResultSubtract);
	UKismetSystemLibrary::PrintString(this, StrResultSubtract, true, true, FColor::Yellow
		, Duration);

	// Multiply(掛け算)の処理
	int32 ResultMultiply = CalcVarA * CalcVarB;
	FString StrResultMultiply = FString::Printf(TEXT("%d"), ResultMultiply);
	UKismetSystemLibrary::PrintString(this, StrResultMultiply, true, true, FColor::Green, Duration);

	// Divide(割り算)の処理(int > float)
	float ResultDivide = (float)CalcVarA / (float)CalcVarB;
	FString StrResultDivide = FString::Printf(TEXT("%f"), ResultDivide);
	UKismetSystemLibrary::PrintString(this, StrResultDivide, true, true, FColor::Blue, Duration);
}
```

### Flow Controlに使用する変数を宣言する

今回使用する変数を宣言します。

| VariableName | VariableType | DefaultValue |
| ------------ | ------------ | ------------ |
| IsPrintHello | bool         | true         |
| CalcType     | int32        | 0            |
| NumA         | int32        | 1            |
| NumB         | int32        | 2            |
| NumC         | int32        | 15           |
| IsBlueprint  | bool         | true         |

```cpp:CPPFlowControlBranch.h
private:
	// Flow Control用の変数
	bool IsPrintHello = true;
	int32 CalcType = 1;
	int32 NumA = 1;
	int32 NumB = 2;
	int32 NumC = 15;
	bool IsPrintHello = true;
```

### if/else文で処理を切り替える（Branchノード）

[Branch]ノード処理を切り替える処理をC++で再現します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-flow_control_branch/2022-01-23-06-39-50.png)

C++では**if文**を使用します。
if文の書き方は以下になります。

```cpp

if(条件)
{
    // 条件がtrueなら
    処理1
}
else
{
    // 条件がfalseなら
    処理2
}

```

CPPFlowControlBranch.cpp BeginPlay関数をif文で修正しましょう。

```cpp:CPPFlowControlBranch.cpp BeginPlay()
void ACPPFlowControlBranch::BeginPlay()
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
		// Add(足し算)の処理
		int32 ResultAdd = CalcVarA + CalcVarB;
		FString StrResultAdd = FString::Printf(TEXT("%d"), ResultAdd);
		UKismetSystemLibrary::PrintString(this, StrResultAdd, true, true, FColor::Red, Duration);

		// Subtract(引き算)の処理
		int32 ResultSubtract = CalcVarA - CalcVarB;
		FString StrResultSubtract = FString::Printf(TEXT("%d"), ResultSubtract);
		UKismetSystemLibrary::PrintString(this, StrResultSubtract, true, true, FColor::Yellow
			, Duration);

		// Multiply(掛け算)の処理
		int32 ResultMultiply = CalcVarA * CalcVarB;
		FString StrResultMultiply = FString::Printf(TEXT("%d"), ResultMultiply);
		UKismetSystemLibrary::PrintString(this, StrResultMultiply, true, true, FColor::Green, Duration);

		// Divide(割り算)の処理(int > float)
		float ResultDivide = (float)CalcVarA / (float)CalcVarB;
		FString StrResultDivide = FString::Printf(TEXT("%f"), ResultDivide);
		UKismetSystemLibrary::PrintString(this, StrResultDivide, true, true, FColor::Blue, Duration);
	}
}
```

Ctrl + Sでファイルを保存し、Compileを行います。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-flow_control_branch/2022-01-23-07-02-24.png)

LevelEditorに戻り、「CPPFlowControlBranch」をViewportにDrag&Dropします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-flow_control_branch/2022-01-23-07-00-33.png)

Level Editorの[Play]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-flow_control_branch/2022-01-23-07-03-47.png)

変数[IsPrintHello]の値がtrueなので、「Hello World!」を出力するPrintStringが実行されました。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-flow_control_branch/2022-01-23-07-04-59.png)


### 比較演算子で条件を書く（比較演算子ノード）

比較演算子ノードでBranchノードの実行ピンを切り替える処理をC++で再現します。
Blueprint側では比較演算子を使用して「NumAとNumBは等しい」という条件を作りました。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-flow_control_branch/2022-01-23-06-42-05.png)

比較演算子を使用したif文の書き方は以下になります。

```cpp
if(変数A == 変数B)
{
    // 変数Aと変数Bの値が同じなら
    処理1
}
else
{
    // 変数Aと変数Bの値が違うなら
    処理2
}
```

BeginPlay関数のif文の条件を比較演算子を使用するように変更します。
（計算結果を出力する処理は変更がないので省略して書いてあります）

```cpp:CPPFlowControlBranch.cpp BeginPlay()

	if (NumA == NumB)
	{
		// PrintStringノードと同じ処理
		// UKismetSystemLibraryクラスのPrintString関数を呼び出す
		UKismetSystemLibrary::PrintString(this, Message, true, true, TextColor, Duration);
	}
	else
	{
		(計算結果を出力する処理)
	}

```

Ctrl + Sでファイルを保存し、Compileを行います。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-flow_control_branch/2022-01-23-07-02-24.png)

Level Editorの[Play]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-flow_control_branch/2022-01-23-07-03-47.png)

変数[NumA][NumB]の値は等しくないので、falseとなり、計算結果を出力する処理が実行されます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-flow_control_branch/2022-01-23-10-14-05.png)


比較演算子は「==」以外にも用意されています。
条件文の種類と同じ値の時、どのような結果になるかまとめました。

```cpp
if(条件)
{
    // 条件がtrueなら
    処理1
}
else
{
    // 条件がfalseなら
    処理2
}

比較演算子を使用した条件文

A == B  ：AとBが等しい
A < B   ：AはBより小さい
A > B   ：AはBより大きい
A <= B  ：AはB以下
A >= B  ：AはB以上
A != B  ：AとBは等しくない

A=3,B=3で等しい時
A == B : true
A <  B ：false
A <= B ：true
A >  B ：false
A >= B ：true
A != B : false
```

C++とBlueprintの比較演算子をまとめた一覧です。

| C++ | Blueprint                                                                                            | 数式 | 読み方     | 使い方 | 意味             |
| --- | ---------------------------------------------------------------------------------------------------- | ---- | ---------- | ------ | ---------------- |
| ==  | ![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-flow_control_branch/2022-01-22-14-27-56.png) | =    | 等しい     | A==B   | AとBは等しい     |
| <   | ![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-flow_control_branch/2022-01-22-14-28-23.png) | <    | 小なり     | A<B    | AはBより小さい   |
| >   | ![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-flow_control_branch/2022-01-22-14-28-48.png) | ＞   | 大なり     | A>B    | AはBより大きい   |
| <=  | ![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-flow_control_branch/2022-01-22-14-29-14.png) | ≦    | 以下       | A<=B   | AはB以下         |
| >=  | ![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-flow_control_branch/2022-01-22-14-29-35.png) | ≧    | 以上       | A>=B   | AはB以上         |
| !=  | ![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-flow_control_branch/2022-01-22-14-29-57.png) | ≠    | 等しくない | A!=B   | AとBは等しくない |



### 論理演算子で複雑な条件を書く（論理演算子ノード）

論理演算子ノードでBranchノードの実行ピンを切り替える処理をC++で再現します。
Blueprint側では論理演算子を使用して「NumCは10より大きく、30以下」という条件を作りました。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-flow_control_branch/2022-01-23-06-42-26.png)

C++で論理演算子を使用する時の書き方です。

```cpp
if(条件1 && 条件2)
{
    // 条件1かつ条件2がtrueなら
    処理1
}
else
{
    // 条件1,条件2がfalseなら
    処理2
}
```

BeginPlay関数のif文の条件を論理演算子を使用するように変更します。

```cpp:CPPFlowControlBranch.cpp BeginPlay()
	if (10<NumC && NumC<=30)
	{
		// PrintStringノードと同じ処理
		// UKismetSystemLibraryクラスのPrintString関数を呼び出す
		UKismetSystemLibrary::PrintString(this, Message, true, true, TextColor, Duration);
	}
	else
	{
		(計算結果を出力する処理)
	}
```

Ctrl + Sでファイルを保存し、Compileを行います。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-flow_control_branch/2022-01-23-07-02-24.png)

Level Editorの[Play]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-flow_control_branch/2022-01-23-07-03-47.png)

変数[NumC]の値は[15]なので、「NumCは10より大きく、30以下」の結果は[true]になり、「Hello World!」を出力するPrintStringの処理が実行されました。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-flow_control_branch/2022-01-23-10-23-36.png)

C++側の「AND Boolean」「OR Boolean」「Not Boolean」の書き方です。
```cpp

// AND Boolean
if(条件1 && 条件2)
{
    // 条件1かつ条件2がtrueなら
    処理1
}
else
{
    // 条件1,条件2がfalseなら
    処理2
}

// OR Boolean
if(条件1 || 条件2)
{
    // 条件1か条件2がtrueなら
    処理1
}
else
{
    // 条件1と条件2の両方がfalseなら
    処理2
}

// Not Boolean
if(!条件)
{
    // 条件がfalseなら
    処理1
}
else
{
    // 条件がtrueなら
    処理2
}

```
C++とBlueprintの論理演算子をまとめた一覧です。

| C++  | Blueprint                                                                                            | 読み方     | 使い方       | 意味              |
| ---- | ---------------------------------------------------------------------------------------------------- | ---------- | ------------ | ----------------- |
| &&   | ![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-flow_control_branch/2022-01-22-17-11-11.png) | かつ       | 1<=a&&a<=5   | aは1以上かつ5以下 |
| \|\| | ![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-flow_control_branch/2022-01-22-17-25-28.png) | または     | a==1\|\|a==2 | Aの値が1または2   |
| !    | ![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-flow_control_branch/2022-01-22-17-25-50.png) | ～ではない | !(a==1)      | Aは1ではない      |

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-flow_control_branch/2022-01-23-14-37-43.png)


### 条件演算子で変数に代入する値を変える

C++側のみですが、**条件演算子**という書き方があります。

```cpp
	FString Message = "C++ Hello World!";
          ↓
	FString Message = (IsBlueprint) ? "Blueprint Hello World!" : "C++ Hello World!";
```

Ctrl + Sでファイルを保存し、Compileを行います。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-flow_control_branch/2022-01-23-07-02-24.png)

Level Editorの[Play]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-flow_control_branch/2022-01-23-07-03-47.png)

変数[Message]の値が「Blueprint Hello World!」で出力されました。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-flow_control_branch/2022-01-23-10-39-25.png)

条件演算子は変数の値を条件で値を代入できます。

```cpp
// 条件演算子
変数 = (条件) ? A : B; 

条件がtrueの時：変数にはAの値が代入される
条件がfalseの時：変数にはBの値が代入される
```

### 連続したif文で複数の選択肢（Branchノード複数で切り替える）

[Branch]ノードを複数呼び出して、複数の選択肢で分岐する処理をC++で再現します。
Blueprint側では変数[CalcType]の数値で引き算の計算結果を1つだけPrintStringで出力するように変更しました。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-flow_control_branch/2022-01-23-06-42-55.png)

C++で複数の条件で分岐したいときは、[else if]を使用します。

```cpp
if(条件1)
{
    // 条件1がtrueなら
    処理1
}
else if(条件2)
{
    // 条件2がtrueなら
    処理2
}
else if(条件3)
{
    // 条件3がtrueなら
    処理3
}
else
{
    // どの条件もfalseなら
    処理4
}
```
Blueprint側と同様に、変数[CalcType]の数値で引き算の計算結果を1つだけPrintStringで出力するように変数のDefaulValueを変更します。

| VariableName | VariableType | DefaultValue |
| ------------ | ------------ | ------------ |
| IsPrintHello | bool         | false        |
| CalcType     | int32        | 1            |

```cpp:CPPFlowControlBranch.h
	// Flow Control用の変数
	bool IsPrintHello = true;
	int32 CalcType = 1;
	int32 NumA = 1;
	int32 NumB = 2;
	int32 NumC = 15;
	bool IsPrintHello = true;
```

計算結果を出力する処理を変数[CalcType]の値で分岐するように変更しましょう。

```cpp:CPPFlowControlBranch.cpp BeginPlay()
void ACPPFlowControlBranch::BeginPlay()
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

Ctrl + Sでファイルを保存し、Compileを行います。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-flow_control_branch/2022-01-23-07-02-24.png)

Level Editorの[Play]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-flow_control_branch/2022-01-23-07-03-47.png)

変数[CalcType]の値が[1]なので、引き算の計算結果のPrintStringが実行されました。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-flow_control_branch/2022-01-23-11-26-47.png)

### C++とBlueprintの比較画像

C++とBlueprintの比較画像です。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-flow_control_branch/2022-01-23-21-54-25.png)

### すべて保存

C++側の説明は以上になります。
プロジェクトをすべて保存しましょう。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-flow_control_branch/2022-01-23-11-38-13.png)

Visual StudioのSolutionもすべて保存しましょう。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-flow_control_branch/2022-01-23-11-39-43.png)
