---
title: "【C++】 PrintStringでHello World!"
emoji: "🐙"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["cpp", "unrealengine", "ue4", "ue5"]
published: false
---

## 【C++】PrintStringでHello World!

### C++でBlueprintを再現すること
【要執筆】。

### Event BeginPlayにPrint String関数を呼び出す処理を実装する

Visual Studio 2019を開きます。
UE5のエディタからは[Tools]メニューか、コンテンツブラウザから作成したActorクラスをダブルクリックとVisual Studioが開けます。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-print_string/2022-01-27-06-15-13.png)

CPPSampleActor.cppのBeginPlay関数にPrintString実装します。
まず、#inclueにKismet/KismetSystemLibrary.hを追加します。

```cpp:CPPSampleActor.cpp
#include "CPPSampleActor.h"
#include "Kismet/KismetSystemLibrary.h" //追加
```

Blueprintで普段使用しているPrintStringノードは、UKismetSystemLibraryクラスにPrintString関数として定義されています。
UKismetSystemLibraryクラスのPrintString関数を呼び出すように処理を追加します。

```cpp:CPPSampleActor.cpp BeginPlay()
void ACPPSampleActor::BeginPlay()
{
	Super::BeginPlay();
	
	// PrintStringノードと同じ処理
	// UKismetSystemLibraryクラスのPrintString関数を呼び出す
	UKismetSystemLibrary::PrintString(this, "C++ Hello World!", true, true, FColor::Cyan, 2.f);
}
```
ソースコードを変更したら、保存します（ショートカット：Ctrl＋Sで保存すると早いです）。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-print_string/2022-01-27-06-16-57.png)

Build ＞Build Solutionを行いコンパイルを行います。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-print_string/2022-01-27-06-17-19.png)

他の手段として、UE5のLevelEditor右下の小さいアイコンがC++のソースコードをコンパイルするボタンなので、アイコンをクリックするとコンパイルが実行されます。
「Compile Complite!」が表示されればコンパイル成功です。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-print_string/2022-01-27-06-17-30.png)

### LevelEditorのViewportにC++のクラスを追加してプレイする
「CPPSampleActor」をLevelEditorのViewportに追加します。
追加する方法はBlueprintと同じです。

- コンテンツブラウザから「CPPSampleActor」をレベルのビューポートにドラッグ&ドロップ
- Place Actorsの検索バーで「CPPSampleActor」を検索して、レベルのビューポートにドラッグ&ドロップ

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-print_string/2022-01-27-06-34-14.png)

C++のActorクラスにはコンポーネントが何もないのでサムネイルが表示されません。レベルに追加されたかは[World Outliner]から確認してください。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-print_string/2022-01-27-06-34-35.png)

[Play]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-print_string/2022-01-27-06-34-49.png)

BluepintのPrintStringノードと同様にLevelEditorのVieport左上に出力がされました。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-print_string/2022-01-27-06-35-06.png)

Output LogタブにもBlueprintノードのPrintStringノードと同様の出力がされています。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-print_string/2022-01-27-06-35-21.png)

### UKismetSystemLibraryクラスのPrintString関数とBlueprintのPrintStringノードを比較する

UKismetSystemLibraryクラスのPrintString関数とBlueprintのPrintStringノードを比較します。
UKismetSystemLibraryクラスのPrintString関数の引数と、BlueprintのInputピンの関係している箇所を矢印で示してみました。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-print_string/2022-01-27-06-35-51.png)

UKismetSystemLibraryクラスのPrintString関数の関係している箇所を変更するとPrintStringノードのように文字列の出力方法を変更できます。

・”文字列”の個所を別の文字に変えれば、出力される文字が変更されます。
・左側の[true]を[false]と書くと、LevelEditorのViewport左上の文字列が出力されなくなります。
・右側の[true]を[false]と書くと、Output Logタブの文字列が出力されなくなります。
・[FColor::Cyan]と書かれているところを、別の色に変更すれば色が変わります。
・[2.f]と書かれている箇所を、[10.0f]に変えれば10秒間表示されるようになっています。

関数の引数については関数について書くときに詳しく説明します。

```cpp:
UKismetSystemLibrary::PrintString(this, "C++ Hello World!", true, true, FColor::Cyan, 2.f);
    ↓
UKismetSystemLibrary::PrintString(this, "C++ Hello World! Change", false, false, FColor::White, 10.f);
```

ブループリントは左から右に、C++は上から下に実行される
C++とBlueprintでは処理の実行される方向が違います。

C++は処理の実行が「**上から下**」
Blueprintは処理の実行が「**左から右**」

ソースコードのプログラミングに慣れていたので、Blueprintは処理の流れる方向が違うため最初は慣れませんでした。
UE4でBlueprintに慣れている人がC++をさわり始めると、上から下に処理が流れることに違和感を覚えるでしょう。

慣れの問題なので、どちらも慣れるまで書くしか解決法がありません。
たくさん書きましょう。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-print_string/2022-01-27-06-37-48.png)

### PrintStringノードの正体
PrintStringノードは、KismetSystemLibrary.hで定義され、KismetInputLibrary.cppで実装されています。

PrintStringノードのプロトタイプ宣言は以下になります。

```cpp
ヘッダーの場所：Program Files\Epic Games\UE_5.0EA\Engine\Source\Runtime\Engine\Classes\Kismet\KismetSystemLibrary.h  

/**
 * Prints a string to the log, and optionally, to the screen
 * If Print To Log is true, it will be visible in the Output Log window.  Otherwise it will be logged only as 'Verbose', so it generally won't show up.
 *
 * @param	InString		The string to log out
 * @param	bPrintToScreen	Whether or not to print the output to the screen
 * @param	bPrintToLog		Whether or not to print the output to the log
 * @param	bPrintToConsole	Whether or not to print the output to the console
 * @param	TextColor		Whether or not to print the output to the console
 * @param	Duration		The display duration (if Print to Screen is True). Using negative number will result in loading the duration time from the config.
 */
UFUNCTION(BlueprintCallable, meta=(WorldContext="WorldContextObject", CallableWithoutWorldContext, Keywords = "log print", AdvancedDisplay = "2", DevelopmentOnly), Category="Utilities|String")
static void PrintString(const UObject* WorldContextObject, const FString& InString = FString(TEXT("Hello")), bool bPrintToScreen = true, bool bPrintToLog = true, FLinearColor TextColor = FLinearColor(0.0, 0.66, 1.0), float Duration = 2.f);

```

PrintStringノードの関数の定義は以下になります。

```cpp
cppの場所：Program Files\Epic Games\UE_5.0EA\Engine\Source\Runtime\Engine\Private\KismetInputLibrary.cpp

void UKismetSystemLibrary::PrintString(const UObject* WorldContextObject, const FString& InString, bool bPrintToScreen, bool bPrintToLog, FLinearColor TextColor, float Duration)
{
#if !(UE_BUILD_SHIPPING || UE_BUILD_TEST) // Do not Print in Shipping or Test

	UWorld* World = GEngine->GetWorldFromContextObject(WorldContextObject, EGetWorldErrorMode::ReturnNull);
	FString Prefix;
	if (World)
	{
		if (World->WorldType == EWorldType::PIE)
		{
			switch(World->GetNetMode())
			{
				case NM_Client:
					// GPlayInEditorID 0 is always the server, so 1 will be first client.
					// You want to keep this logic in sync with GeneratePIEViewportWindowTitle and UpdatePlayInEditorWorldDebugString
					Prefix = FString::Printf(TEXT("Client %d: "), GPlayInEditorID);
					break;
				case NM_DedicatedServer:
				case NM_ListenServer:
					Prefix = FString::Printf(TEXT("Server: "));
					break;
				case NM_Standalone:
					break;
			}
		}
	}
	
	const FString FinalDisplayString = Prefix + InString;
	FString FinalLogString = FinalDisplayString;

	static const FBoolConfigValueHelper DisplayPrintStringSource(TEXT("Kismet"), TEXT("bLogPrintStringSource"), GEngineIni);
	if (DisplayPrintStringSource)
	{
		const FString SourceObjectPrefix = FString::Printf(TEXT("[%s] "), *GetNameSafe(WorldContextObject));
		FinalLogString = SourceObjectPrefix + FinalLogString;
	}

	if (bPrintToLog)
	{
		UE_LOG(LogBlueprintUserMessages, Log, TEXT("%s"), *FinalLogString);
		
		APlayerController* PC = (WorldContextObject ? UGameplayStatics::GetPlayerController(WorldContextObject, 0) : NULL);
		ULocalPlayer* LocalPlayer = (PC ? Cast<ULocalPlayer>(PC->Player) : NULL);
		if (LocalPlayer && LocalPlayer->ViewportClient && LocalPlayer->ViewportClient->ViewportConsole)
		{
			LocalPlayer->ViewportClient->ViewportConsole->OutputText(FinalDisplayString);
		}
	}
	else
	{
		UE_LOG(LogBlueprintUserMessages, Verbose, TEXT("%s"), *FinalLogString);
	}

	// Also output to the screen, if possible
	if (bPrintToScreen)
	{
		if (GAreScreenMessagesEnabled)
		{
			if (GConfig && Duration < 0)
			{
				GConfig->GetFloat( TEXT("Kismet"), TEXT("PrintStringDuration"), Duration, GEngineIni );
			}
			GEngine->AddOnScreenDebugMessage((uint64)-1, Duration, TextColor.ToFColor(true), FinalDisplayString);
		}
		else
		{
			UE_LOG(LogBlueprint, VeryVerbose, TEXT("Screen messages disabled (!GAreScreenMessagesEnabled).  Cannot print to screen."));
		}
	}
#endif
}
```

難しそうですが、実際に関係あるのはAddOnScreenDebugMessage関数とUE_LOGマクロです。

- **GEngine->AddOnScreenDebugMessage関数**：LevelEditorのViewport左上に文字列を出力する関数
- **UE_LOGマクロ**：Output Tagに文字列を出力するマクロ

```cpp
// LevelEditorのViewport左上に文字列を出力する関数
GEngine->AddOnScreenDebugMessage((uint64)-1, Duration, TextColor.ToFColor(true), FinalDisplayString);

// Output Tagに文字列を出力するマクロ
UE_LOG(LogBlueprint, VeryVerbose, TEXT("Screen messages disabled (!GAreScreenMessagesEnabled).  Cannot print to screen."));
```

GEngine->AddOnScreenDebugMessage関数とUE_LOGマクロを使用する処理を追加して、文字列を出力してみましょう。
CPPSampleActor.cpp BeginPlay関数に処理を追加します。

```cpp
void ACPPSampleActor::BeginPlay()
{
	Super::BeginPlay();

	// PrintStringノードと同じ処理
	// UKismetSystemLibraryクラスのPrintString関数を呼び出す
	UKismetSystemLibrary::PrintString(this, "C++ Hello World!", true, true, FColor::Cyan, 2.f);

	// Output Logに文字列を出力するマクロ
	UE_LOG(LogTemp, Display, TEXT("Display Message"));
	UE_LOG(LogTemp, Warning, TEXT("Warning Message"));
	UE_LOG(LogTemp, Error, TEXT("Error Message"));

	// Viewportの左上に文字列を出力する関数
	GEngine->AddOnScreenDebugMessage(-1, 10.0f, FColor::White, "C++ Hello World!", true, FVector2D(2.0f, 2.0f));
}
```

ソースコードを保存して、Compileを実行します。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-print_string/2022-01-27-06-40-44.png)

[Play]ボタンをクリックします。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-print_string/2022-01-27-06-40-54.png)

PrintString関数とは違うサイズで出力されました。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-print_string/2022-01-27-06-41-04.png)

Output Logにはそれぞれ色の違う文字列が出力されています。

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-print_string/2022-01-27-06-41-47.png)


### すべて保存

C++側の説明は以上になります。
プロジェクトをすべて保存しましょう。

【画像差し替え】
![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-function/2022-01-26-16-00-41.png)

Visual StudioのSolutionもすべて保存しましょう。
![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_cpp-flow_control_switch/2022-01-23-21-46-14.png)


## 【参照URL】

https://docs.unrealengine.com/4.27/ja/ProgrammingAndScripting/ProgrammingWithCPP/UnrealArchitecture/StringHandling/FString/

https://docs.unrealengine.com/4.27/en-US/API/Runtime/Engine/Engine/UEngine/AddOnScreenDebugMessage/1/
