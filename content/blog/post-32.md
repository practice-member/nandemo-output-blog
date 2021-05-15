---
title: "Android StudioでLayout Editorが表示されない事象に対応する"
date: 2021-02-28T13:13:42Z
draft: false

# author's github account name
author:
 - "Kawaken555"

# post thumb
image: "images/post/post-32/sum-nail.jpg"

# meta description
description: "Android StudioでLayout Editorが表示されない事象に対応する"

# taxonomies
categories: 
  - "Android"
tags:
  - "Android Studio"
  - ""

# post type
type: "post"
---

## 環境   

Android Studio 4.2.0 及び 4.2.1   
minSdkVersion 26  
targetSdkVersion 30  
 


## Android Studioを 4.2.0にしたらレイアウトのDesignビューが表示されなくなった

Android Studio を 4.2.0 にアップデートしたら、一部の Layout における Design ビューが   
表示されなくなりました。   

画面は以下のようになってます。   

![エラー画面](../../images/post/post-32/empty_screen.jpeg)  


「 String index out of range: -1 」 の詳細は以下。   

```
java.lang.StringIndexOutOfBoundsException: String index out of range: -1
	at java.base/java.lang.StringLatin1.charAt(StringLatin1.java:47)
	at java.base/java.lang.String.charAt(String.java:693)
	at android.content.res.BridgeTypedArray.getType(BridgeTypedArray.java:1024)
	at android.content.res.BridgeTypedArray.getType(BridgeTypedArray.java:809)
	at android.content.res.BridgeTypedArray.getValue(BridgeTypedArray.java:778)
	at android.content.res.BridgeTypedArray.peekValue(BridgeTypedArray.java:847)
	at android.view.View.<init>(View.java:5951)
	at android.view.ViewGroup.<init>(ViewGroup.java:697)
	at android.widget.FrameLayout.<init>(FrameLayout.java:99)
	at com.android.layoutlib.bridge.MockView.<init>(MockView.java:55)
	at com.android.layoutlib.bridge.MockView.<init>(MockView.java:51)
	at com.android.layoutlib.bridge.MockView.<init>(MockView.java:47)
	at android.view.BridgeInflater.createViewFromTag(BridgeInflater.java:324)
	at android.view.LayoutInflater.createViewFromTag(LayoutInflater.java:959)
	at android.view.LayoutInflater.rInflate_Original(LayoutInflater.java:1121)
	at android.view.LayoutInflater_Delegate.rInflate(LayoutInflater_Delegate.java:72)
	at android.view.LayoutInflater.rInflate(LayoutInflater.java:1095)
	at android.view.LayoutInflater.rInflateChildren(LayoutInflater.java:1082)
	at android.view.LayoutInflater.rInflate_Original(LayoutInflater.java:1124)
	at android.view.LayoutInflater_Delegate.rInflate(LayoutInflater_Delegate.java:72)
	at android.view.LayoutInflater.rInflate(LayoutInflater.java:1095)
	at android.view.LayoutInflater.rInflateChildren(LayoutInflater.java:1082)
	at android.view.LayoutInflater.rInflate_Original(LayoutInflater.java:1124)
	at android.view.LayoutInflater_Delegate.rInflate(LayoutInflater_Delegate.java:72)
	at android.view.LayoutInflater.rInflate(LayoutInflater.java:1095)
	at android.view.LayoutInflater.rInflateChildren(LayoutInflater.java:1082)
	at android.view.LayoutInflater.inflate(LayoutInflater.java:680)
	at android.view.LayoutInflater.inflate(LayoutInflater.java:499)
	at com.android.layoutlib.bridge.impl.RenderSessionImpl.inflate(RenderSessionImpl.java:325)
	at com.android.layoutlib.bridge.Bridge.createSession(Bridge.java:369)
	at com.android.tools.idea.layoutlib.LayoutLibrary.createSession(LayoutLibrary.java:141)
	at com.android.tools.idea.rendering.RenderTask.createRenderSession(RenderTask.java:710)
	at com.android.tools.idea.rendering.RenderTask.lambda$inflate$6(RenderTask.java:865)
	at com.android.tools.idea.rendering.RenderExecutor$runAsyncActionWithTimeout$2.run(RenderExecutor.kt:174)
	at java.base/java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1128)
	at java.base/java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:628)
	at java.base/java.lang.Thread.run(Thread.java:834)
```


「 Render Problem 」の詳細は以下   

```
java.lang.reflect.InvocationTargetException
	at jdk.internal.reflect.GeneratedMethodAccessor971.invoke(Unknown Source)
	at java.base/jdk.internal.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
	at java.base/java.lang.reflect.Method.invoke(Method.java:566)
	at android.view.BridgeInflater.lambda$createViewFromCustomInflater$0(BridgeInflater.java:259)
	at android.view.BridgeInflater.createViewFromCustomInflater(BridgeInflater.java:285)
	at android.view.BridgeInflater.onCreateView(BridgeInflater.java:122)
	at android.view.LayoutInflater.onCreateView(LayoutInflater.java:928)
	at android.view.LayoutInflater.onCreateView(LayoutInflater.java:948)
	at android.view.LayoutInflater.createViewFromTag(LayoutInflater.java:1002)
	at android.view.BridgeInflater.createViewFromTag(BridgeInflater.java:309)
	at android.view.LayoutInflater.createViewFromTag(LayoutInflater.java:959)
	at android.view.LayoutInflater.rInflate_Original(LayoutInflater.java:1121)
	at android.view.LayoutInflater_Delegate.rInflate(LayoutInflater_Delegate.java:72)
	at android.view.LayoutInflater.rInflate(LayoutInflater.java:1095)
	at android.view.LayoutInflater.rInflateChildren(LayoutInflater.java:1082)
	at android.view.LayoutInflater.rInflate_Original(LayoutInflater.java:1124)
	at android.view.LayoutInflater_Delegate.rInflate(LayoutInflater_Delegate.java:72)
	at android.view.LayoutInflater.rInflate(LayoutInflater.java:1095)
	at android.view.LayoutInflater.rInflateChildren(LayoutInflater.java:1082)
	at android.view.LayoutInflater.rInflate_Original(LayoutInflater.java:1124)
	at android.view.LayoutInflater_Delegate.rInflate(LayoutInflater_Delegate.java:72)
	at android.view.LayoutInflater.rInflate(LayoutInflater.java:1095)
	at android.view.LayoutInflater.rInflateChildren(LayoutInflater.java:1082)
	at android.view.LayoutInflater.inflate(LayoutInflater.java:680)
	at android.view.LayoutInflater.inflate(LayoutInflater.java:499)
	at com.android.layoutlib.bridge.impl.RenderSessionImpl.inflate(RenderSessionImpl.java:325)
	at com.android.layoutlib.bridge.Bridge.createSession(Bridge.java:369)
	at com.android.tools.idea.layoutlib.LayoutLibrary.createSession(LayoutLibrary.java:141)
	at com.android.tools.idea.rendering.RenderTask.createRenderSession(RenderTask.java:710)
	at com.android.tools.idea.rendering.RenderTask.lambda$inflate$6(RenderTask.java:865)
	at com.android.tools.idea.rendering.RenderExecutor$runAsyncActionWithTimeout$2.run(RenderExecutor.kt:174)
	at java.base/java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1128)
	at java.base/java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:628)
	at java.base/java.lang.Thread.run(Thread.java:834)
Caused by: java.lang.StringIndexOutOfBoundsException: String index out of range: -1
	at java.base/java.lang.StringLatin1.charAt(StringLatin1.java:47)
	at java.base/java.lang.String.charAt(String.java:693)
	at android.content.res.BridgeTypedArray.getType(BridgeTypedArray.java:1024)
	at android.content.res.BridgeTypedArray.getType(BridgeTypedArray.java:809)
	at android.content.res.BridgeTypedArray.getValue(BridgeTypedArray.java:778)
	at android.content.res.BridgeTypedArray.peekValue(BridgeTypedArray.java:847)
	at android.view.View.<init>(View.java:5951)
	at android.widget.TextView.<init>(TextView.java:996)
	at android.widget.EditText.<init>(EditText.java:87)
	at android.widget.EditText.<init>(EditText.java:83)
	at androidx.appcompat.widget.AppCompatEditText.<init>(AppCompatEditText.java:74)
	at androidx.appcompat.widget.AppCompatEditText.<init>(AppCompatEditText.java:69)
	at androidx.appcompat.app.AppCompatViewInflater.createEditText(AppCompatViewInflater.java:209)
	at androidx.appcompat.app.AppCompatViewInflater.createView(AppCompatViewInflater.java:127)
	... 34 more

```


## 原因と対応方法    


原因は、 EditView に以下の記述でした。  

```
android:autofillHints=""
``` 


何かの記事を見て Missing autofillHints attribute の警告を消すために書いていたのですが、   
これを以下のように変えると不具合は解消しました。

```
android:autofillHints='""'
``` 


ただこの方法も後に不具合の原因になると思われるので、   
素直に tools:ignore="Autofill" や android:importantForAutofill="no" を  
つけたほうが良いと思われます。   






