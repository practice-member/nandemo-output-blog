---
title: "PythonのLintツールと自動整形ツールを導入してみた"
date: 2021-08-29T06:19:18Z
draft: false

# author's github account name
author:
 - "Kawaken555"

# post thumb
image: "images/post/post-39/post-39.jpg"

# meta description
description: "PythonのLintツールと自動整形ツールを導入してみた"

# taxonomies
categories: 
  - "Python"
tags:
  - ""
  - ""

# post type
type: "post"
---

### はじめに

調査成果として、lint と自動整形について調査が終了し、記事を書いていただきたので、  

早速プロジェクトに導入してみました。   

lint には、「試すのが簡単そう」とのことで pylint 、 自動整形には勉強会で話題になった black を採用しています。     



### やったこと

#### 1. pylint、blackのインストール準備

fastapi/requirements.txt の末尾に新たに pylint、black を追加します。  

バージョンは本変更実施時の最新です。   

現在の最新バージョンについては 下記をご確認ください。

[pylint](https://pypi.org/project/pylint/)

[black](https://pypi.org/project/black/) 

requirements.txt は今こんな感じです。

```
fastapi==0.67.0
uvicorn==0.14.0
sqlalchemy==1.4.22
mysqlclient==2.0.3
pylint==2.10.2
black==21.7b0
```



なお、pylint は 「Visual Studio for Python プロジェクトにはデフォルトで「[pylint](https://www.pylint.org/)」が導入されて」いる

ということでしたが、   

明示的にインストールしないとRemote Container がエラーモーダルを出すのでここではpylint も列挙しています。



#### 2. .devcontainer.jsonの編集

.devcontainer.json に、「settings」 を追加します。

この settingsは、Remote Container を使っていない場合にはVSCode の settings.json に書く内容を記載する場所です。     

```
{
  "name": "Python",
  "dockerComposeFile": "docker-compose.yml",
  "service": "python",
  "workspaceFolder": "/fastapi",
  "extensions": [
    "ms-python.python",
    "formulahendry.code-runner",
  ],
  "settings": {
    "python.linting.enabled": true,
    "python.linting.pylintEnabled": true,
    "python.linting.flake8Enabled":false,
    "python.linting.lintOnSave": true,
    "python.fomatting.provider":"black",
    "editor.formatOnSave":true
},
}
```



#### 3.Docker image の削除  

現在、requirements.txt を読み込み pip install する処理を    

fastapi/Dockerfile で実施しています。   

つまり、image が作られる際に pip install が実施されているということです。   

今回 requirements.txt の依存性を更新したので、

image を削除しビルドし直す必要があります。   



ただ、下記のコマンドを使って image の削除をしようとしてのですが、

自分の環境だとimage だけがうまく削除できませんでした。

```
コンテナ停止
docker stop $(docker ps -q)

コンテナ削除
docker-compose down --rmi all --volumes
```



結局Docker の GUI から削除しました。

devcontainer のせいでしょうか。。。     



次にVSCode の左下の緑の部分をクリックし、「Reopen in Container」します。



コンテナ立ち上げ後、右下に 「Configuration file(s) changed: devcontainer.json. The container might need to be rebuilt to apply the changes.」 と出てきたら、「build」を選択してください。



#### 4.反映されたか確認をする

適当な箇所に以下の関数をコピペし、Ctrl + S を押してみてください。

自動で整形してくれるはずです。   

```
def hoge():
    print("或いは" 
    "牡蠣で一杯の"
     "海")
```



また、pylint の静的解析の結果は VSCode の下部にある「問題タブ」に表示されるので、確認してみてください。   
