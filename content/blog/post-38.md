---
title: "Pythonで使えるGraphQLのライブラリを調査した"
date: 2021-08-13T13:10:00Z
draft: false

# author's github account name
author:
 - "Kawaken555"

# post thumb
image: "images/post/post-38/post-38.png"

# meta description
description: ""

# taxonomies
categories: 
  - "Python"
tags:
  - "GraphQL"
  - ""

# post type
type: "post"
---

### 経緯   

前から気になっていたGraphQLを使ってみたかったことが始まりです。        

今手元にはチュートリアルが終わって完成した FastAPI + SQLAlchemy 環境があるので、     

今回はその環境を使う前提で、クライアントサイドで使うPython ライブラリを調査します。     

因みに Python は 3.9 を使用しています。



### 調査内容   

GraphQLの公式サイトを見てみると  

[こちら](https://graphql.org/code/#python)にPythonで使用できるライブラリが列挙されています。    

githubのスター数で並んでおり、上位3位は以下の3つです。



* graphene(グラフェン)
* ariadne(アリアドネ)
* strawberry





#### ■ graphene

* MIT License
* 27日前に最新リリース(調査時点)
* star 6.7k    
* Python 3.7 までサポート
* SQL (Django, SQLAlchemy), NoSQL, custom Python objectsなどのデータソースをサポート   



github:  https://github.com/graphql-python/graphene  

pip:   https://pypi.org/project/graphene/  

公式: https://graphene-python.org/  



#### ■ ariadne

* BSD-3-Clause License
* 5ヶ月前に最新リリース(調査時点)
* star 1.5k    
* Python 3.9 までサポート
* スキーマファーストという、GraphQLコミュニティで広く使用されている書き方ができる



github:  https://github.com/mirumee/ariadne  

pip:   https://pypi.org/project/ariadne/  

公式: https://ariadnegraphql.org/ 



#### 



#### ■ Strawberry

* MIT License
* 2日前に最新リリース(調査時点)
* star 1.1k    
* Python 3.9 までサポート
* スキーマファースト
* dataclasses(Python 3.7 の機能？)にインスパイアされたライブラリ   
* Python の型ヒントを使用した書式なので書きやすそう     
* 初期開発のため急な変更があるかもしれない([公式に文言](https://strawberry.rocks/docs/general/why#why-should-you-use-strawberry))





github:  https://github.com/strawberry-graphql/strawberry  

pip:   https://pypi.org/project/strawberry-graphql/  

公式: https://strawberry.rocks/   





### 結論みたいなもの     

SQLAlchemy をサポートしていると名言している点と、

最も使われており情報が多いという点で graphene を選択してしまいました。   

してしまいました、というのも現時点で graphene は Python 3.7 までのサポートとなっており、   

今私が使っている Python 3.9 をサポートしていないライブラリなんですよね。。。

調査時点ではそれを失念して選んでしまいました。。。



とりあえず graphene で実装してみて動いたのですが、   

ちょっと今後 ariadne や strawberry への変更が必要かもしれません。     

