---
title: "Dockerfileのベストプラクティスを考えてみた"
date: 2020-12-29T07:33:43Z
draft: false

# post thumb
image: "images/post/post-3/docker-logo.png"

# meta description
description: ""

# taxonomies
categories: 
  - "Docker"
tags:
  - ""
  - ""

# post type
type: "post"
---
### イメージサイズは出来るだけ軽くする
  
* scratchやalpineなど軽量なベースイメージを選択する
* ランタイムに必要なファイルのみCOPYする
* 不要なパッケージのインストールを控える
* レイヤを減らす

### レイヤの減らし方

* RUNで実行する場合は、&&で連結させる
* [マルチステージビルド](https://docs.docker.com/develop/develop-images/multistage-build/)を利用する

#### マルチステージビルドを利用した例 

![マルチステージビルドを利用した例](../../images/post/post-3/sample-code1.png)  

<!---
FROM golang:1.7.3
WORKDIR /go/src/github.com/alexellis/href-counter/
RUN go get -d -v golang.org/x/net/html  
COPY app.go .
RUN CGO_ENABLED=0 GOOS=linux go build -a -installsuffix cgo -o app .

FROM alpine:latest  
RUN apk --no-cache add ca-certificates
WORKDIR /root/
COPY --from=0 /go/src/github.com/alexellis/href-counter/app .
CMD ["./app"]  
-->

* ADDを利用したアンチパターン

BADパターン

![BADパターン](../../images/post/post-3/sample-code2.png)  

<!---
ADD http://sample.com/big.tar.xz /usr/src/things/
RUN tar -xJf /usr/src/things/big.tar.xz -C /usr/src/things
RUN make -C /usr/src/things all
-->

GOODパターン

![GOODパターン](../../images/post/post-3/sample-code3.png)  

<!---
RUN mkdir -p /usr/src/things \
&& curl -SL http://sample.com/big.tar.xz \
| tar -xJC /usr/src/things \
&& make -C /usr/src/things all
-->

### ビルドキャッシュを正しく活用する
イメージをビルドする際、キャッシュ内で再利用出来るイメージを探します。  
なければイメージのキャッシュは削除されます。  
以下のコードはBADのほうがレイヤが少ないためGOODに見えますが、  
appに変更が発生するたびに、ライブラリのインストールが実施されビルド時間が長くなります。

BADパターン

![BADパターン](../../images/post/post-3/sample-code4.png)  

<!---
COPY app /tmp/
RUN pip install --requirement /tmp/requirements.txt
-->

GOODパターン

![GOODパターン](../../images/post/post-3/sample-code5.png)  

<!---
COPY requirements.txt /tmp/
RUN pip install --requirement /tmp/requirements.txt
COPY app /tmp/
-->

### まとめ
Dockerは自分のpc環境を汚さずに開発出来るだけでなく、  
開発環境を高速に構築出来る最高のツールだと考えています。  
しかし、イメージのサイズやキャッシュ/ビルドなどを考えずに  
利用していると、pcのディスク容量が逼迫していきます。  
ビルド時間も高速化を検討しないと、  
開発する時間がとれなくなってしまいます。  
Dockerを便利に利用するために、  
これからもベストプラクティスを考えていこうと思います。
