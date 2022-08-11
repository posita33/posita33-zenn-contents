---
title: "一次式の計算の利用"
free: false
---

## 問題

(1)

$$
  A=3x-5, B=5-2xのとき、3A - 2Bを計算しなさい。
$$

(2)

下の図のように黒丸を並べます。

![](/images/books/book-ue5_mathematical_programming/chap_03_using_linear_calculations/2022-08-11-10-28-20.png)

① 4番目の図形で使う黒丸の個数を求めなさい。

② n番目の図形で使う黒丸の個数を、nを使った式で表しなさい。

## 問題の解答

(1)

$$
  A=3x-5, B=5-2xのとき、3A - 2Bを計算しなさい。
$$

$$
  3A - 2B
$$

$$
= 3(3x-5) - 2(5-2x)
$$

$$
= 9x - 15 - 10 + 4x
$$

$$
= 9x + 4x + 15 - 10
$$

$$
= 13x + 5
$$


(2)

下の図のように黒丸を並べます。

![](/images/books/book-ue5_mathematical_programming/chap_03_using_linear_calculations/2022-08-11-10-28-20.png)

① 4番目の図形で使う黒丸の個数を求めなさい。

![](/images/books/book-ue5_mathematical_programming/chap_03_using_linear_calculations/2022-08-11-10-45-35.png)

$$
2 + 3 \times 4
$$

$$
= 2 + 12
$$

$$
= 14
$$

② n番目の図形で使う黒丸の個数を、nを使った式で表しなさい。

![](/images/books/book-ue5_mathematical_programming/chap_03_using_linear_calculations/2022-08-11-10-49-15.png)

$$
2 + 3 \times n
$$

$$
= 2 + 3n
$$

$$
= 3n + 2
$$

## BPで数式を表現

![](/images/books/book-ue5_mathematical_programming/chap_03_using_linear_calculations/2022-08-11-11-03-27.png)

![](/images/books/book-ue5_mathematical_programming/chap_03_using_linear_calculations/2022-08-11-11-15-14.png)

## C++で数式を表現

```cpp
	float A = 0.0f;
	float B = 0.0f;
	float x = 1.0f;
	float n = 0.0f;
	float answerF = 0.0f;

	// (1) A=3x−5,B=5−2xのとき、3A−2Bを計算しなさい。
	A = (3.0f * x) - 5.0f;
	B = 5.0f - (2.0f * x);
	
	answerF = (3 * A) - (2 * B);

	// (2)
	// ② n番目の図形で使う黒丸の個数を、nを使った式で表しなさい。 
	// ① n = 4の時の個数
	n = 4.0f;
	answerF = (3 * n) + 2;
```