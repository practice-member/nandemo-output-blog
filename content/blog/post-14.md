---
title: "インターン用環境をDockerで作ってみた(MySQL編)"
date: 2021-01-31T08:55:58Z
draft: false

# author's github account name
author:
 - "Kawaken555"

# post thumb
image: "images/post/post-14/post-14.jpg"

# meta description
description: "PHP、MySQL環境をDockerで作ってみた"

# taxonomies
categories: 
  - "Docker"
tags:
  - "PHP"
  - "MySQL"

# post type
type: "post"
---



### 経緯

私の所属会社は頻繁にインターン生を招いて研修を行っています。  
先日その講師を頼まれました。  

環境はXAMPPで作成し、Apache+PHP+MySQLを使用します。  
古いバージョンのXAMPPを使用しており、PHPが5.6でした。  

特に古いバージョンを選んでいる理由がないようなので、  
合わせる必要はないかなと思って詳細に覚えてないです。  


  
さて、講師を行うにあたり自分も環境構築しようと思ったのですが、  
正直自分のPCにXAMPP入れたくないという気持ちがモリモリ。   

そこで勉強がてらDockerで環境を構築してみました。  
本記事はそのなかでも、MySQL関係のファイルについて忘備録です。  

自分の後任もワンライナーで環境構築できるようになって良いことづくめ。   
やったね。  

コードはリモートレポジトリにPush済みです。    
URLは以下になります。   


https://github.com/Kawaken555/docker-php-apache-mysql


### 各ファイルについて  


#### docker-compose

```
version: '3'
services:
    mysql:
        container_name: mysql
        build: ./docker/db
        environment:
            - MYSQL_DATABASE=db1
            - MYSQL_ROOT_USER=root
            - MYSQL_PASSWORD=mysql           
            - MYSQL_ROOT_PASSWORD=mysql
        volumes:
            - ./docker/db/data:/var/lib/mysql
            - ./docker/db/sql:/docker-entrypoint-initdb.d
        ports:
            - "3306:3306"
        restart: always

    apache-php:
        container_name: php
        build: ./docker/php
        ports:
            - "80:80"
        volumes:
            - ./src:/var/www/html
        links:
            - 'mysql'
        restart: always
```

* 「container_name」はコンテナの名前をつけています。   
PHPからDBを呼ぶ際に、hostとしてコンテナ名を呼ぶので、わかりやすく短めの名前をつけます。  
「container_name」をつけないと「プロジェクト名-mysql_1」のような長い名前がつけられてしまいます。  

* 「build」には、./docker/db のdockerfileを使ってbuildしますよーということが記載してあります。  

* 「environment」は環境変数を使いMySQLの初期設定を設定。  

* 「volumes」ではホスト側のディレクトリをコンテナ内のディレクトリにマウントしています。  


* MySQL公式のimageでは、「docker-entrypoint-initdb.d」に初期化用SQLを入れておくと、imageを起動した際に自動でSQLを実行してくれます。  

* 「./docker/db/sql:/var/lib/mysql」ではDBやテーブルのファイルがマウントされます。  


### dockerfile(MySQL)

```
FROM mysql:latest

RUN apt-get update && apt-get install --no-install-recommends -y \
  locales \
  && apt-get autoremove -y \
  && rm -rf /var/lib/apt/lists/* \
  && sed -i -E 's/# (ja_JP.UTF-8)/\1/' /etc/locale.gen \
  && locale-gen 

ENV LANG ja_JP.UTF-8

COPY ./my.cnf /etc/mysql/conf.d/my.cnf

RUN chmod 644 /etc/mysql/conf.d/*

```

* 「FROM mysql:8.0.17」で使用するimageを指定しています。  

* 「RUN apt-get update」ではパッケージを更新。  

* 「apt-get install -y \ locales」でlocaleコマンドをインストール。  

* 「&& apt-get autoremove -y \&& rm -rf /var/lib/apt/lists/*」でキャッシュ等を削除しimageの大きさを削減。  

* 「sed -i -E 's/# (ja_JP.UTF-8)/\1/' /etc/locale.gen」 で etc/locale.gen を書き換え。  
\# を削除。    

* 「locale-gen」コマンドで、locale.genファイルに書いてあるロケールを生成。  


* 「ENV LANG ja_JP.UTF-8」で環境変数に日本語を設定。  

* 「COPY ./my.cnf /etc/mysql/conf.d/my.cnf」で予め用意しておいたMySQLの設定ファイルをコンテナへコピー。   


* 「RUN chmod 644 /etc/mysql/conf.d/*」 で設定ファイルの権限を変更。  
権限を変更については、以下のURLによると理由はこんな感じ。  
    * mysql は File の Permission が 777 の .cnf を読まない。  
    * Windows からマウントしているディレクトリ/ファイルはすべて 777 になる。  
    * /etc/mysql/conf.d で volume 指定したファイルも 777 になる。  

```
https://qiita.com/waterada/items/1dbf6a977611e0e8f5c8
```



### my.ini

```
[mysql]
default-character-set=utf8mb4

[mysqld]
character-set-server=utf8mb4
collation-server=utf8mb4_general_ci
general-log=1
general-log-file=/var/log/mysql/mysqld.log
default_authentication_plugin=mysql_native_password

[client]
default-character-set=utf8
```

やってることはほぼ文字化け対策。  
utf8ではなくutf8mb4になっている箇所は後に 🍺=🍣問題や ハハパパ問題 について調べるときに修正するので気にしないでください。  

「default_authentication_plugin=mysql_native_password」が曲者でハマリポイント。  

MySQL8.0.4以降はデフォルトの認証方法が変更されましたが、  
PHPの接続ライブラリが新しい認証方法に対応していていないため、  
ここを書き換えてあげる必要があります。  


### まとめ

MySQL編はこれで終了です。  
PHP編は書くつもりですがいつになることやら。。。   

実際にdockerfileやdocker-composeを作って手を動かすことで理解がdockerに対する理解が深まりました。  
今回作ったファイルを叩き台として、色々試していきたいです。   

