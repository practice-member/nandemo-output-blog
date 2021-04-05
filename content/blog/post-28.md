---
title: "FastAPI ロギング調査"
date: 2021-02-28T13:13:31Z
draft: false

# author's github account name
author:
 - "greenwakame"

# post thumb
image: "images/post/post-28/fastapi-logo.png"

# meta description
description: ""

# taxonomies
categories: 
  - "FastAPI"
tags:
  - "logging"

# post type
type: "post"
---

### 「ロギング」とは
起こった出来事についての情報などを一定の形式で時系列に記録を蓄積することである。  
そのように記録されたデータのことを「ログ」という。

### 「Middleware」の使用例
[公式](https://fastapi.tiangolo.com/tutorial/middleware/)には、レスポンスに処理を追加する例が記載されています。

```
import time

from fastapi import FastAPI, Request

app = FastAPI()


@app.middleware("http")
async def add_process_time_header(request: Request, call_next):
    start_time = time.time()
    response = await call_next(request)
    process_time = time.time() - start_time
    response.headers["X-Process-Time"] = str(process_time)
    return response
```

### 「カスタムリクエスト」と「APIRouteクラス」
APIRouterを利用することで、カスタムリクエストを容易に実装することが出来ます。

```
import time
from typing import Callable

from fastapi import APIRouter, FastAPI, Request, Response
from fastapi.routing import APIRoute


class TimedRoute(APIRoute):
    def get_route_handler(self) -> Callable:
        original_route_handler = super().get_route_handler()

        async def custom_route_handler(request: Request) -> Response:
            before = time.time()
            response: Response = await original_route_handler(request)
            duration = time.time() - before
            response.headers["X-Response-Time"] = str(duration)
            print(f"route duration: {duration}")
            print(f"route response: {response}")
            print(f"route response headers: {response.headers}")
            return response

        return custom_route_handler


app = FastAPI()
router = APIRouter(route_class=TimedRoute)


@app.get("/")
async def not_timed():
    return {"message": "Not timed"}


@router.get("/timed")
async def timed():
    return {"message": "It's the time of my life"}


app.include_router(router)
```

下記は「X-Response-Time」をレスポンスに追加している例になります。

```
import time
from typing import Callable

from fastapi import APIRouter, FastAPI, Request, Response
from fastapi.routing import APIRoute


class TimedRoute(APIRoute):
    def get_route_handler(self) -> Callable:
        original_route_handler = super().get_route_handler()

        async def custom_route_handler(request: Request) -> Response:
            before = time.time()
            response: Response = await original_route_handler(request)
            duration = time.time() - before
            response.headers["X-Response-Time"] = str(duration)
            print(f"route duration: {duration}")
            print(f"route response: {response}")
            print(f"route response headers: {response.headers}")
            return response

        return custom_route_handler


app = FastAPI()
router = APIRouter(route_class=TimedRoute)


@app.get("/")
async def not_timed():
    return {"message": "Not timed"}


@router.get("/timed")
async def timed():
    return {"message": "It's the time of my life"}


app.include_router(router)
```

### 「例外処理」のロギング
「ValidationErrorLoggingRoute」か「RequestValidationError」を、  
利用してログキングすることが出来ますが、  
「ValidationErrorLoggingRoute」の方が容易に実装出来そうです。

try/exceptブロック内でリクエストを処理するだけです。

```
from typing import Callable, List

from fastapi import Body, FastAPI, HTTPException, Request, Response
from fastapi.exceptions import RequestValidationError
from fastapi.routing import APIRoute


class ValidationErrorLoggingRoute(APIRoute):
    def get_route_handler(self) -> Callable:
        original_route_handler = super().get_route_handler()

        async def custom_route_handler(request: Request) -> Response:
            try:
                return await original_route_handler(request)
            except RequestValidationError as exc:
                body = await request.body()
                detail = {"errors": exc.errors(), "body": body.decode()}
                raise HTTPException(status_code=422, detail=detail)

        return custom_route_handler


app = FastAPI()
app.router.route_class = ValidationErrorLoggingRoute


@app.post("/")
async def sum_numbers(numbers: List[int] = Body(...)):
    return sum(numbers)
```

例外が発生したRequest場合でも、  
インスタンスはスコープ内にあるため、  
エラーを処理するときにリクエスト本文を読み取って利用できます。

```
from typing import Callable, List

from fastapi import Body, FastAPI, HTTPException, Request, Response
from fastapi.exceptions import RequestValidationError
from fastapi.routing import APIRoute


class ValidationErrorLoggingRoute(APIRoute):
    def get_route_handler(self) -> Callable:
        original_route_handler = super().get_route_handler()

        async def custom_route_handler(request: Request) -> Response:
            try:
                return await original_route_handler(request)
            except RequestValidationError as exc:
                body = await request.body()
                detail = {"errors": exc.errors(), "body": body.decode()}
                raise HTTPException(status_code=422, detail=detail)

        return custom_route_handler


app = FastAPI()
app.router.route_class = ValidationErrorLoggingRoute


@app.post("/")
async def sum_numbers(numbers: List[int] = Body(...)):
    return sum(numbers)
```

### まとめ
今回は「FastAPI」でのロギングについて調べてみましたが、  
最低限実装したい形式は全て[「カスタムリクエストとAPIRouteクラス」](https://fastapi.tiangolo.com/advanced/custom-request-and-route/)や[「Middleware」](https://fastapi.tiangolo.com/tutorial/middleware/)に、  
記述されていましたので、ますます「FastAPI」は開発しやすそうなフレームワークだと認識できました。