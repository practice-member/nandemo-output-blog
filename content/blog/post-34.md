---
title: "Python用のlinterを検討してみた"
date: 2021-08-01T14:10:44Z
draft: false

# author's github account name
author:
 - "greenwakame"

# post thumb
image: "images/post/post-12/python-logo.png"

# meta description
description: ""

# taxonomies
categories: 
  - "python"
tags:
  - "python"
  - "linter"
  - "vscode"

# post type
type: "post"
---

### 「lint/linter」とは
「lint」とは、プログラムなどのソースコードを読み込んで内容を分析し、  
問題点を指摘してくれる静的解析ツール。  
ツールのことを指す場合は「linter」呼ばれている。

### 「PEP」とは
「[PEP](https://www.python.org/dev/peps/)」とは、
pythonコミュニティに対して情報や新機能・プロセス・環境設定などを説明する文書の集合体です。  
コードの一貫性など詳しく規約が定められているようですので、  
開発する前に一読しておいたほうが良いと思われます。

### よく見かけるlinterの紹介

### pycodestyle(pep8)
「[pep8](https://pypi.org/project/pep8/)」というワードをよく見かけますが、  
現在は「[pycodestyle](https://pypi.org/project/pycodestyle/)」に変更されているようで、  
先程紹介したpythonコミニティのガイドラインに基づいた「linter」のようです。

### pylint
Visual Studio for Python プロジェクトにはデフォルトで、  
「[pylint](https://www.pylint.org/)」が導入されています。  
PythonスタイルガイドであるPEP 8が推奨するスタイルに従がっているようです。  
Visual Studioで開発する場合は、まずこれを試すのが簡単そうでした。

### pyflakes/flake8
「[pyflakes](https://pypi.org/project/pyflakes/)」は単品として利用しているよりも、  
「[pycodestyle](https://pypi.org/project/pycodestyle/)」と統合してしている「[flake8](https://pypi.org/project/flake8/)」を利用することが多いようです。  
ソースコードの解析は「[pyflakes](https://pypi.org/project/pyflakes/)」が、  
ソースコードのスタイルチェックは「[pycodestyle](https://pypi.org/project/pycodestyle/)」が行い、  
結果はまとめて表示されます。

### PEP以外のチェックスタイル

### Google Python Style Guide
基本的には、「pycodestyle」と同じガイドラインに基づいているようですが、  
「[Google Python Style Guide](https://google.github.io/styleguide/pyguide.html)」では追加でチェックしているスタイルがあるようです。  
差異は少し調べてみましたが、公式では差異の抜粋などはありませんでしたので、  
調査が必要だと思われます。

### まとめ
VSCodeで開発する場合は、[設定方法](https://code.visualstudio.com/docs/python/linting)が紹介されていますので、  
特に理由などない場合は、有効設定するだけで利用できる「linter」から選択するのが便利かもしれません。  
現状の開発環境では、ソースコードの解析を保存時に自動で実施し、  
スタイルチェックも合わせて確認するのは当たり前になっています。  
もし開発ルール的に許容されるなら、コード整形も合わせて実施しておくと、  
のちのち助かることもあるかもしれません。
