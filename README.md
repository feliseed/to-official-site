# TOS - 公式サイト

[![Deploy to AWS EC2](https://github.com/feliseed/tos-hp/actions/workflows/deploy-staging.yml/badge.svg)](https://github.com/feliseed/tos-hp/actions/workflows/deploy-staging.yml)
[![Laravel Tests](https://github.com/feliseed/tos-hp/actions/workflows/test.yml/badge.svg)](https://github.com/feliseed/tos-hp/actions/workflows/test.yml)

## 動作要件

PHP 8.3+
Laravel 11+

```text
APP_URL=http://localhost:8000

# 固定値「db」を指定。コンテナ間はtosリポジトリのdocker-compose.ymlのサービス名（db）で通信するため。
DB_HOST=db
```

```shell
# 起動
docker-compose up -d

# ⚠️ 初回もしくはcomposerライブラリを追加する場合は。必ず以下でdockerボリュームを更新してください。
docker-compose exec php composer install

# 停止
docker-compose stop

# リセット
docker-compose down; docker-compose up -**d**
```

## アセットコンパイル

CSS, JSはコンパイルする必要があります。
resources -> public

```shell
npm run watch
# or
npm run dev
```

## 書式整形

標準的な書式に自動で整形します。

```shell
./vendor/bin/pint
```

## 静的構文解析

コードの誤りや曖昧な部分を自動で検出します。

```shell
./vendor/bin/phpstan analyse
```

<https://github.com/nunomaduro/larastan>
