---
title: "正の数・負の数"
free: false
---

## 原点と3軸

Viewportに配置したActorを選択するとマニピュレータが表示されます。
色は軸（X,Y,Z）の種類を表し、矢印の向きで±が分かるようになっています。
X,Y,Zが全て0.0に設定されている位置が**原点**になります。

![](/images/books/book-ue5_mathematical_programming/chap_02_positive_and_negative_numbers/2022-07-09-18-55-58.png)

## 正の数・負の数と符号

正の数か負の数かは原点位置を基準に考えます。
3D空間なのでカメラの位置によって左か右かは変わってしまいます。
この本では左側を「負の数」、右側を「正の数」とします。

![](/images/books/book-ue5_mathematical_programming/chap_02_positive_and_negative_numbers/2022-07-09-19-07-48.png)

Actorを矢印側に移動するとLocationの値がプラスされます。

![](/images/books/book-ue5_mathematical_programming/chap_02_positive_and_negative_numbers/2022-07-09-19-14-08.png)

Actorを矢印の反対側に移動するとLocationの値がマイナスされます。
原点より左になると数値に負の数を表す符号の「-」が付きます。

![](/images/books/book-ue5_mathematical_programming/chap_02_positive_and_negative_numbers/2022-07-09-19-16-44.png)

Unreal Engineでは正の数の符号は省略されますが、正の数は「+」を付けて表します。

![](/images/books/book-ue5_mathematical_programming/chap_02_positive_and_negative_numbers/2022-07-09-21-58-59.png)

## Unreal Engineの単位

Unreal Engineの単位はuu（Unreal Unit）が使われます。
1uuは1cmです。
「Actorを配置」から追加できるCubeは100uuの立方体です。
画像のLocationは「Y:100.0」が設定されているので原点から「100uu = 100cm = 1m」離れています。

![](/images/books/book-ue5_mathematical_programming/chap_02_positive_and_negative_numbers/2022-07-09-21-42-06.png)

## 配置してみよう

「青」、「赤」のSphereを表示されている文字の位置に配置してみましょう。

![](/images/books/book-ue5_mathematical_programming/chap_02_positive_and_negative_numbers/2022-07-09-21-48-25.png)

「青」は原点より左側、「赤」は原点より右側になります。

![](/images/books/book-ue5_mathematical_programming/chap_02_positive_and_negative_numbers/2022-07-09-18-46-55.png)

## 絶対値

「青」と「赤」の場所は違いますが、距離は原点から離れている距離は同じです。
「絶対値はいくつか？」と問われた時に、**絶対値**は「400」になります。

![](/images/books/book-ue5_mathematical_programming/chap_02_positive_and_negative_numbers/2022-07-09-22-05-33.png)

Print Stringで位置と絶対値を表示してみます。

![](/images/books/book-ue5_mathematical_programming/chap_02_positive_and_negative_numbers/2022-07-09-22-17-21.png)

位置と絶対値をPrintStringで出力するBlueprint。

![](/images/books/book-ue5_mathematical_programming/chap_02_positive_and_negative_numbers/2022-07-09-22-18-23.png)


C++で絶対値を取得するにはFMath::Abs()を使用します。
AbsはAbsolute（絶対値）の略称です。

```cpp
	float abs = FMath::Abs(400.0f);
```

## 正の数・負の数の大小

「緑」を-2m(-200uu)、「黄色」を1m(100uu)の位置に配置します。

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

