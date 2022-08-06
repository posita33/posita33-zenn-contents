---
title: "📕2章 文字と式 まとめ📕"
free: false
---

## 数学的知識

### 文字を使った式

#### 文字式の表し方

- 積では記号×を省く
- 文字と数の積は、数を文字の前に書く
- 同じ文字の積は累乗の指数を使って表す
- 商では記号÷を使わずに分数の形で書く

#### 1、-1と文字の式

1、-1と文字の積では、1を省略する。

$$
  x \times 1 = x、 x \times (-1) = -x
$$

#### 商の記号

分数の符号は数字の前に書く。

$$
  x \div (-7) = - \frac{x}{7}
$$

#### 代入、式の値

式の中の文字を数に置き換えることを、文字に数を**代入**するという。
代入して計算した結果を、その時の**式の値**という。

#### 代入する時の注意

- 負の数を代入する時は、かっこを付けて代入する
- 指数の付いた式に分数を代入する時は、かっこをつけて代入する
- 分数の形の式に分数を代入するときは、÷を使った式に直してから代入する


### 数量の表し方

#### 代金の計算

$$
(代金) = (単価) \times (個数)
$$

#### 2桁の整数の表し方

十の位がx、一の位がyの時、

$$
 10x + y
$$

#### 速さ・時間・道のり

$$
（道のり） = （速さ） \times （時間）
$$

$$
 （速さ） = \frac{（道のり）}{（時間）} 
$$

$$
（時間） = \frac{（道のり）}{（速さ）} 
$$

#### 百分率（ひゃくぶんりつ）

$$
\frac{1}{100} または、0.001を1％（パーセント）と書く
$$

$$
 x％ =　\frac{x}{100}
$$

#### 歩合（ぶあい）

$$
 1割（いちわり） = \frac{1}{10} = 10％
$$

$$
 1分（いちぶ） = \frac{1}{100} = 1％
$$

$$
 1厘（いちりん） = \frac{1}{1000} = 0.1％
$$

#### 面積

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

#### 円の円周と面積

$$
（円周率） = （円周の長さ） \times （直径）
$$

$$
（円周の長さ） = （直径）\times （円周率）
$$

$$
（円の面積） = （半径）\times （半径） \times （円周率）
$$

### 一次式の計算

#### 一次式について

加法だけの式で加法の記号＋で結ばれたそれぞれを「**項（こう）**」という。
文字を含む項の数部分を「その項の**係数（けいすう）**」という。
数だけの項を「**定数項**」ということがある。
図の3xのように文字が１つだけの項を「**１次の項**」という。
1次の項だけか、1次の項と数だけの項からできている式を「**一次式**」という。

![](/images/books/book-ue5_mathematical_programming/chap_03_calculation_of_a_linear_expression/2022-08-06-10-34-47.png)

#### 同類項

図の3xと2xのように文字の部分が同じ項は「**同類項**」という。

![](/images/books/book-ue5_mathematical_programming/chap_03_calculation_of_a_linear_expression/2022-08-06-10-57-29.png)

#### 項をまとめる

文字の項、数の項どうしをまとめる。

![](/images/books/book-ue5_mathematical_programming/chap_03_calculation_of_a_linear_expression/2022-08-06-11-08-31.png)

#### （）内の符号を変える

以下のような式の際に（）の符号を変更する

$$
 3x - (4x - 3)
$$

カッコ内の符号は反転する。

$$
 3x - 4x + 3
$$

#### 縦書きの計算

1次式は縦書きの計算もできる。

![](/images/books/book-ue5_mathematical_programming/chap_03_calculation_of_a_linear_expression/2022-08-06-11-13-46.png)

#### 乗法の交換法則

aとbをかける時に、aとbを入れ替えても積は同じになる。

$$
a \times b = b \times a
$$

プログラムでも積は同じになる。

![](/images/books/book-ue5_mathematical_programming/chap_03_calculation_of_a_linear_expression/2022-08-06-11-44-17.png)

#### 乗法の結合法則

a,bとcをかける時、aとｂをかけた後にcをかけた積と、bとcを書けた後にaをかけた積は同じになる。

$$
(a \times b) \times c = a \times (b \times c)
$$

プログラムでも積は同じになる。

![](/images/books/book-ue5_mathematical_programming/chap_03_calculation_of_a_linear_expression/2022-08-06-11-47-19.png)

Blueprintであれば、AddPinでInputピンを増やして接続することができる。

![](/images/books/book-ue5_mathematical_programming/chap_03_calculation_of_a_linear_expression/2022-08-06-11-48-46.png)

#### 分配法則

カッコの外の数値をカッコ内のすべての項にかける。

![](/images/books/book-ue5_mathematical_programming/chap_03_calculation_of_a_linear_expression/2022-08-06-11-40-03.png)

### 1次式の計算の利用
### 関係を表す式

## UnrealEngine知識

## BP & C++


### 関連ページ

すでに書いた内容で関連するページです。

https://zenn.dev/posita33/books/ue5_starter_cpp_and_bp_001/viewer/chap_02_bp-variable

https://zenn.dev/posita33/books/ue5_starter_cpp_and_bp_001/viewer/chap_02_cpp-variable
