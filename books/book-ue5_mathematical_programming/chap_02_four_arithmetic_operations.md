---
title: "四則の混じった計算"
free: false
---


## 問題

(1) 

$$
  (-8) \times (+4) - (+27) \div (-3)
$$

(2)

$$
  (+3.6) - \{(-3)^2 - 4 \times (0.2 - 1.6) \}
$$

(3)

$$
  \Bigl( \frac{3}{4} - \frac{2}{3} \Bigl) \div \frac{6}{8} - \Bigl(\frac{6}{4} + \frac{1}{3} \Bigl) \times 36
$$

## 四則

### 四則とは

加法、減法、乗法、除法をまとめて**四則**という。

計算の順番は「カッコの中・累乗」 -> 「乗除」 -> 「加減」の順番に計算する。

### 分配法則

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


### 問題の解答


(1) 

$$
  (-8) \times (+4) - (+27) \div (-3)
$$

$$
  = (-32) - (-9)
$$

$$
  = (-32) + (+9)
$$

$$
  = -23
$$


(2)

$$
  (+3.6) - \{(-3)^2 - 4 \times (0.2 - 1.6) \}
$$

$$
 = (+3.6) - \{(+9) - 4 \times (- 1.4) \}
$$

$$
 = (+3.6) - \{(+9) - (-5.6) \}
$$

$$
 = (+3.6) - (+14.6)
$$

$$
 = -11
$$


(3)

$$
  \Bigl( \frac{3}{4} - \frac{2}{3} \Bigl) \div \frac{6}{8} - \Bigl(\frac{6}{4} + \frac{1}{3} \Bigl) \times 36
$$

$$
  = \Bigl( \frac{9}{12} - \frac{8}{12} \Bigl) \times \frac{8}{6} - \Bigl(\frac{18}{12} + \frac{4}{12} \Bigl) \times 36
$$

$$
  = \Bigl( \frac{1}{12} \Bigl) \times \frac{8}{6} - \Bigl(\frac{22}{12} \Bigl) \times 36
$$

$$
  = \frac{1}{6} - 66
$$

$$
  = - 65 \frac{5}{6} 
$$


## BPで数式を表現

![](/images/books/book-ue5_mathematical_programming/chap_02_four_arithmetic_operations/2022-07-18-12-06-44.png)

## C++で数式を表現

```cpp
	float answerF = 0.0f;

	// (1) (−8)×(+4)−(+27)÷(−3)
	answerF = (-8.0f) * (+4.0f) - (27.0f) / (-3.0f);

	// (2) (+3.6)−{(−3)^2 −4×(0.2−1.6)}
	answerF = (+3.6f) - (FMath::Pow(-3.0f, 2.0f) - 4.0f * (0.2f - 1.6f));

	// (3) (3/4 - 2/3)÷6/8 - (6/4 + 1/3) × 36
	answerF = (3.0f/4.0f - 2.0f/3.0f) / (6.0f/8.0f) - (6.0f/4.0f + 1.0f/3.0f) * 36.0f;
```