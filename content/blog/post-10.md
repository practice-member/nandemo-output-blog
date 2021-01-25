---
title: "Hugoのフォルダの役割について"
date: 2020-12-29T07:33:58Z
draft: false

# author's github account name
author:
 - "Kawaken555"

# post thumb
image: "images/post/post-10/post-10.jpg"

# meta description
description: "Hugoの各フォルダの説明"

# taxonomies
categories: 
  - "Static site generator"
tags:
  - "Hugo"
  - ""

# post type
type: "post"
---

### はじめに


Hugoでのサイト構築に困っている人向けの記事です。  
詳しくは、当サイトのヘッダーにあるGithubリンクから  
当ブログのレポジトリ内のファイル構成を見てください。   



### Hugoのフォルダの役割について

#### ■blog-project\content\


ブログ記事を作成し格納するためのフォルダです。  
「hugo」コマンドにより、  
このフォルダ内のマークダウンファイルがコンパイルされます。  




#### ■blog-project\docs\


Github Pages に記事を公開するためのフォルダです。    
config.toml に、 hugoコマンド でコンパイルされた成果物を  
docsフォルダを へ格納するよう設定を書いています。  

Github Pages はこの docsフォルダ の内容をそのまま画面に表示します。  

docsフォルダ を使用する方法で Github Pages を使いたい場合は、  
このdocsフォルダ はプロジェクトの rootフォルダ に  
なければならないので注意してください。  






#### ■blog-project\layouts\

使用しているテーマの画面構成を書き換えたいときに使用します。  
下記で解説している themesフォルダ 内の layoutsフォルダ から、  
画面構成を変更したい htmlファイル をコピーし、  
blog-project\layouts\ に格納します。  


themesフォルダ よりも blog-project\layouts\ のファイルの  
内容が優先して画面に表示されるので、
blog-project\layouts\ 内に格納したファイルを  
変更することで画面表示を変えることができます。

liva-hugoの場合は themes\liva-hugo\layouts のファイルを  
全て blog-project\layouts\ へコピーしました。  

編集したいファイルだけ個別にコピーしたところ、エラーが発生したからです。   
テーマによっては個別に編集対応できるのかもしれません。  



テーマの配布元がthemesの内容を更新しても、  
ユーザーがカスタマイズしたファイルが  
上書き更新されないようにするための仕組みだと思われます。  


逆に、配布元のテーマの更新があったときには個別に対処しなければ  
更新内容が反映されないということは覚えておかねばならないです。  






#### ■blog-project\themes\


使用しているテーマが格納されたフォルダです。  
テーマによってはこの中に使用例としてサンプルが格納されています。  


本ブログで採用しているliva-hugoでは、  
「exampleSite」フォルダがサンプルに当たります。  
「exampleSite」通りに config.toml や imageフォルダ を作ると、  
demoサイトと同じものが作れます。  




#### ■blog-project\static\


記事で使用する画像などを保管しておくフォルダです。   



### 今後について

また改修等で新しい情報が入った際には書き足す予定です。  

