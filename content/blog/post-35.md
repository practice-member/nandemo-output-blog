---
title: "FastAPIでもホットリロードがしたい！"
date: 2021-08-01T14:10:47Z
draft: false

# author's github account name
author:
 - "Kawaken555"

# post thumb
image: "images/post/post-35/fastapi-logo.png"

# meta description
description: ""

# taxonomies
categories: 
  - "Python"
tags:
  - "FastAPI"
  - ""

# post type
type: "post"
---

### FastAPIでホットリロードモードで起動するには  

FastAPI起動の際に以下のオプションを付けると    

FastAPIをホットリロードモードで起動することができます。    

```
--reload
```



今私は Docker 環境で FastAPI を使用しているので、  

上記オプションは Dockerfile の CMD コマンドに追記しました。   



```
FROM python:3.9

WORKDIR /fastapi

COPY . /fastapi/

RUN pip install --trusted-host pypi.python.org -r requirements.txt

ENV NAME World

EXPOSE 8000

CMD ["uvicorn", "app:app", "--host", "0.0.0.0", "--port", "8000", "--reload"]
```



これで FastAPI をホットリロードモードで起動できます。   
