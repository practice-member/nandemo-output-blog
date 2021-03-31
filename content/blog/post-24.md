---
title: "FastAPI 認証処理について"
date: 2021-02-28T13:13:23Z
draft: false

# author's github account name
author:
 - "Kawaken555"

# post thumb
image: "images/post/post-24/post-24.jpg"

# meta description
description: "FastAPI 認証処理について"

# taxonomies
categories: 
  - "survey"
tags:
  - "FastAPI"
  - "Python"

# post type
type: "post"
---


#### 前提   

本稿では、認証処理を「クライアントが誰であるかを確認する処理」とし、   
主にログイン処理に使えるライブラリについて調べました。    


#### 認証処理の種類   

認証処理の方式について、いくつかの規格があります。   

認証のことを調べる際はまず以下の資料を頭の片隅に置いて取り組むとうまく理解が進みました。   


* よくわかる認証と認可   
https://dev.classmethod.jp/articles/authentication-and-authorization/  


* Basic認証、Digest認証、Bearer認証、OAuth認証方式について    
https://architecting.hateblo.jp/entry/2020/03/27/130535  


* OAuth 2.0 の解説サイトを漁る前に  
https://qiita.com/kojisaiki/items/48adf59d5d634fd330af



#### FastAPIで使用できる認証ライブラリ  


##### ■ FastAPI-Login   
    

特徴としては以下の特徴があります。    

* シンプルな認証依存性を提供     
* トークンをリクエストヘッダまたはクッキーとしてサポート   
* ユーザーが未承認の場合のコールバックのサポート    
* OpenAPIサポート   


カスタマイズ前提のシンプルなライブラリで、   
手軽にログイン機能を作成したい場合に重宝しそうな印象です。  

```
URL：https://fastapi-login.readthedocs.io/
最終リリース日： Feb 19, 2021   
Stars : 112   
License: MIT License   
```


##### ■ FastAPI-Users  

予め機能が一通り揃っていて、無難な選択肢という印象です。  


特徴としては以下の特徴があります。   

* Cookie認証とJWT認証をサポートしています。   
* User登録、ログイン、パスワードの再設定、メールルートの確認がすぐに使えます。  
* 以下のORマッパーをサポートしています。     
SQLAlchemy,MongoDB,TortoiseORM,ormar  


※Cookie認証とJWT認証についてはこちら  
https://qiita.com/doyaaaaaken/items/02357c2ebca994160804



```
URL : https://frankie567.github.io/fastapi-users/
最終リリース日： Mar 9, 2021   
Stars : 706  
License: MIT License   
Python3.7以上が必要   
```


##### ■ FastAPI-Contrib   

認証及び認可の機能を提供してくれるライブラリです。   
 
ORマッパーはMongoDBのみのサポートとなっている点や、  
公式ドキュメントが他のライブラリよりも貧弱な点が気になります。   



```
https://pypi.org/project/fastapi-contrib/  
最終リリース日：  Mar 1, 2021  
Stars : 300  
License: MIT License 
```


#### まとめ

ドキュメントが比較的充実していて、  
サポートしているORマッパーが多く
ある程度機能が初めから揃っているFastAPI-Users を  
選択するのが良いと考えています。   


