---
title: "ZennでよくつかうMarkdown記法のSnippetを登録する"
emoji: "📑"
type: "idea" # tech: 技術記事 / idea: アイデア
topics: ["zenn", "vscode", "markdown"]
published: true
---

## Snippetを登録する
ZennのBookや記事を見ていると、見たことが無いMarkdown表示があります。
使い方は分かったけど、入力するのが面倒くさい。
単語のショートカットをしたいので、Snippetを登録することにしました。


**メッセージブロック**を表示するMarkdown記法
```
:::message
メッセージをここに
:::
```
:::message
メッセージをここに
:::

**message**の入力を`mzenn`を入力すれば、変換対象となるSnippetを登録します。

[ファイル]メニューからユーザースニペットを開きます。
![](/images/articles/zenn_markdown_snippet/2022-01-18-15-22-38.png)
*ファイル > ユーザー設定 > ユーザースニペット*

`markdown.json`を選択します。
![](/images/articles/zenn_markdown_snippet/2022-01-18-15-24-50.png)
*markdownで検索 > markdown.json*


```json:markdown.json
{
	"Markdown Zenn Message": {
		"prefix": "mzenn",
	 	"body": [
	 		":::message",
			"メッセージをここに" ,
	 		":::"
	 	],
	 	"description": "Zenn Original : Messge Block"
	}
}

```

prefixに設定した`mzenn`を入力し、`Ctrl + Space`を入力すると、Snippetに登録したbodyとdescriptionが表示されます。
リストから`mzenn`を選択すると、Messageブロックが入力されます。

![](/images/articles/zenn_markdown_snippet/2022-01-18-15-36-27.png)

![](/images/articles/zenn_markdown_snippet/2022-01-18-15-38-24.png)

:::message
メッセージをここに
:::

## 他のZennオリジナル記法やよく使う記法を追加する。

### 登録したPrefixとmarkdown.json
Zennオリジナル記法以外にもよく使う記法を登録しました。
| Prefix | 概要                                |
|--------|-----------------------------------|
| mzenn  | ZennのオリジナルMarkdown記法              |
| mmath  | 数式                                |
| mimage | 画像挿入のMarkdown(UnrealEngineだとよく使う) |


```json:markdown.json
{
	// Place your snippets for markdown here. Each snippet is defined under a snippet name and has a prefix, body and 
	// description. The prefix is what is used to trigger the snippet and the body will be expanded and inserted. Possible variables are:
	// $1, $2 for tab stops, $0 for the final cursor position, and ${1:label}, ${2:another} for placeholders. Placeholders with the 
	// same ids are connected.
	// Example:
	// "Print to console": {
	// 	"prefix": "log",
	// 	"body": [
	// 		"console.log('$1');",
	// 		"$2"
	// 	],
	// 	"description": "Log output to console"
	// }

	"Markdown Zenn Message": {
		"prefix": "mzenn",
	 	"body": [
	 		":::message",
			"メッセージをここに" ,
	 		":::"
	 	],
	 	"description": "Zenn Original : Messge Block"
	},

	"Markdown Zenn Message Alert": {
		"prefix": "mzenn",
	 	"body": [
	 		":::message alert",
			"警告メッセージをここに" ,
	 		":::"
	 	],
	 	"description": "Zenn Original : Messge Alert Block"
	},

	"Markdown Zenn Toggle": {
		"prefix": "mzenn",
	 	"body": [
	 		":::details タイトル",
			"表示したい内容" ,
	 		":::"
	 	],
	 	"description": "Zenn Original : Toggle"
	},

	"Markdown Code cpp": {
		"prefix": "mcode",
	 	"body": [
	 		"```cpp:.cpp",
			"" ,
	 		"```"
	 	],
	 	"description": "code block : .cpp"
	},

	"Markdown Code header": {
		"prefix": "mcode",
	 	"body": [
	 		"```h:.h",
			"" ,
	 		"```"
	 	],
	 	"description": "code block : .h"
	},

	"Markdown Zenn Math": {
		"prefix": "mmath",
	 	"body": [
	 		"$$",
			"A + B" ,
	 		"$$"
	 	],
	 	"description": "Zenn Original : Math"
	},

	"Markdown Image Basic": {
		"prefix": "mimage",
	 	"body": [
	 		"![Alt](Image Path)",
	 	],
	 	"description": "Image Basick"
	},

	"Markdown Image width": {
		"prefix": "mimage",
	 	"body": [
	 		"![Alt](Image Path =250px)",
	 	],
	 	"description": "Image Width"
	},

	"Markdown Image caption": {
		"prefix": "mimage",
	 	"body": [
	 		"![Alt](Image Path)",
	 		"*caption*",
	 	],
	 	"description": "Image with caption"
	}
}
```

### Zenn独自(mzenn)

prefixの文字列は重複するとリスト化します。
![](/images/articles/zenn_markdown_snippet/2022-01-18-15-49-25.png)


警告ありのメッセージ

:::message alert
警告メッセージをここに
:::

折りたたむことが出来るアコーディオン
:::details タイトル
表示したい内容
:::

### ソースコード(mcode)
ソースコードもよく使うので、C++の.Cppと.hを追加しました。
```cpp:.cpp
int A = 10;
```

よく使用する言語があるか確認して追加します。
[📄 対応言語の一覧 →](https://prismjs.com/#supported-languages)


### 数式(mmath)
数式を表示出来るMarkdown記法

$$
A + B
$$

>Zenn ではKaTeXによる数式表示に対応しています。
KaTeXのバージョンは常に最新バージョンを使用します。
>
>[📄 KaTeXがサポートする記法の一覧 →](https://katex.org/docs/support_table.html)

### 画像挿入
Unreal Engineだとスクリーンショットをよく使うのでimage挿入のsnippetです。

| Type     | Markdown                         |
|----------|----------------------------------|
| 通常       | ![Alt](Image Path)               |
| 幅指定      | ![Alt](Image Path =250px)        |
| キャプションあり | ![Alt](Image Path)<br/>\*caption\* |


## 参照URL

https://qiita.com/12345/items/97ba616d530b4f692c97

https://coffee-nominagara.com/2019-01-25-094628

https://zenn.dev/miz_dev/articles/157a7aaad0bdcf
