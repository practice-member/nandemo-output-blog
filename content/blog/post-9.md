---
title: "Google Analyticsを導入してみた"
date: 2020-12-29T07:33:56Z
draft: false

# author's github account name
author:
 - "greenwakame"

# post thumb
image: "images/post/post-9/google-analytics-logo.png"

# meta description
description: ""

# taxonomies
categories: 
  - "Analytics"
tags:
  - "Google Analytics"
  - ""

# post type
type: "post"
---
### アカウント設定
#### Google Analyticsの公式へアクセスし、「無料で設定」をクリック

![「無料で設定」をクリック](../../images/post/post-9/google-analytics-1.png) 

#### 「アカウント名」を入力し、不要であればチェックを外す

![初期状態](../../images/post/post-9/google-analytics-2.png) 

![編集後](../../images/post/post-9/google-analytics-3.png) 

### プロパティ設定
#### レポートのタイムゾーンを「日本」に変更

![「無料で設定」をクリック](../../images/post/post-9/google-analytics-4.png) 

![「無料で設定」をクリック](../../images/post/post-9/google-analytics-5.png) 

#### 通貨を「円」に変更

![「無料で設定」をクリック](../../images/post/post-9/google-analytics-6.png) 

![「無料で設定」をクリック](../../images/post/post-9/google-analytics-7.png) 

#### プロパティ名を入力

![「無料で設定」をクリック](../../images/post/post-9/google-analytics-8.png) 

#### 「詳細オプションを表示」をクリック

![「無料で設定」をクリック](../../images/post/post-9/google-analytics-9.png) 

![「無料で設定」をクリック](../../images/post/post-9/google-analytics-10.png) 

#### 「ウェブサイトのURL」を入力

![「無料で設定」をクリック](../../images/post/post-9/google-analytics-11.png) 

![「無料で設定」をクリック](../../images/post/post-9/google-analytics-13.png) 

### ビジネス概要設定

#### 「業種」を選択

![「無料で設定」をクリック](../../images/post/post-9/google-analytics-14.png) 

![「無料で設定」をクリック](../../images/post/post-9/google-analytics-15.png) 

#### 「ビジネスの規模」を選択

![「無料で設定」をクリック](../../images/post/post-9/google-analytics-16.png) 

![「無料で設定」をクリック](../../images/post/post-9/google-analytics-17.png) 

#### 「作成」をクリック後、「同意」する

![「無料で設定」をクリック](../../images/post/post-9/google-analytics-18.png) 

![「無料で設定」をクリック](../../images/post/post-9/google-analytics-19.png) 

### ウェブストリームの詳細

![「無料で設定」をクリック](../../images/post/post-9/google-analytics-20.png) 

### トラッキングIDが表示されている箇所

#### 「管理」をクリック

![「無料で設定」をクリック](../../images/post/post-9/google-analytics-21.png) 

#### 「トラッキング情報」をクリック

![「無料で設定」をクリック](../../images/post/post-9/google-analytics-22.png) 

#### 「トラッキングID」配下に表示されている

![「無料で設定」をクリック](../../images/post/post-9/google-analytics-23.png) 

### 「HUGO」 config.toml を編集

```
[params]
logo = "images/blog_test_logo.png"
home = "Home"
# Meta data
description = "学んだことを何でもアウトプットするためのブログ"
author = "Practice Members"
# Google Analitycs
googleAnalitycsID = "ここにトラッキングIDを記述します"
# copyright
copyright = "| copyright &copy; 2020 [Themefisher](https://themefisher.com) All Rights Reserved |"

  # Preloader
  [params.preloader]
  enable = true
  preloader = "" # use .png , .svg or .gif format

  # search
  [params.search]
  enable = true
```

### まとめ
今回は事前に「googole account」は作成済みでしたのでスキップしましたが、  
導入までに一時間くらいで導入することが出来ました。  
無料で分析が出来る素晴らしいサービスなので、  
実際に利用してみてメリットなどを投稿出来たらと考えています。

