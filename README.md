# Redash

redashアプリをdocker on herokuで動かすためのファイル群

## デプロイ方法

```sh
heroku container:push --recursive
```


## セットアップ

### アドオン

- postgres
- redis
- sendgrid

を追加する

### 環境変数

環境変数を `heroku config:set` コマンドを利用して設定していく

```
PYTHONUNBUFFERED:     0
QUEUES:               queries,scheduled_queries,celery
REDASH_COOKIE_SECRET: YOUR_SECRET_TOKEN
REDASH_DATABASE_URL:  PostgresのURL
REDASH_LOG_LEVEL:     INFO
REDASH_REDIS_URL:     redisのURL
REDASH_MAIL_PASSWORD:      sendgridのパスワード
REDASH_MAIL_PORT:          587
REDASH_MAIL_SERVER:        smtp.sendgrid.net
REDASH_MAIL_USERNAME:      sendgridのユーザ
REDASH_MAIL_USE_TLS:       true

```

### 初回のデプロイ時に必要なセットアップ

dbを作る必要がある。デプロイ語に次のコマンドでいけるはず(未確認)

```sh
heroku run /app/manage.py database create_tables
```