---
title: "AndroidのsetColorFilterでハマった話"
date: 2021-05-20T13:44:47Z
draft: false

# author's github account name
author:
 - "Kawaken555"

# post thumb
image: "images/post/post-33/post-33.jpg"

# meta description
description: "AndroidのsetColorFilterでハマった話"

# taxonomies
categories: 
  - "Android"
tags:
  - "mobile"
  - ""

# post type
type: "post"
---

#### 環境

Android Studio 4.2.1  
minSdkVersion 26  
targetSdkVersion 30  

#### ImageViewの色をつけようとしたけどつけられなかった


以下のような拡張関数を作って ImageViewに セットした SVG の色をつけようとしました。   

```
fun ImageView.setColor(colorCode: Int) {

    setColorFilter(colorCode, PorterDuff.Mode.SRC_IN)
}
```


なお colorCode には、color.xml のリソースを以下のような形で書いて渡していました。   

```
saveIcon.setColor(R.color.red)
```



#### エラーは出ないのに色がつかない

しかし上記のコードでは意図した色がつかず、何故かグレーになってしまいました。    


以前上記の方法で SVG にグレーの色を付けた経験があったので、何故できないんだ、    
なんで今回もグレーになってしまうんだと悩みました。


#### setColorFilterに渡している引数が違った  

R.color.red で返ってくるのは、xml ファイルに記載された文字列と紐付いたリソース IDらしいです。   
Intの情報ではありますが、色情報ではないです。  


なので、上記の拡張関数は以下のように書き、リソースから色情報を取得しなくてはなりません。

```
fun ImageView.setColor(colorCode: Int) {
    val color = ResourcesCompat.getColor(resources, colorCode, null)

    setColorFilter(color, PorterDuff.Mode.SRC_IN)
}
```

偶然にも以前意図した色をつけることが出来てしまっていたので悩んでしまいました。  
今後足りていない values/xxxx.xml について理解を深めようと思います。

