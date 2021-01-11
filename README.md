###### ■起動
```
docker-compose build --no-cache
```
```
docker-compose up -d
```
```
docker exec -it hugo /bin/bash
```
###### ■ローカルサーバー起動 (-D はドラフトも表示するオプション)
```
hugo server -D --bind="0.0.0.0"
```
###### ■コンパイル(管理者のみ使用)
```
hugo
```
###### ■記事の作成
```
hugo new content/blog/ファイル名.md
```
