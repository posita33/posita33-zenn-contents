---
title: "文字を使った式"
free: false
---

## 問題

(1)

$$
  x \times 3 \times y
$$

(2)

$$
  (p - q) \div 5
$$

(3)

$$
  (-4) \times a \times a + 3 \times a
$$

(4)

$$
  x = -\frac{4}{7}のとき、式１： x - \frac{2}{3} 、式2： 5x ^ 2 - 2x の値を求めなさい。
$$

## 文字を使った式

### 文字式の表し方

- 積では記号×を省く
- 文字と数の積は、数を文字の前に書く
- 同じ文字の積は累乗の指数を使って表す
- 商では記号÷を使わずに分数の形で書く

### 1、-1と文字の式

1、-1と文字の積では、1を省略する。

$$
  x \times 1 = x、 x \times (-1) = -x
$$

### 商の記号

分数の符号は数字の前に書く。

$$
  x \div (-7) = - \frac{x}{7}
$$

### 代入、式の値

式の中の文字を数に置き換えることを、文字に数を**代入**するという。
代入して計算した結果を、その時の**式の値**という。

### 代入する時の注意

- 負の数を代入する時は、かっこを付けて代入する
- 指数の付いた式に分数を代入する時は、かっこをつけて代入する
- 分数の形の式に分数を代入するときは、÷を使った式に直してから代入する

## 問題の解答

(1)

$$
  x \times 3 \times y
$$

$$
  = 3xy
$$

(2)

$$
  (p - q) \div 5
$$

$$
  = \frac{p - q}{5}
$$

(3)

$$
  (-4) \times a \times a + 3 \times a
$$

$$
  = -4a^2 + 3a
$$

(4)

$$
  x = -\frac{4}{7}のとき、式１： x - \frac{2}{3} 、式2： 5x ^ 2 - 2x の値を求めなさい。
$$

---

$$
  式1：x - \frac{2}{3}
$$

$$
  = -\frac{4}{7} - \frac{2}{3}
$$

$$
  = -\frac{12}{21} - \frac{14}{21}
$$

$$
  = - \frac{26}{21}
$$

--- 

$$
  式2：5x ^ 2 - 2x
$$

$$
  = 5 \times (-\frac{4}{7})^ 2 - 2 \times (-\frac{4}{7})
$$

$$
  = 5 \times \frac{16}{49} - 2 \times (-\frac{4}{7})
$$

$$
  = \frac{80}{49} + \frac{8}{7}
$$

$$
  = \frac{80}{49} + \frac{56}{49}
$$

$$
  = \frac{136}{49}
$$

## BPで数式を表現

![](/images/books/book-ue5_mathematical_programming/chap_03_character_expression/2022-07-23-22-44-13.png)

Setノードでxに値を代入するか、Default Valueに値を設定する。

![](/images/books/book-ue5_mathematical_programming/chap_03_character_expression/2022-07-23-23-25-34.png)

![](/images/books/book-ue5_mathematical_programming/chap_03_character_expression/2022-07-23-23-23-39.png)

## C++で数式を表現

```cpp
	float x = 1.0f;
	float y = 1.0f;
	int p = 1;
	int q = 1;
	int a = 1;

	float answerF = 0.0f;
	int answerI = 0;

	// (1) x × 3 × y
	answerF = x * 3 * y;

	// (2) (p - q) ÷ 5
	answerI = (p - q) / 5;

	// (3) (−4) × a × a + 3 × a
	answerI = (4) * a * a + 3 * a;

	// (4) x = - 3/4
	x = -3 / 4;

	// (4) 式1： x - (2 / 3)
	answerF = x - (2 / 3);

	// (4) 式2： x^2 - 2x
	answerF = FMath::Pow(x, 2) - 2 * x;
```