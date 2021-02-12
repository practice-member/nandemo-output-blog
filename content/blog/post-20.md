---
title: "AndroidのespressoでDatepickerのテストをする時の忘備録"
date: 2021-02-12T13:56:56Z
draft: false

# author's github account name
author:
 - "Kawaken555"

# post thumb
image: "images/post/post-20/post-20.jpg"

# meta description
description: "AndroidのespressoでDatepickerのテストをする時ハマったこと"

# taxonomies
categories: 
  - "mobile"
tags:
  - "espresso"
  - "Android"

# post type
type: "post"
---

### ■結論

以下のコードで実行できます   
なお、kotlinです。    

```
onView(withClassName(Matchers.equalTo(DatePicker::class.java.name))).perform(
    setDate(
        year,
        month,
        day
    )
)
```



### ■解説

#### Datepickerを特定する


つい何でもwithId()で行いたくなりますが、以下を見るとDatepickerはwithId()では扱えないそうです。    


「実行時に、AndroidはDatePickerのIDを複数のサブ要素間で共有するため"withId" は使用しないでください。」  
だそうな。   
https://stackoverflow.com/questions/30597680/android-epresso-datepicker-click-on-ok-add-a-year-instead-of-validate  



実際withId()を使用すると以下のエラーが出ます。

```
androidx.test.espresso.NoMatchingViewException: 
No views in hierarchy found matching: with id is <プロジェクト名/View名>
```

なのでwithClassName()を使用します。   


#### datepickerに値を入力する

datepickerへ値を入力する際には、まず以下のライブラリをgradleに追加します。

```
androidTestImplementation 'androidx.test.espresso:espresso-contrib:3.3.0'
```

そして以下のメソッドを使用します。   

```
PickerActions.setDate()
```



最終的に、以下のコードとなります。   

```
onView(withId(R.id.datePicker)).perform(click())
onView(withClassName(Matchers.equalTo(DatePicker::class.java.name))).perform(
    setDate(
        year,
        month,
        day
    )
)
onView(withText("OK")).perform(click());
```


### ■最後に

意外と詰まったのでメモとして残しておこうと思い記事にしました。   
未熟故にコードがわかりにくくなっており、今後大規模なリファクタリングをせねばなりません。   
そのときに備え、セコセコUIテストを作ろうと思います。    
