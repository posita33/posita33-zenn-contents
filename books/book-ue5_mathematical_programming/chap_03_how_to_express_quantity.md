---
title: "数量の表し方"
free: false
---

## 問題

(1)

1個130円のリンゴをa個、6個300円のミカンをb個、
5本250円のバナナを3本買った時の代金の合計

(2)

xkmの道のり時速40kmで進み、ykmの道のりを30kmで進んだ時にかかった時間

(3)

定価x円の商品を、定価のy割引で購入した時の値段

(4)

底辺がxcm、高さがycmの三角形と半径rcmの円が重なっている時の、
波線部分の面積（円周率はπとする）

![](/images/books/book-ue5_mathematical_programming/chap_03_how_to_express_quantity/2022-07-30-22-11-29.png)

## 数量の表し方

### 代金の計算

$$
(代金) = (単価) \times (個数)
$$

### 2桁の整数の表し方

十の位がx、一の位がyの時、

$$
 10x + y
$$

### 速さ・時間・道のり

$$
（道のり） = （速さ） \times （時間）
$$

$$
 （速さ） = \frac{（道のり）}{（時間）} 
$$

$$
（時間） = \frac{（道のり）}{（速さ）} 
$$

### 百分率（ひゃくぶんりつ）

$$
\frac{1}{100} または、0.001を1％（パーセント）と書く
$$

$$
 x％ =　\frac{x}{100}
$$

### 歩合（ぶあい）

$$
 1割（いちわり） = \frac{1}{10} = 10％
$$

$$
 1分（いちぶ） = \frac{1}{100} = 1％
$$

$$
 1厘（いちりん） = \frac{1}{1000} = 0.1％
$$

### 面積

$$
（三角形の面積） = （底辺）\times（高さ）\div 2
$$

$$
（長方形の面積） = （縦の長さ）\times （横の長さ）
$$

$$
（平行四辺形の面積） = （底辺）\times （高さ）
$$

$$
（台形の面積）= （上底 + 下底）\times （高さ） \div 2
$$

### 円の円周と面積

$$
（円周率） = （円周の長さ） \times （直径）
$$

$$
（円周の長さ） = （直径）\times （円周率）
$$

$$
（円の面積） = （半径）\times （半径） \times （円周率）
$$

### 

## 問題の解答

(1)

1個130円のリンゴをa個、6個300円のミカンをb個、
5本250円のバナナを3本買った時の代金の合計

$$
 (130 \times a) + ((300 \div 6) \times b ) + ((250 \div 5) \times 3)
$$

$$
= 130a + 50b + 150 (円)
$$

(2)

xkmの道のり時速40kmで進み、ykmの道のりを30kmで進んだ時にかかった時間

$$
(x \div 40) + (y \div 30) 
$$

$$
= \frac{x}{40} + \frac{y}{30} （時間）
$$


(3)

定価x円の商品を、定価のy割引で購入した時の値段

$$
 x(1-\frac{y}{10}) または、x - \frac{xy}{10}（円） 
$$

(4)

底辺がxcm、高さがycmの三角形と半径rcmの円が重なっている時の、
斜線部分の面積（円周率はπとする）

![](/images/books/book-ue5_mathematical_programming/chap_03_how_to_express_quantity/2022-07-30-22-12-19.png)

$$
(x \times y \div 2) - (r \times r \times \pi)
$$

$$
 = \frac{xy}{2} - \pi r^2（cm^2）
$$

## BPで数式を表現

![](/images/books/book-ue5_mathematical_programming/chap_03_how_to_express_quantity/2022-07-31-08-40-22.png)

![](/images/books/book-ue5_mathematical_programming/chap_03_how_to_express_quantity/2022-07-31-08-16-13.png)

![](/images/books/book-ue5_mathematical_programming/chap_03_how_to_express_quantity/2022-07-31-08-20-35.png)

![](/images/books/book-ue5_mathematical_programming/chap_03_how_to_express_quantity/2022-07-31-08-30-50.png)

πをかける時に使えるノード「Multiply by Pi」、「Get PI」

![](/images/books/book-ue5_mathematical_programming/chap_03_how_to_express_quantity/2022-07-31-08-27-39.png)

## C++で数式を表現

```cpp
	int a = 1;
	int b = 1;
	int x = 1;
	int y = 1;
	int r = 1;
	int answerI = 0;
	int answerF = 0.0f;

	// (1) (130×a)+((300÷6)×b)+((250÷5)×3)
	answerI = (130 * a) + ((300 / 6) * b) + ((250 / 5) * 3);

	// (2) (x / 40) + (y / 30)
	answerI = (x / 40) + (y / 30);

	// (3) x - (xy / 10)
	answerI = x - (x * y / 10);

	// (4) (xy / 2) - πr^2
	answerF = (x * y / 2.0f) - (r * r * PI);
```

定数「PI」を使用するには、Math/UnrealMathUtility.hをIncludeします。

```cpp
#include “Math/UnrealMathUtility.h”

float mathPi = PI;
```

https://forums.unrealengine.com/t/what-is-the-equivalent-of-math-pi-in-the-unreal-engine-api/273833

Blueprintと同じPiをかけるための関数を使用するには「Kismet/KismetMathLibrary.h」をIncludeします。

```cpp
#include "Kismet/KismetMathLibrary.h"

・・・

	answerF = (x * y / 2.0f) - (r * r * UKismetMathLibrary::GetPI());

	answerF = (x * y / 2.0f) - (UKismetMathLibrary::MultiplyByPi(r * r));
```