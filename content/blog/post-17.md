---
title: "FastAPIを調べました"
date: 2021-02-06T08:30:52Z
draft: false

# author's github account name
author: daisukesasaki787
 - ""

# post thumb
image: "images/post/post-1.jpg"

# meta description
description: "FastAPI調査"

# taxonomies
categories: 
  - "Python"
tags:
  - "Python"
  - ""

# post type
type: "post"
---
# FastAPIとはなにか
Pythonのフレームワークの一種です。  
Pythonの代表的なフレームワークに下記があります。 
   
Django: フルスタックフレームワーク  
Flask: マイクロフレームワーク  

FastAPIはFlaskと同じマイクロフレームワークになります。  
  
### FastAPIの機能について  
公式のリファレンスをみて気になった機能に自動ドキュメント生成について記載があった。以下抜粋。  
> Standards-based: API のオープンスタンダードに基づいており、完全に互換性があります: OpenAPI (以前は Swagger として知られていました) や JSON スキーマ.  

### Swaggerとはなにか  
SwaggerはRESTFul APIを構築するためのオープンソースのフレームワーク。  
「Open API Initative」という団体がRESTful APIのインターフェースの記述をするための標準フォーマットを推進しています。  
その標準フォーマットがSwaggerです。  
  
この自動ドキュメント生成機能でSwagger(ドキュメント)が生成されるのでSwagger UIで直接APIを呼び出しテストが実行できます。  
  
公式リファレンスに記載で気になった記載に下記があります。   
> FastAPI は巨人の肩の上に立っています。  
>  
> Web の部分はStarlette  
> データの部分はPydantic  
   
### Starletteとは  
StarletteはASGI Framework/toolkitの一つです。  
下記のような特徴をもちます。  
   
 ・WebSocketのサポート  
 ・GraphQLのサポート  
 ・プロセス内バックグラウンドタスク  
 ・起動およびシャットダウンイベント  
 ・requestsに基づいて構築されたテストクライアント  
 ・CORS、GZip、静的ファイル、ストリーミング応答  
 ・セッションとCokieのサポート  
 ・テストカバレッジ100%  
 ・型アノテーション100%のコードベース   
  
### Pydanticとは   
PydanticはPythonのヒントを利用してData validation/serializationを行うライブラリです。   
データベースのためにORMsや、ODMsなどの、Pydanticに基づく外部ライブラリを備えています。  
これは、すべてが自動的に検証されるため、多くの場合、リクエストから取得したオブジェクトをデータベースに直接渡すことができるということを意味しています。   
  
FastAPIは上記の技術体をベースに作られているので(完全互換性あり)「巨人の肩の上に立っています」と表記されているみたいです。  
 
以上FastAPIを調べて気になった個所を抜粋してみました。
