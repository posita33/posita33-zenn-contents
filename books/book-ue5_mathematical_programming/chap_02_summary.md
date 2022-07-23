---
title: "📕1章 正の数・負の数 まとめ📕"
free: false
---

# 1章 正の数・負の数 まとめ

## 数学的知識

### 正の数・負の数

#### 正の数・負の数と符号

正の数か負の数かは原点位置を基準に考えます。
左側を「負の数」、右側を「正の数」

![](/images/books/book-ue5_mathematical_programming/chap_02_positive_and_negative_numbers/2022-07-09-19-07-48.png)

Unreal Engineでは正の数の符号は省略されますが、正の数は「+」、負の数は「-」を付けて表します。

![](/images/books/book-ue5_mathematical_programming/chap_02_positive_and_negative_numbers/2022-07-09-21-58-59.png)

#### 絶対値

「青」と「赤」の場所は違いますが、距離は原点から離れている距離は同じです。
「絶対値はいくつか？」と問われた時に、**絶対値**は「400」になります。

![](/images/books/book-ue5_mathematical_programming/chap_02_positive_and_negative_numbers/2022-07-09-22-05-33.png)

## 正の数・負の数の大小

![](/images/books/book-ue5_mathematical_programming/chap_02_positive_and_negative_numbers/2022-07-09-22-28-09.png)

画像の数値を大小の不等号を使って表します。

$$
-400 < -200 < 100 < 400
$$

不等号は数の大小を表す記号です。
不等号の向きは整えます。
なので、逆向きに書くこともできます。

$$
400 > 100 > -200 > -400
$$

---

### 四則

加法、減法、乗法、除法をまとめて**四則**という。

| 算数   | 数学 | 記号 | 検索英語 | 結果 |
| ------ | ---- | ---- | -------- | ---- |
| たし算 | 加法 | +    | Add      | 和   |
| ひき算 | 減算 | -    | Subtract | 差   |
| かけ算 | 乗算 | ×    | Multiply | 積   |
| わり算 | 除算 | ÷    | Divide   | 商   |

---

### 加法と減法

#### 同符号と異符号

同符号のケース

$$
(+5) + (+8) または(-5) + (-8)
$$

異符号のケース

$$
(+3) + (-8) または (-3) + (+8)
$$

#### かっこの外し方

$$
+(+1) = +1
$$

$$
+(-1) = -1
$$

$$
-(+1) = -1
$$

$$
-(-1) = +1
$$

#### 加法の交換法則

たす数とたされる数を入れ替えても和は同じになる。

$$
a + b = b + a
$$

#### 加法の結合法則

()で括った方が計算順序は早くなるが、加法だけの場合はどの順番で計算しても和は同じになる。

$$
(a + b) + c = a + (b + c)
$$

---

### 乗法と除法

#### 乗法の符号

$$
(+) \times (+) = +
$$

$$
(-) \times (-) = +
$$

$$
(+) \times (-) = -
$$

$$
(-) \times (+) = -
$$

#### 0との積

0をかけると積は0になります。

$$
  a \times 0 = 0
$$

$$
  0 \times a \times b = 0
$$

#### 累乗

同じ数をいくつかかけたものを「**累乗**」という。かけあわせた個数を示す右肩の数字を「**指数**」という。

$$
3 \times 3 = 3^2
$$

---

### 四則の混じった計算

#### 四則の計算順序

計算の順番は「カッコの中・累乗」 -> 「乗除」 -> 「加減」の順番に計算する。

#### 分配法則

$$
  (a + b) \times c = ac + bc 
$$

$$
  \Bigl( \frac{3}{4} - \frac{2}{3} \Bigl) \times 12
$$

$$
  = \frac{3}{4} \times 12 - \frac{2}{3} \times 12
$$

$$
  = 3 \times 3 - 2 \times 4
$$

$$
  = 9 - 8
$$

$$
  = 1
$$

---

### 正の数・負の数の利用

#### 平均

何個かの数の合計から等しくなるようにした数を**平均**という。

$$
（平均）= (合計) \div (個数)
$$

#### 逆数

2つの数の積が1になる場合、一方の数を他方の数の**逆数**という。

$$
  \frac{1}{3} \times 3 = 1
$$

$$
3の逆数は\frac{1}{3} 、 \frac{1}{3}の逆数は3
$$

#### 分数と少数の除法

$$
  \frac{2}{5} \times 0.5 \div \frac{1}{10}
$$

$$
  = \frac{2}{5} \times \frac{5}{10} \times \frac{10}{1}
$$

$$
  = 2
$$

$$
0.5は \frac{5}{10}  、 \div \frac{1}{10} は \times \frac{10}{1}に直して計算を行う
$$

---

## UnrealEngine知識

### 原点と3軸

Viewportに配置したActorを選択するとマニピュレータが表示されます。
色は軸（X,Y,Z）の種類を表し、矢印の向きで±が分かるようになっています。
X,Y,Zが全て0.0に設定されている位置が**原点**になります。

![](/images/books/book-ue5_mathematical_programming/chap_02_positive_and_negative_numbers/2022-07-09-18-55-58.png)

### ActorのLocation値について

Actorを矢印側に移動するとLocationの値がプラスされます。

![](/images/books/book-ue5_mathematical_programming/chap_02_positive_and_negative_numbers/2022-07-09-19-14-08.png)

Actorを矢印の反対側に移動するとLocationの値がマイナスされます。
原点より左になると数値に負の数を表す符号の「-」が付きます。

![](/images/books/book-ue5_mathematical_programming/chap_02_positive_and_negative_numbers/2022-07-09-19-16-44.png)

### Unreal Engineの単位

Unreal Engineの単位はuu（Unreal Unit）が使われます。
1uuは1cmです。
「Actorを配置」から追加できるCubeは100uuの立方体です。
画像のLocationは「Y:100.0」が設定されているので原点から「100uu = 100cm = 1m」離れています。

![](/images/books/book-ue5_mathematical_programming/chap_02_positive_and_negative_numbers/2022-07-09-21-42-06.png)

---

## BP & CP

### プログラムの四則演算

| 数学 | 記号 | BP検索英語 | BP                                                                                           | C++ |
| ---- | ---- | ---------- | -------------------------------------------------------------------------------------------- | --- |
| 加法 | +    | Add        | ![](/images/books/book-ue5_mathematical_programming/chap_02_summary/2022-07-23-10-17-07.png) | +   |
| 減算 | -    | Subtract   | ![](/images/books/book-ue5_mathematical_programming/chap_02_summary/2022-07-23-10-20-10.png) | -   |
| 乗算 | ×    | Multiply   | ![](/images/books/book-ue5_mathematical_programming/chap_02_summary/2022-07-23-10-20-41.png) | *   |
| 除算 | ÷    | Divide     | ![](/images/books/book-ue5_mathematical_programming/chap_02_summary/2022-07-23-10-21-18.png) | /   |

### 加法と減法

$$
(+2) + (+5)
$$

$$
(+4) - (-5)
$$

$$
(+6) - (+8) + (-7) - (-4)
$$

![](/images/books/book-ue5_mathematical_programming/chap_02_summary/2022-07-23-10-27-26.png)

```cpp
	int answer = 0;
	
	answer = (+2) + (+5);

	answer = (+4) - (-5);

	answer = (-6) - (+8) + (-7) - (-4);
```

### 乗法と除法

$$
(+4) \times (-8)
$$

$$
(+3) \times (-6) \times (-5)
$$


$$
  (-8) \div (+2)
$$

$$
  (- \frac{4}{5}) \div (+1.6) \div (-\frac{3}{10}) \times (-0.5)
$$

![](/images/books/book-ue5_mathematical_programming/chap_02_summary/2022-07-23-10-42-53.png)


### 累乗

$$
(-3^2) \times (-5)^2
$$

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_summary/2022-07-23-10-44-49.png)

```cpp
	float answerf = -(FMath::Pow(3.0f, 2.0f)) * FMath::Pow(-5.0f, 2.0f);
```

### 絶対値

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_summary/2022-07-23-11-00-16.png)

```cpp
    float ansewerF = FMath::Abs(400.0f);
```

### 四則の混じった計算

$$
  (+3.6) - \{(-3)^2 - 4 \times (0.2 - 1.6) \}
$$

$$
  \Bigl( \frac{3}{4} - \frac{2}{3} \Bigl) \div \frac{6}{8} - \Bigl(\frac{6}{4} + \frac{1}{3} \Bigl) \times 36
$$

![](/images/books/ue5_starter_cpp_and_bp_001/chap_02_summary/2022-07-23-11-03-34.png)

```cpp
	// (+3.6)−{(−3)^2 −4×(0.2−1.6)}
	answerF = (+3.6f) - (FMath::Pow(-3.0f, 2.0f) - 4.0f * (0.2f - 1.6f));

	// (3/4 - 2/3)÷6/8 - (6/4 + 1/3) × 36
	answerF = (3.0f/4.0f - 2.0f/3.0f) / (6.0f/8.0f) - (6.0f/4.0f + 1.0f/3.0f) * 36.0f;
```
