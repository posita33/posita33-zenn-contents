---
title: "【C++＆BP Column】BlueprintとC++のClassを複製する"
emoji: "📘"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["cpp", "unrealengine", "ue4", "ue5", "blueprint"]
published: false
---

## C++のClassのDuplicateは出来ないのか？

Blueprintは右クリックから[Duplicate]を選択すれば複製することができる。

では、C++で同じことをするにはどうしたらいいのだろう？

### C++とBPにHelloのPrintStringを出力するActorClassを作成する

![](/images/articles/column_cpp_bp-class_duplicate/2022-01-21-06-22-26.png)



![](/images/articles/column_cpp_bp-class_duplicate/2022-01-21-06-39-58.png)

```cpp:CPPActor.h
// Fill out your copyright notice in the Description page of Project Settings.

#pragma once

#include "CoreMinimal.h"
#include "GameFramework/Actor.h"
#include "CPPActor.generated.h"

UCLASS()
class CLASSDUPLICATE_API ACPPActor : public AActor
{
	GENERATED_BODY()

protected:
	// Called when the game starts or when spawned
	virtual void BeginPlay() override;
};
```

```cpp:.cpp
// Fill out your copyright notice in the Description page of Project Settings.

#include "CPPActor.h"
#include "Kismet/KismetSystemLibrary.h"

// Called when the game starts or when spawned
void ACPPActor::BeginPlay()
{
	UKismetSystemLibrary::PrintString(
		this
		, FString::Printf(TEXT("Hello"))
		, true
		, true
		, FColor::White
		, 10.0f);
}
```

### BlueprintのクラスをDuplicate(複製)する


![](/images/articles/column_cpp_bp-class_duplicate/2022-01-21-06-43-12.png)

![](/images/articles/column_cpp_bp-class_duplicate/2022-01-21-06-50-54.png)

![](/images/articles/column_cpp_bp-class_duplicate/2022-01-21-08-00-35.png)

### C++のクラスは同じ親を持つクラスを作成して処理をコピー＆ペーストする
C++には複製機能が見つけられませんでした。

Contents BrowserからC++のクラスを右クリックして表示されるメニューはC++クラスを継承した新規C++かBlueprintのクラスを作成する項目でした。

|Menu |動作 |
|---|---|
|Create C++ class derived from (クラス) |(クラス)を継承したC++クラスを作成する|
|Create Blueprint class based on (クラス) |(クラス)を継承したBlueprintクラスを作成する |

![](/images/articles/column_cpp_bp-class_duplicate/2022-01-21-07-37-21.png)

一番早そうな方法は「**同じ親クラスを持つ新規クラスを作成して、処理をCopy&Pasteする**」方法でした。

![](/images/articles/column_cpp_bp-class_duplicate/2022-01-21-08-03-38.png)


![](/images/articles/column_cpp_bp-class_duplicate/2022-01-21-08-07-37.png)


![](/images/articles/column_cpp_bp-class_duplicate/2022-01-21-08-16-52.png)

![](/images/articles/column_cpp_bp-class_duplicate/2022-01-21-08-19-13.png)