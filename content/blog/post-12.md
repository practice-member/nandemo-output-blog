---
title: "Pythonの単体テスト用ツールについて"
date: 2021-01-31T08:55:53Z
draft: false

# author's github account name
author:
 - "greenwakame"

# post thumb
image: "images/post/post-12/python-logo.png"

# meta description
description: ""

# taxonomies
categories: 
  - "survey"
tags:
  - "python"
  - "unit test tool"
  - "test framework"

# post type
type: "post"
---

### 単体テストとは
人やプロジェクトごとに「単体テスト」の定義が違うことがあります。  
* コードが正確であるか
* 単機能が正確であるか
  
言葉の定義は大事なので、自分が作成する「単体テスト」が、  
どちらかまたは別の定義なのか把握してから、  
作業に取り組むことをおすすめします。

### ホワイトボックステスト
「コードが正確であるか」を確認するテスト手法として、  
「ホワイトボックステスト」の中でよく利用されるパターンが下記になります。

* 命令網羅  
最低一回は命令文を実施するテストパターンです。  
「命令網羅」だけで「単体テスト」を実施してしまうと、  
不完全なテストになるためおすすめはしません。
* 分岐網羅  
上記の「命令網羅」と違う点は、  
判定条件をTRUE/FALSEを最低一回ずつ実施するテストパターンです。  
条件分岐歯科実施しない「命令網羅」より網羅率が良いので、  
「分岐網羅」で単体テストを実施することをおすすめします。

### ブラックボックステスト
それほど高い品質を期待していない場合は、  
「機能テスト」だけで「単体テスト」を済ましてしまうケースが多いです。  
Webアプリケーションの場合、UI(画面)からの機能単位で実施することが多いですが、  
バグを見逃さないためにも適切なテストケースを作成することが大事です。  
「ブラックボックステスト」としてよく利用されるパターンが下記になります。

* 単機能境界値テスト  
データの最大値、最小値だけでなく、  
型が数値だけなのか文字列もあるのかなど、
検討する必要があります。

* 組み合わせテスト
実施する条件を2つ以上組み合わせたテストケースになります。  
検討し始めると様々な組み合わせが考えられるt思います。  
なので出来る限り自動化しておくことをおすすめします。

### Pythonのテストフレームワーク
「テストフレームワーク」とは、ソフトウェアのテストを行うフレームワークのことです。  
各言語に合わせて提供されており、  
開発現場でも下記で紹介する「テストフレームワーク」を使用したテスト行われています。  

* [unittest](https://docs.python.org/ja/3/library/unittest.html)  
<br>
Pythonの標準モジュールで提供されている「テストフレームワーク」です。  
「ユニットテストフレームワーク」は元々「JUnit」に触発されたもので、   
他の言語の主要な「ユニットテストフレームワーク」と同じように利用できます。

sample code
```
import unittest

class TestStringMethods(unittest.TestCase):

    def test_upper(self):
        self.assertEqual('foo'.upper(), 'FOO')

    def test_isupper(self):
        self.assertTrue('FOO'.isupper())
        self.assertFalse('Foo'.isupper())

    def test_split(self):
        s = 'hello world'
        self.assertEqual(s.split(), ['hello', 'world'])
        # check that s.split fails when the separator is not a string
        with self.assertRaises(TypeError):
            s.split(2)

if __name__ == '__main__':
    unittest.main()
```

* [pytest](https://docs.pytest.org/en/stable/)  
<br>
サードパーティーの「ユニットテストフレームワーク」です。  

以下のコマンドでインストールできます。

```
pip install pytest
```

sample code
```
def inc(x):
    return x + 1


def test_answer():
    assert inc(3) == 5
```

### 比較  

##### 記述形式
unittestとpytestでは記述形式に違いがありました。  
<br>
unittestの場合はオブジェクト指向で書くため、  
クラス単位でテストパターンを書いていきます。  
assert文はメソッド単位を呼び出して実施します。  
<br>
pytestでは関数単位でテストパターンを書くことになり、  
assert文は比較演算子で実行結果を比較するようになっています。

##### 実行結果
unittestの実行結果はシンプルでテストを実行したときに結果、  
テストが通らなかったときはどこのテストが通らなかったのかを行番号で示すしくみです。  
<br>
pytestの実行結果はテストに失敗したときに失敗した箇所を細かく表示するため、  
テストに失敗した原因を特定しやすいです。  
テストを実行しているPythonのバージョン、  
pytestのバージョン、  
テストを実行しているディレクトリ、  
のテスト実行時の環境を出力するため、  
テストに失敗したときの原因を実行環境から推測することもできます。

### まとめ
今回Pythonの「テストフレームワーク」を調査してみて、  
まずは標準で実装されている「unittest」を利用し、  
足りないと感じたら「pytest」を導入してみようと思いました。  
ただ、Pythonで開発していくので、  
Pythonらしく書ける「pytest」で書きたくなるような気もしてます。