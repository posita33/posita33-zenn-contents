---
title: "関係を表す式"
free: false
---

## 問題

(1)

x円のクリームパンを5個とy円のアンパンを3個買って、3000円払ったらお釣りはz円でした。


(2)

x円のクリームパンを5個とy円のアンパンを3個買って、3000円払ったらお釣りはz円以下でした。


## 関係を表す式

### 等式

**等号**（=）を使って数量の関係を表した式を**等式**という。
等式で、等号の左側の式を**左辺**、右側の式を**右辺**、合わせて**両辺**という。

![](/images/books/book-ue5_mathematical_programming/chap_03_equation_for_the_relationship/2022-08-11-15-04-08.png)

### 不等式

不等号（≧, ≦, >, <）を使って数量の間の大小関係を表した式を**不等式**という。

![](/images/books/book-ue5_mathematical_programming/chap_03_equation_for_the_relationship/2022-08-11-15-49-33.png)


![](/images/books/book-ue5_mathematical_programming/chap_03_equation_for_the_relationship/2022-08-11-15-52-34.png)

### C++とBPの等号、不等号

```cpp
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

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-flow_control_branch/2022-03-05-11-20-27.png)

| 検索Word | Menu項目      | Blueprint                                                                                            | C++ | 数式 | 読み方     | 使い方 | 意味             |
| -------- | ------------- | ---------------------------------------------------------------------------------------------------- | --- | ---- | ---------- | ------ | ---------------- |
| ==       | Equal         | ![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-flow_control_branch/2022-01-22-14-27-56.png) | ==  | =    | 等しい     | A==B   | AとBは等しい     |
| <        | Less          | ![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-flow_control_branch/2022-01-22-14-28-23.png) | <   | <    | 小なり     | A<B    | AはBより小さい   |
| >        | Greater       | ![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-flow_control_branch/2022-01-22-14-28-48.png) | >   | ＞   | 大なり     | A>B    | AはBより大きい   |
| <=       | Less Equal    | ![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-flow_control_branch/2022-01-22-14-29-14.png) | <=  | ≦    | 以下       | A<=B   | AはB以下         |
| >=       | Greater Equal | ![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-flow_control_branch/2022-01-22-14-29-35.png) | >=  | ≧    | 以上       | A>=B   | AはB以上         |
| !=       | Not Equal     | ![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_bp-flow_control_branch/2022-01-22-14-29-57.png) | !=  | ≠    | 等しくない | A!=B   | AとBは等しくない |


## 問題の解答

(1)

x円のクリームパンを5個とy円のアンパンを3個買って、3000円払ったらお釣りはz円でした。

$$
3000 - (5x + 3y) = z
$$

(2)

x円のクリームパンを5個とy円のアンパンを3個買って、3000円払ったらお釣りはz円以下でした。

$$
3000 - (5x + 3y) \leqq z
$$

## BPで数式を表現

![](/images/books/book-ue5_mathematical_programming/chap_03_equation_for_the_relationship/2022-08-11-21-33-59.png)

## C++で数式を表現

```cpp
	float x = 1.0f;
	float y = 2.0f;
	float z = 0.0f;

	// (1) 3000−(5x+3y)=z
	if (3000 - ((5 * x) + (3 * y)) == z)
	{ }

	// (2) 3000−(5x+3y)≦z
	if (3000 - ((5 * x) + (3 * y)) <= z)
	{ }

```