---
order: 7
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1c3eda9b-0fe1-81aa-80fe-cb6ae2b3678c
title: 로컬 - Redis 설치
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-81b8-a968-f6b1b2a79b94
    title: Redis
  - id: 1c3eda9b-0fe1-81c7-ae23-cfbc9fd6e83a
    title: 비전공자도 이해할 수 있는 Redis - 캐싱 [ 리펙토링 필요 ]
  - id: 1c3eda9b-0fe1-81aa-80fe-cb6ae2b3678c
    title: 로컬 - Redis 설치
excerpt: '[Install Redis on macOS]() 로컬 yaml HomeBrew 설치 (이미 설치되어 있다면 재설치 필요 X) $ /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)" HomeBrew 설치 '
cover: null
icon: null
notionProperties:
  Tags: Ch 2,사용법
  상태: 완료
schema_version: 1
parent_id: 1c3eda9b-0fe1-81c7-ae23-cfbc9fd6e83a
created: 2025-03-27T07:47:52.771Z
updated: 2025-03-27T07:47:52.771Z
legacy_path: Main/Redis-f6b1b2a79b94/비전공자도 이해할 수 있는 Redis - 캐싱 [ 리펙토링 필요 ]-cfbc9fd6e83a/로컬 - Redis 설치-cb6ae2b3678c/index.md
legacy_category: Redis
source_url: https://beautiful-college-c84.notion.site/1c3eda9b0fe181aa80fecb6ae2b3678c
---
[Install Redis on macOS]()

<a id="1c3eda9b0fe1812aa9d9e0c638c8b377"></a>

### 로컬 

<a id="1c3eda9b0fe181f58f09d2c7c9220ab5"></a>

```yaml
# HomeBrew 설치 (이미 설치되어 있다면 재설치 필요 X)
$ /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

# HomeBrew 설치 여부 확인
$ brew --version

# redis 설치
$ brew install redis

# redis 실행
$ brew services start redis

# redis 실행 여부 확인
$ brew services info redis

# reids 중지
$ brew services stop redis
```

<a id="1c3eda9b0fe18176ba7ae32896767d89"></a>

### Docker

<a id="1c3eda9b0fe18158b109f6eabe59f3a9"></a>

```bash
docker run -d -p 6379:6379 redis:latest
```

<a id="1c3eda9b0fe1811b88afe47395cbe617"></a>

### Docker compose 

<details>
<summary>Spring Boot &#43; mysql &#43; redis</summary>

<a id="1c3eda9b0fe181ed96f8d6b1ca9e79a7"></a>

```yaml
services:
  server:
    container_name: my-server
    build: .
    environment:
      SPRING_DATASOURCE_URL: jdbc:mysql://mysql:3306/mydb?useSSL=false&serverTimezone=UTC&allowPublicKeyRetrieval=true
      SPRING_DATASOURCE_USERNAME: me
      SPRING_DATASOURCE_PASSWORD: 12345678
      SPRING_REDIS_HOST: redis
      SPRING_REDIS_PORT: 6379
    ports:
      - "8080:8080"
    restart: unless-stopped
    depends_on:
      mysql:
        condition: service_healthy
      redis:
        condition: service_healthy

  mysql:
    image: mysql:latest
    container_name: my-mysql
    environment:
      MYSQL_ROOT_PASSWORD: pwd123
      MYSQL_DATABASE: mydb
      MYSQL_USER: me
      MYSQL_PASSWORD: 12345678
    ports:
      - "3306:3306"
    volumes:
      - mysql_data:/var/lib/mysql
    restart: unless-stopped
    healthcheck:
      test: [ "CMD", "mysqladmin", "ping", "-h", "localhost" ]
      interval: 10s
      timeout: 5s
      retries: 5

  redis:
    image: redis:latest
    container_name: my-redis
    ports:
      - "6379:6379"
    restart: unless-stopped
    healthcheck:
      test: [ "CMD", "redis-cli", "ping" ]
      interval: 10s
      timeout: 5s
      retries: 5

volumes:
  mysql_data:
```

</details>

<a id="1c3eda9b0fe181d2969efb06e8d47fcb"></a>

```yaml
services:
  redis:
    image: redis:latest
    container_name: my-redis
    ports:
      - "6379:6379"
    restart: unless-stopped
    healthcheck:
      test: [ "CMD", "redis-cli", "ping" ]
      interval: 10s
      timeout: 5s
      retries: 5
```

<a id="1c3eda9b0fe1811ab1b1d761af4e4f9d"></a>

### Redis 접속

<a id="1c3eda9b0fe181aca83eee8ea50e6742"></a>

```yaml
$ redis-cli # Redis에 접속

127.0.0.1:6379> ping
PONG # 이렇게 출력되면 정상적으로 Redis가 실행되고 있다는 뜻
```
