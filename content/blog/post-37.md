---
title: " Pythonのソースの自動整形について"
date: 2021-08-01T14:10:54Z
draft: false

# author's github account name
author:
 - "daisukesasaki787"

# post thumb
image: "images/post/post-37/python-logo.png"

# meta description
description: ""

# taxonomies
categories: 
  - "python"
tags:
  - "python"
  - "yapf"
  - "black"

# post type
type: "post"
---

コーディングをする際のソースの自動整形について調べました。

### yapf
１つ目は yapf になります。
google社が作成しています

https://github.com/google/yapf

ちなみにyapfはYet Another Python Formatterの略だそうです。

動作条件は下記の通りで

Python 2.7

Python 3.6.4以降

Python 2.7でyapfを動かすならば、Python 2系のソースのみが整形の対象です。

同じように、Python 3系でyapfを動かすなら、Python 3系のソースのみが整形の対象となります。

.style.yapf というファイルを作成するとオプションの指定をファイルに記載することができます。

高いカスタマイズ性が特徴です。


### black
２つ目は black になります。

Python 3.6.0 以上に対応しています。

PEP8 に準拠しています。

こちらはyapfに比べてカスタマイズ性が低いです。

変更できるのは一行あたりの文字数だけになります。

### まとめ
今回はPythonの代表的な2つの自動整形ツールを調べてみました。

特にこだわりがないのであればblackを使用、柔軟に対応したいのであればyapfを使用するといった使い分けができます。

個人的にはblackを使用して面倒な設定は行わないようにしたいなと思いました。


