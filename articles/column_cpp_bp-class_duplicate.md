---
title: "【C++＆BP Column】BlueprintとC++のClassを複製する・継承したクラスを作成する"
emoji: "🥼"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["cpp", "unrealengine", "ue4", "ue5", "blueprint"]
published: true
---

## C++のClassのDuplicateは出来ないのか？

チュートリアルのチャプター毎にファイルを分けたいです。

Blueprintは右クリックから[Duplicate]を選択すれば複製できます。

では、C++で同じことをするにはどうしたらいいのだろう？

分からなかったので、調べてみました。

作成したクラスを継承したクラスを作成することもまとめました。

### C++とBPにHelloのPrintStringを出力するActorClassを作成する

Blueprint側にPrintStringでHelloと出力する処理を実装します。
![](/images/articles/column_cpp_bp-class_duplicate/2022-01-21-06-22-26.png)


C++側にも同様の処理を実装した「CPPActor」を実装します。
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

## クラスをDuplicate(複製)する 

同じ変数や関数を持ったクラスをDuplicate（複製）します。

### BlueprintのクラスをDuplicate(複製する)
まずは簡単にDuplicate（複製）できるBlueprintの手順です。
Duplicate(複製)したいBlueprintクラスを右クリックし、Duplicateを選択します。
ショートカットキーは[**Ctrl + W**]です。(「Ctrl + C」> [Ctrl + V]でもOK)
![](/images/articles/column_cpp_bp-class_duplicate/2022-01-21-06-43-12.png)

DuplicateされたBlueprintクラスを開くと、同じ処理が表示されます。
![](/images/articles/column_cpp_bp-class_duplicate/2022-01-21-06-50-54.png)

DuplicateしたBlueprintクラスの名前を変更します。
![](/images/articles/column_cpp_bp-class_duplicate/2022-01-21-08-00-35.png)

### C++のクラスは同じ親を持つクラスを作成して処理をコピー＆ペーストする
C++には複製機能が見つけられませんでした。
C++のクラスを別名でコピーするといった事はあまり行われず、継承することで処理として解決することが一般的でした。
ヘッダーファイルとCPPファイルの2つに分かれることも別名クラスファイルを作りづらい理由になっていました。

Contents BrowserからC++のクラスを右クリックして表示されるメニューはC++クラスを継承した新規C++かBlueprintのクラスを作成する項目でした。

|Menu |動作 |
|---|---|
|Create C++ class derived from (クラス) |(クラス)を継承したC++クラスを作成する|
|Create Blueprint class based on (クラス) |(クラス)を継承したBlueprintクラスを作成する |

![](/images/articles/column_cpp_bp-class_duplicate/2022-01-21-07-37-21.png)

一番早そうな方法は「**同じ親クラスを持つ新規クラスを作成 > 処理をCopy&Paste > クラス名を置換**」方法でした。

新規C++クラスを作成します。
![](/images/articles/column_cpp_bp-class_duplicate/2022-01-21-08-03-38.png)

ClassTypeを複製元と同じにして、名前を設定します。
![](/images/articles/column_cpp_bp-class_duplicate/2022-01-21-08-07-37.png)

Visual Studioで隣り合うようにパネルを動かして、処理をコピーします。
全体をコピーして、複製先にペーストする場合は、クラス名を置換することで対応できます。
クラス名次第で置換が上手くいかないこともありますので、気を付けてください。
![](/images/articles/column_cpp_bp-class_duplicate/2022-01-21-08-16-52.png)

![](/images/articles/column_cpp_bp-class_duplicate/2022-01-21-08-19-13.png)


## クラスを継承する

次に、作成したクラスを継承したクラスの作り方です。
クラスの継承はコンテンツブラウザでC++とBP両方とも対応できました。

### Blueprintの子クラスを作成する

Blueprintの子クラスを作成します。  
親クラスとなるBlueprintクラスを右クリックし、[Create Child Blueprint Class]を選択します。  
![](/images/articles/column_cpp_bp-class_duplicate/2022-01-21-20-53-50.png)

「(親クラスとなるBlueprintクラス名)_Child」が作成されます。
作成された子Blueprintを開いて、親クラスを確認します。
![](/images/articles/column_cpp_bp-class_duplicate/2022-01-21-20-58-26.png)

BlueprintEditorの右上に親クラス名が表示されます。
もう1つの確認方法は、「Class Settings」ボタンをクリックし、[Parent Class]プロパティから確認できます。[Parent Class]プロパティはリストから親クラスを変更できます。
![](/images/articles/column_cpp_bp-class_duplicate/2022-01-21-20-59-58.png)

### C++クラスを継承したC++クラスを作成する

Contents BrowserからC++のクラスを右クリックして表示されるメニューはC++クラスを継承した新規C++かBlueprintのクラスを作成する項目でした。
C++はクラスの複製はできなかったものの、継承したクラスを作成できます。
2つのメニューを選択した時の動きを説明します。

|Menu |動作 |
|---|---|
|Create C++ class derived from (クラス) |(クラス)を継承したC++クラスを作成する|
|Create Blueprint class based on (クラス) |(クラス)を継承したBlueprintクラスを作成する |

「Create C++ class derived from (クラス) 」メニューを実行してみます。
![](/images/articles/column_cpp_bp-class_duplicate/2022-01-21-21-08-15.png)

ClassTypeとNameを設定して、[Create Class]ボタンをクリックします。
![](/images/articles/column_cpp_bp-class_duplicate/2022-01-21-23-04-31.png)

「Create C++ class derived from (クラス) 」メニューを実行したC++クラスの子クラスが作成されます。
![](/images/articles/column_cpp_bp-class_duplicate/2022-01-21-21-18-46.png)

```h:CPPActorChild.h
// Fill out your copyright notice in the Description page of Project Settings.

#pragma once

#include "CoreMinimal.h"
#include "CPPActor.h"
#include "CPPActorChild.generated.h"

/**
 * 
 */
UCLASS()
class CLASSDUPLICATE_API ACPPActorChild : public ACPPActor
{
	GENERATED_BODY()
	
};

```

```cpp:CPPActorChild.cpp
// Fill out your copyright notice in the Description page of Project Settings.


#include "CPPActorChild.h"


```

```cpp:CPPActorChild.h
class CLASSDUPLICATE_API ACPPActorChild : public ACPPActor
「: public ACPPActor」の部分が親クラス
```

### C++クラスを継承したBlueprintを作成する
[Create Blueprint class based on (クラス) ]メニューを実行すると、C++クラスからBlueprintの子クラスを作成できます。

[Create Blueprint class based on (クラス) ]メニューを実行します。
![](/images/articles/column_cpp_bp-class_duplicate/2022-01-21-21-25-40.png)

子クラスとなるBlueprint名を設定します。
作成するフォルダを選択したら、[Create Blueprint Class]ボタンをクリックします。
![](/images/articles/column_cpp_bp-class_duplicate/2022-01-21-21-27-46.png)

選択したフォルダに移動すると、C++クラスの子クラスとなるBlueprintが作成されています。
![](/images/articles/column_cpp_bp-class_duplicate/2022-01-21-21-29-19.png)

親クラスを確認すると、[Create Blueprint class based on (クラス) ]メニューを実行したC++クラスの名前が表示されています。
![](/images/articles/column_cpp_bp-class_duplicate/2022-01-21-21-30-57.png)

## まとめ
Blueprintがあるから、あるだろうと思ったら無かった。
C++クラスの別名コピー＋リファクタリングを一緒にしてくれるような拡張が見つかりませんでした。
ありそうでない？
少し意外でした。
