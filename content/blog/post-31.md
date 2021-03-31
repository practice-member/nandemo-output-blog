---
title: "「OpenAPI Generator Tool」について調べてみた"
date: 2021-02-28T13:13:40Z
draft: false

# author's github account name
author:
 - "greenwakame"

# post thumb
image: "images/post/post-31/OpenAPI_Logo_Pantone.png"

# meta description
description: ""

# taxonomies
categories: 
  - "survey"
tags:
  - "openapi"
  - "generator"

# post type
type: "post"
---

### 「OpenAPI Generator Tool」とは
[OpenAPI Specification](https://github.com/OAI/OpenAPI-Specification/blob/master/versions/3.0.0.md)形式で記述されたYAMLやJSONのファイルをもとに、  
コード生成してくれるツールのことです。

### 「OpenAPI Specification形式」とは
REST APIの記述フォーマットのことです。  
* 使用可能なエンドポイント(/○○○)と各エンドポイントでの操作(CRUD)
* 操作パラメータ各操作の入力と出力
* 認証方法
* 連絡先情報、ライセンス、利用規約およびその他の情報。  
  
詳しい仕様は[公式](https://github.com/OAI/OpenAPI-Specification/blob/master/versions/3.0.0.md)を参照してください。

### 「OpenAPI仕様」で開発されているツールの紹介

### 公式

#### 「Swagger」
![Swagger](../../images/post/post-31/swagger_icon.png)  
* [Swagger Editor](https://editor.swagger.io/) API仕様を書くためのエディタ
* [Swagger UI](https://swagger.io/tools/swagger-ui/) ドキュメントを生成するツール
* [Swagger Codegen](https://swagger.io/tools/swagger-codegen/) コードを生成するツール

### サードパーティ

#### GUI Editor 「Stoplight Studio」
![Stoplight Studio](../../images/post/post-31/stoplight_studio.jpg)  
先程紹介した「[Swagger Editor](https://editor.swagger.io/)」の場合、
YAMLファイルを触っていくのですが、  
「[Stoplight Studio](https://stoplight.io/studio/)」の場合は、  
直感的にGUI操作で記述することが出来ます。

* OpenAPI v2/v3対応
* 無料
* 「Prism」が統合されている
* Lintを利用してリアルタイムでエラーチェックできる

### モックサーバ 「Prism」
![Prism](../../images/post/post-31/readme-header.svg)  
「[Prism](https://stoplight.io/open-source/prism)」は、ターミナルからOpenAPI Specification形式で記述されたファイルを、  
読み込むことで簡単にAPIのモックサーバが起動できます。

* OpenAPI v2/v3対応
* 無料
* ダイナミックレスポンス対応
* リクエストのバリデーション対応
* CORS対応

### 「Dredd」
![Dredd](../../images/post/post-31/dredd-logo.png)  
「[Dredd](https://dredd.org/en/latest/)」は、OpenAPI Specification形式で記述されたファイルと、  
APIサーバの検証を行うコマンドラインベースのテストツールになります。

* OpenAPI v2/v3対応
* テストで利用できる言語が豊富

### まとめ
今回、「FastAPI」で利用する「OpenAPI Generator Tool」を調べてみましたが、  
「FastAPI」で開発する際は、「FastAPI」に標準で実装されている  
機能を利用するのが現状では良さそうでした。  
上記を利用しない場合は、自分で機能を上書き拡張対応が必要そうです。  
「OpenAPI Specification形式」対応のサードパーティ系で、  
大変便利そうな「Stoplight Studio」/「Prism」/「Dredd」を、  
知ることができましたので、  
ひとつひとつ導入検討していこうと思います。