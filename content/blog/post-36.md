---
title: "エラーログ確認方法の調査"
date: 2021-08-01T14:10:51Z
draft: false

# author's github account name
author:
 - "be00"

# post thumb
image: "images/post/post-36.jpg"

# meta description
description: ""

# taxonomies
categories: 
  - "Python"
tags:
  - "log"

# post type
type: "post"
---


### FastAPIでのログ確認方法
いろいろ調べてみましたが自分の中でまとまりきらないので、気になったことなどをとにかく箇条書きにします。

この記事をもとに勉強会メンバーの皆さんのお力を借りてまとめられたらと思っています。（半端な内容で申し訳ありません）

- 以前、田畑さんが執筆していた[「ロギング調査」の記事](https://practice-member.github.io/nandemo-output-blog/blog/post-28/)が該当するのかな。

- Middlewareを使ったロギングを行なった場合、どこにそのログは出力されるのか？自分でログの中身を取り出して適当な場所に保存できるのかも・・・
該当しそうな記事は[こちら](https://blog.jicoman.info/2021/01/how-to-logging-request-and-response-body-by-fastapi/)にありましたが自分にはまだ難しく読み解けませんでした。

- そもそもVSCodeのパネルの見方がわかっていなかったけど、問題パネルと出力パネルとデバッグコンソールに表示される内容は今回知りたいエラーログには該当しないのか？

- パネルの見方は[ここ](https://murashun.jp/article/programming/visual-studio-code/panel.html)に記載がありました。出力パネルが一番それっぽいものの、今回開発時に知りたいエラーログとは別物のようですね・・・

- Python ロギングで調査していたときによく目にして、[この辺](https://qiita.com/Galvalume29/items/835b65cddaf094c2b3c2)が怪しいのかなと思ったのはloggingモジュールのコンソールにログを出力するStreamHandlerとファイルに出力するFileHandlerの使用です。うまく使えればよさそうですが、今回の調査内容にマッチしているかは判断できず。

- 調査を開始してすぐ「printでログを出力する」といった内容の記事をいくつか目にしたものの、[ログ出力のための print と import logging はやめてほしい](https://qiita.com/amedama/items/b856b2f30c2f38665701)と言う記事を見て掘り下げるのはやめました。

### 最後に
ここまでずらずらと書きましたが、個人的にはtreamHandlerとかを使うのが良さげと思いましたがいかがでしょう。  
全然趣旨とズレてるようでしたらまた見直させてください。