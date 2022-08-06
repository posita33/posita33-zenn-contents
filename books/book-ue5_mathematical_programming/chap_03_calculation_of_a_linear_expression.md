---
title: "一次式の計算"
free: false
---

## 問題

(1)

$$
  5x - 8 - 2x + 4
$$

(2)

$$
  (8x - 5) - (-7x + 3)
$$

(3)

$$
 3(4x -3) - 4(2x - 2)
$$

(4)

$$
\frac{3x + 5}{4} - \frac{x - 3}{3}
$$

## 一次式の計算

### 一次式について

加法だけの式で加法の記号＋で結ばれたそれぞれを「**項（こう）**」という。
文字を含む項の数部分を「その項の**係数（けいすう）**」という。
数だけの項を「**定数項**」ということがある。
図の3xのように文字が１つだけの項を「**１次の項**」という。
1次の項だけか、1次の項と数だけの項からできている式を「**一次式**」という。

![](/images/books/book-ue5_mathematical_programming/chap_03_calculation_of_a_linear_expression/2022-08-06-10-34-47.png)

### 同類項

図の3xと2xのように文字の部分が同じ項は「**同類項**」という。

![](/images/books/book-ue5_mathematical_programming/chap_03_calculation_of_a_linear_expression/2022-08-06-10-57-29.png)

### 項をまとめる

文字の項、数の項どうしをまとめる。

![](/images/books/book-ue5_mathematical_programming/chap_03_calculation_of_a_linear_expression/2022-08-06-11-08-31.png)

### （）内の符号を変える

以下のような式の際に（）の符号を変更する

$$
 3x - (4x - 3)
$$

カッコ内の符号は反転する。

$$
 3x - 4x + 3
$$

### 縦書きの計算

1次式は縦書きの計算もできる。

![](/images/books/book-ue5_mathematical_programming/chap_03_calculation_of_a_linear_expression/2022-08-06-11-13-46.png)

### 乗法の交換法則

aとbをかける時に、aとbを入れ替えても積は同じになる。

$$
a \times b = b \times a
$$

プログラムでも積は同じになる。

![](/images/books/book-ue5_mathematical_programming/chap_03_calculation_of_a_linear_expression/2022-08-06-11-44-17.png)

### 乗法の結合法則

a,bとcをかける時、aとｂをかけた後にcをかけた積と、bとcを書けた後にaをかけた積は同じになる。

$$
(a \times b) \times c = a \times (b \times c)
$$

プログラムでも積は同じになる。

![](/images/books/book-ue5_mathematical_programming/chap_03_calculation_of_a_linear_expression/2022-08-06-11-47-19.png)

Blueprintであれば、AddPinでInputピンを増やして接続することができる。

![](/images/books/book-ue5_mathematical_programming/chap_03_calculation_of_a_linear_expression/2022-08-06-11-48-46.png)

### 分配法則

カッコの外の数値をカッコ内のすべての項にかける。

![](/images/books/book-ue5_mathematical_programming/chap_03_calculation_of_a_linear_expression/2022-08-06-11-40-03.png)

## 問題の解答

(1)

$$
  5x - 8 - 2x + 4
$$

$$
= 5x - 2x - 8 + 4
$$

$$
= 3x - 4
$$


(2)

$$
  (8x - 5) - (-7x + 3)
$$

$$
=  8x - 5 + 7x - 3
$$

$$
=  8x + 7x - 5 - 3
$$

$$
=  15x - 8
$$

(3)

$$
 3(4x - 3) - 4(2x - 2)
$$

$$
= 12x - 9 - 8x + 8
$$

$$
= 12x - 8x - 9 + 8
$$

$$
= 4x - 1
$$

(4)

$$
\frac{3x + 5}{4} - \frac{x - 3}{3}
$$

$$
= \frac{3(3x + 5)}{12} - \frac{4(x - 3)}{12}
$$

$$
= \frac{9x + 15}{12} - \frac{4x - 12}{12}
$$

$$
= \frac{9x + 15 - (4x - 12)}{12}
$$

$$
= \frac{9x + 15 - 4x + 12}{12}
$$

$$
= \frac{9x - 4x + 15 + 12}{12}
$$
$$
= \frac{5x + 27}{12}
$$

## BPで数式を表現

![](/images/books/book-ue5_mathematical_programming/chap_03_calculation_of_a_linear_expression/2022-08-06-16-08-31.png)

![](/images/books/book-ue5_mathematical_programming/chap_03_calculation_of_a_linear_expression/2022-08-06-16-10-45.png)

![](/images/books/book-ue5_mathematical_programming/chap_03_calculation_of_a_linear_expression/2022-08-06-16-23-36.png)

![](/images/books/book-ue5_mathematical_programming/chap_03_calculation_of_a_linear_expression/2022-08-06-16-23-11.png)

## C++で数式を表現

```cpp
	float x = 1;
	float answerF = 0.0f;

	// (1) 5x - 8 - 2x + 4
	answerF = (5.0f * x) - 8.0f - (2.0f * x) + 4.0f;

	// (2)  (8x - 5) - (-7x + 3)
	answerF = ((8.0f * x) - 5.0f) - ((-7.0f * x) + 3.0f);

	// (3)  3(4x - 3) - 4(2x - 2)
	answerF = (3.0f * ((4.0f * x) - 3.0f)) - (4.0f * ((2.0f * x) - 2.0f));

	// (4) (3x + 5) / 4 - (x - 3) / 3
	answerF = (((3.0f * x) + 5.0f) / 4.0f) - ((x - 3.0f) / 3.0f);
```