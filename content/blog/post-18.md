---
title: "python デバッグ環境構築について調査しました"
date: 2021-02-06T08:30:54Z
draft: false

# author's github account name
author:
 - "Kawaken555"

# post thumb
image: "images/post/post-18/post-18.jpg"

# meta description
description: "python デバッグ環境構築について調査しました"

# taxonomies
categories: 
  - "Survey"
tags:
  - "Python"
  - "Docker"
  - "debug"

# post type
type: "post"
---
### 前提

* Editor  
VSCode   

* Plugin   
Python (ms-python.python)  
Remote Contaner (ms-vscode-remote.remote-containers)   
   


* その他環境  
Dockr image は python:3.6 使用    
Remote Contaner でコンテナ内の python:3.6 を参照しプログラムを実行  



### VSCodeでデバッグ環境を作る  

* launch.jsonを作成する  

VSCodeのデバッグ機能を使うためには、「launch.json」という設定ファイルを作成する必要があります。     
 

まずVSCodeのデバッグアイコンをクリックします。   

![デバッグアイコン](../../images/post/post-18/debug-icon.jpeg)  


その後以下の箇所を押下します。  

![ファイル作成](../../images/post/post-18/procedure.jpeg)  


以下の内容のlaunch.jsonが作成されます。

 
![ファイル内容](../../images/post/post-18/launch-json.jpeg)  


あとは適当にブレークポイントを打ちます。   

![ブレークポイント](../../images/post/post-18/draw-break-point.jpeg)  


「実行」メニューの「デバッグの開始」から実行します。  

![実行](../../images/post/post-18/start-debug.jpeg)  


デバッグが実行されます。


![ステップ実行](../../images/post/post-18/step-excecute.jpeg)    

変数の中身は以下に表示されます。   

![変数の中身](../../images/post/post-18/valiable-contents.jpeg)  



### 余談

別件で Docker + Python Flask + Remote Container + VSCodeでデバッグ環境を作った際ハマったことです。   


* 出ていたエラー  
```
Address already in use
```

* 原因  
Dockerfile の方で、最後に以下のコマンドを実行していました。  
Docker コンテナを立ち上げた時点でサーバーも起動するようになってます。    
```
CMD ["python", "app.py"]
```

そして以下が Flask プロジェクトの launch.json です。  
上記と同様の手順で自動生成されたファイルです。

```
"args": [
  "run",
  "--no-debugger",
  "--no-reload"
],
```


同じサーバーを2つ立ち上げようとしたことによるエラーでした。   


* 対策  
取り敢えず Dockerfile の CMD ["python", "app.py"] の部分をコメントアウトし、対応しています。    
後日もっと良い方法を探せたら良いなぁ。   



