---
title: "整数の性質"
free: false
---

## 問題

(1)
100以下の整数のうち、4の倍数であって、8の倍数ではない整数を求めよう。

(2)
「210」を素因数分解しよう。

(3)
素因数分解を利用して、「90」の約数をすべて求めよう。

(4)

90にできるだけ小さな自然数をかけて、ある整数の2乗にします。どんな数をかけますか。


## 一次式の計算の利用

### 倍数と約数

整数x,yが　y = x × (整数)　で表せるとき、

yはxの「**倍数**」、xはyの「**約数**」といいます。

### 素数

1とその数自信のほかの約数がない数を「**素数**」といいます。
ただし、1は素数ではありません。

### 因数

整数が靴化の自然数の積の形で表されるとき、その一つ一つの数を**因数**といいます。

「33 = 3 x 11」と表されるので、3と11は33の因数です。

### 素因数

素数である因数を**素因数**といいます。

### 素因数分解

自然数を素因数の積で表すことを**素因数分解**といいます。

### 約数とその個数

$$
ある自然数がa^2 \times b^2 \times c^2のように素因数分解できるとき
$$

$$
a^xの約数は1, a , a^2・・・a^x → x + 1
$$

$$
b^yの約数は1, b , b^2・・・b^y → y + 1
$$

$$
c^zの約数は1, c , c^2・・・c^z → z + 1
$$

$$
(x+1) \times (y+1) \times (z+1) で求められる。
$$

### 指数法則

![](/images/books/book-ue5_mathematical_programming/chap_04_properties_of_integers/2022-08-20-18-32-51.png)

$$
(5^2)^3 = 25^3 = 3125
$$

$$
5^{2 \times 3} = 5^6 = 3125
$$

$$
(5^2)^3 = 5^{2 \times 3}
$$

![](/images/books/book-ue5_mathematical_programming/chap_04_properties_of_integers/2022-08-20-18-33-10.png)

$$
3^2 \times 4^2 = 9 \times 16 = 144
$$

$$
(3 \times 4)^2 = 12^2 = 144
$$

$$
3^2 \times 4^2 = (3 \times 4)^2
$$

## 問題の解答

(1)
100以下の整数のうち、4の倍数であって、8の倍数ではない整数を求めよう。

![](/images/books/book-ue5_mathematical_programming/chap_04_properties_of_integers/2022-08-20-07-47-51.png)

100以下の自然数の「4の倍数」の個数から「8の倍数」の個数を引けば解答を求められます。

$$
（4の倍数）100 \div 4 = 25　余り 0
$$

$$
（8の倍数）100 \div 8 = 12　余り 4
$$

$$
25 - 12
$$

$$
= 13(個)
$$

(2)
「210」を素因数分解しよう。

![](/images/books/book-ue5_mathematical_programming/chap_04_properties_of_integers/2022-08-20-21-35-12.png)

$$
210 = 2 \times 3 \times 5 \times 7
$$

(3)
素因数分解を利用して、「90」の約数をすべて求めよう。

90を素因数分解します。

![](/images/books/book-ue5_mathematical_programming/chap_04_properties_of_integers/2022-08-20-22-10-12.png)

90の約数

- 1
- 2, 3, 5
- 素因数2つの積：2×3=6, 3²=9, 2×5=10, 3×5=15
- 素因数3つの積：2x3²=18, 2x3x5=30 3²×5=45
- 素因数4つの積：2x3²x5=90

$$
1, 2, 3, 5, 6, 9, 10, 15, 18, 30, 45, 90
$$

(4)
90にできるだけ小さな自然数をかけて、ある整数の2乗にします。どんな数をかけますか。

90を素因数分解します。

![](/images/books/book-ue5_mathematical_programming/chap_04_properties_of_integers/2022-08-20-22-14-24.png)

指数が奇数の因数を偶数にするには、2と5をかけます。

$$
(2 \times 3^2 \times 5) \times (2 \times 5)
$$

$$
 = 2^2 \times 3^2 \times 5^2
$$

$$
 = (2 \times 3 \times 5)^2
$$

$$
 = 30^2
$$

$$
かける数は、2 \times 5 = 10になります。
$$

## BPで数式を表現

(1)
100以下の整数のうち、4の倍数であって、8の倍数ではない整数を求めよう。

![](/images/books/book-ue5_mathematical_programming/chap_04_properties_of_integers/2022-08-20-23-00-24.png)

(2)
「210」を素因数分解しよう。

![](/images/books/book-ue5_mathematical_programming/chap_04_properties_of_integers/2022-08-20-23-04-55.png)

(3)
素因数分解を利用して、「90」の約数をすべて求めよう。

プログラムであれば色んな求め方があります。1番シンプルなプログラムを組んでみます。

90までの数をループで回して、割った時に余が0になる値を配列に追加します。
ループが完了した時には、配列に約数が追加されています。

![](/images/books/book-ue5_mathematical_programming/chap_04_properties_of_integers/2022-08-20-23-14-18.png)

(4)
90にできるだけ小さな自然数をかけて、ある整数の2乗にします。どんな数をかけますか。

1～100の中に「ある整数の2乗」、「解答のかける数」があるとして考えてみます。

90に1～100をかけます。
90にかけた数から1～100を割ります。
2乗なので、割る数と割った数が同じになったら二乗です。
その際に、割った時に余りがないことも確認します。

![](/images/books/book-ue5_mathematical_programming/chap_04_properties_of_integers/2022-08-20-23-39-30.png)

## C++で数式を表現

```cpp
	int answerI = 0;
	bool answerB = false;

	// (1) 100以下の整数のうち、4の倍数であって、8の倍数ではない整数を求めよう。
	answerI = (100 / 4) - (100 / 8);
	
	// (2) 「210」を素因数分解しよう。
	answerB = 2 * 3 * 5 * 7 == 210;

	// (3) 素因数分解を利用して、「90」の約数をすべて求めよう。
	int num = 90;
	TArray<int> divisors = {};

	for (int i = 1; i <= num; i++)
	{
		if(num % i == 0)
			divisors.Add(i);
	}

	// (4) 90にできるだけ小さな自然数をかけて、ある整数の2乗にします。どんな数をかけますか。
	num = 90;

	for (int i = 1; i <= 100; i++)
	{
		for (int j = 1; j <= 100; j++)
			// 割る数と割った数が同じになって余りは0
			if (num * i / j == j && num * i % j == 0)
			{
				// このときのiの値が解答
				break;
			}
	}
```
