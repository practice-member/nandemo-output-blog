---
title: "docker-composeのトピックス"
date: 2020-12-29T07:33:46Z
draft: false

# author's github account name
author:
 - "greenwakame"

# post thumb
image: "images/post/post-4/docker-compose-logo.png"

# meta description
description: ""

# taxonomies
categories: 
  - "Docker"
  - "docker-compose"
tags:
  - ""
  - ""

# post type
type: "post"
---
### コンテナ名を指定する

![コンテナ名を指定するした例](../../images/post/post-4/sample-code1.png) 

<!--
version: '3'
services:
  java:
    image: java:11
    container_name: {指定したいコンテナ名を明記}
-->

### イメージを利用しない場合はビルド指定する

![イメージを利用しない場合はビルド指定するした例](../../images/post/post-4/sample-code2.png) 

<!--
version: '3'
services:
  spring_boot:
      build:
        context: ./{指定したいディレクトリ名を明記}
        dockerfile: {指定したいファイル名を明記}
        args:
          - ENVIRONMENT=${ENVIRONMENT}
-->

### コンテナ同士の依存関係がある場合は起動順序を指定する

![コンテナ同士の依存関係がある場合は起動順序を指定するした例](../../images/post/post-4/sample-code3.png) 

<!--
version: '3'
services:
  angular:
      build:
        context: ./angular
        args:
          - ENVIRONMENT=${ENVIRONMENT}
      depends_on:
        - {依存関係上の親にあたるコンテナを指定}
-->

### 永続的なデータやファイルがある場合はvolumesを指定する

![永続的なデータやファイルがある場合はvolumesを指定するした例](../../images/post/post-4/sample-code4.png) 

<!--
version: '2'
services:
  mysql:
    container_name: works-mysql
    build: ./mysql
    environment:
      - MYSQL_DATABASE=${MYSQL_DATABASE}
      - MYSQL_ROOT_USER=${MYSQL_ROOT_USER}
      - MYSQL_ROOT_PASSWORD=${MYSQL_ROOT_PASSWORD}
      - TZ=Japan
    volumes:
      - ./mysql/initdb.d:/docker-entrypoint-initdb.d
      - ./mysql/dbdata:/var/lib/mysql
-->

### コンテナ同士の疎通がある場合はnetworksを利用する

![コンテナ同士の疎通がある場合はnetworksを利用するした例](../../images/post/post-4/sample-code5.png) 

<!--
networks:
  works-net:
    driver: bridge
    ipam:
      config:
        - subnet: "192.168.208.0/20"
-->

### docker-composeを分割しコンテナ間の疎通がある場合のnetworks指定方法

明記するnetworks名はプレフィックスを忘れないようにする

BAD
```
works-net
```

GOOD
```
external_works-net
```

![明記するnetworks名はプレフィックスを忘れないようにする](../../images/post/post-4/sample-code6.png) 

<!--
networks:
  {アクセスしたいnetworks名を明記}:
    external: true
-->

### コンテナを起動したままにさせる

ttyオプションを付与する

![ttyオプションを付与するした例](../../images/post/post-4/sample-code7.png) 

<!--
version: '3'
services:
  java:
    image: java:11
    container_name: java
    tty: true
-->

### まとめ
Dockerを利用して開発するうえで、  
docker-composeは大変便利です。  
ひとつのDockerコンテナで完結する開発であれば、  
不要になる話ですが、基本的に複数のコンテナを利用することが多くなると思われます。  
コンテナをまとめて管理するのにdocker-composeは、  
簡単であり便利だと認識しています。
