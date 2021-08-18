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



### スキーマファーストとコードファースト

GraphQL のライブラリを調べていくと、  

「スキーマファースト」と「コードファースト」という言葉をよく目にしました。     

「スキーマファースト」は、GraphQL SDLという言語でスキーマを定義します。      

バックエンドの言語やフレームワークに縛られない実装ができますが、  

SDL は言語機能的に貧弱なようで要件によっては物足りなくなるかもしれません。    



一方「コードファースト」は、バックエンドの実装言語でスキーマを定義します。    

SDL よりも柔軟な実装ができる一方で、バックエンドの言語に縛られてしまうデメリットがあります。       



ライフサイクルが長いシステムの場合や、APIサーバーを多数用意しなくてはならない大規模なシステムではスキーマファーストのほうが良いのかもしれないと思いました。            

個人開発ではコードファーストのほうが、ORマッパーとの連携がしやすかったりと手軽で使い勝手が良さそうです。     



### 洗い出したライブラリの候補   

GraphQLの公式サイトを見てみると  

[こちら](https://graphql.org/code/#python)にPythonで使用できるライブラリが列挙されています。    

githubのスター数で並んでおり、上位3位は以下の3つです。



* Graphene(グラフェン)
* Ariadne(アリアドネ)
* Strawberry



#### ■ Graphene

* MIT License
* 27日前に最新リリース(調査時点)
* コードファースト
* star 6.7k    
* Python 3.7 までサポート
* SQL (Django, SQLAlchemy), NoSQL, custom Python objectsなどのデータソースをサポート   
* 利用者が多く情報量が多いが、[ここ](https://github.com/graphql-python/graphql-core#integration-with-other-libraries-and-roadmap) を読むと他の2つに比べてPython のエコシステムの変化についていけていない、とまでは言わないまでも遅れてそう。Phthon 3.7 までしかサポートしてないのはそのせい？     



github:  https://github.com/graphql-python/graphene  

pip:   https://pypi.org/project/graphene/  

公式: https://graphene-python.org/  



#### ■ Ariadne

* BSD-3-Clause License
* 5ヶ月前に最新リリース(調査時点)
* スキーマファースト
* star 1.5k    
* Python 3.9 までサポート
* 良いという評判もあまりないしかと言って悪いとも聞かない。スキーマファーストのライブラリを選ぶならこれかも。  



github:  https://github.com/mirumee/ariadne  

pip:   https://pypi.org/project/ariadne/  

公式: https://ariadnegraphql.org/ 





#### ■ Strawberry

* MIT License

* 2日前に最新リリース(調査時点)

* コードファースト

* star 1.1k    

* Python 3.9 までサポート

* dataclasses(Python 3.7 の機能？)にインスパイアされたライブラリ   

* Grapheneよりももっとコードファースト

* Python の型ヒントを使用した書式なので書きやすそう     

  ※ 他のライブラリが型を指定するのに「 String 」と書かないと行けないところを Strawberry では「 str 」とPython っぽく書けそう

* 初期開発のため急な変更があるかもしれない([公式に文言](https://strawberry.rocks/docs/general/why#why-should-you-use-strawberry))





github:  https://github.com/strawberry-graphql/strawberry  

pip:   https://pypi.org/project/strawberry-graphql/  

公式: https://strawberry.rocks/   





### 結論みたいなもの     

SQLAlchemy をサポートしていると名言している点と、

最も使われており情報が多いという点で Graphene を選択してしまいました。   

してしまいました、というのも現時点で Graphene は Python 3.7 までのサポートとなっており、   

今私が使っている Python 3.9 をサポートしていないライブラリなんですよね。。。

調査時点ではそれを失念して選んでしまいました。。。



とりあえず Graphene で実装してみて動いたのですが、    

ちょっと今後 Ariadne や Strawberry への変更が必要かもしれません。     



大きな変更が入る可能性がある Strawberry よりも Ariadne ですかね。      





