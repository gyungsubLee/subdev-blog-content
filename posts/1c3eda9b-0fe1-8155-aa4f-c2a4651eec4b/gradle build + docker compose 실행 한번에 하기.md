---
order: 8
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1c3eda9b-0fe1-8155-aa4f-c2a4651eec4b
title: gradle build + docker compose 실행 한번에 하기
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-8138-94e1-d1a8abd3203c
    title: Docker
  - id: 1c3eda9b-0fe1-8115-b158-c17d844ab16c
    title: 비전공자도 이해할 수 있는 Docker 입문/실전
  - id: 1c3eda9b-0fe1-8155-aa4f-c2a4651eec4b
    title: gradle build + docker compose 실행 한번에 하기
excerpt: "방법 1) docker-compose 실행 전에 빌드 스크립트 실행 --- 1. start.sh 파일 생성 docker-compose.yml 파일이 있는 루트 디렉토리에 start.sh 생성 docker 📂 my-spring-app ├── 📂 src ├── 📂 build ├── 📄 Dockerfile ├── 📄 "
cover: null
icon: null
notionProperties:
  Tags: 추가
  상태: 완료
schema_version: 1
parent_id: 1c3eda9b-0fe1-8115-b158-c17d844ab16c
created: 2025-03-27T07:47:52.769Z
updated: 2025-05-18T13:43:53.966Z
legacy_path: Main/Docker-d1a8abd3203c/비전공자도 이해할 수 있는 Docker 입문-실전-c17d844ab16c/gradle build + docker compose 실행 한번에 하기-c2a4651eec4b/index.md
legacy_category: Docker
source_url: https://beautiful-college-c84.notion.site/1c3eda9b0fe18155aa4fc2a4651eec4b
---
<a id="1c3eda9b0fe1810eb718fc64e79ddf9a"></a>

### <strong>방법 1) docker&#45;compose 실행 전에 빌드 스크립트 실행</strong>

---

1. <strong><code>start&#46;sh</code></strong><strong> 파일 생성</strong>
    <a id="1c3eda9b0fe18175a75ded9e51286fb5"></a>

    <code>docker&#45;compose&#46;yml</code><strong> 파일이 있는 루트 디렉토리</strong>에 <code>start&#46;sh</code> 생성

    <a id="1c3eda9b0fe181d99a3df620e759347a"></a>

    ```docker
    📂 my-spring-app
    ├── 📂 src
    ├── 📂 build
    ├── 📄 Dockerfile
    ├── 📄 docker-compose.yml  ← 여기!
    ├── 📄 start.sh             ← 여기 만들기!
    ├── 📄 settings.gradle.kts
    └── 📄 build.gradle.kts
    ```

1. <strong><code>start&#46;sh</code></strong><strong> 스크립트 작성</strong>
    <a id="1c3eda9b0fe1812b8e9cc53f41b9b9ed"></a>

    ```bash
    #!/bin/bash

    # 현재 스크립트가 위치한 디렉토리로 이동 (어디서 실행해도 정상 동작)
    cd "$(dirname "$0")"

    echo "🔨 Gradle Build 시작..."
    ./gradlew clean build || { echo "❌ Gradle Build 실패!"; exit 1; }

    echo "🚀 Docker Compose 실행..."
    docker compose up -d --build

    echo "📋 Docker compose ps 실행..."
    docker compose ps
    ```

1. <strong><code>start&#46;sh</code></strong><strong> 실행</strong>
    <a id="1c3eda9b0fe181f19aebdda6945b3cca"></a>

    ```docker
    # 	실행 권한 부여
    chmod +x start.sh
    ```

    <a id="1c3eda9b0fe18139a51df4b7b3f0642b"></a>

    ```bash
    # 실행
    ./start.sh
    ```

<a id="1c3eda9b0fe181599401c70ff0d4ca6d"></a>

### <strong>방법 2)  Dockerfile 내에서 </strong><strong><code>&#46;/gradlew build</code></strong><strong> 실행 </strong><strong>&#91; 권장 ❌ &#93;</strong>

---

<a id="1c3eda9b0fe181989ba8d69b1031ad63"></a>

Dockerfile 안에서 &#46;/gradlew build를 실행하는 것도 가능하지만,

<a id="1c3eda9b0fe181cf8b5dd00501b3ed9a"></a>

매번 이미지를 빌드할 때마다 Gradle을 다시 빌드해야 하므로 비효율적이다 &#46;

1. <strong>Dockerfile에서 Gradle 빌드 포함 (비추천)</strong>
    <a id="1c3eda9b0fe181e29a88e7aebf79807b"></a>

    ```docker
    FROM gradle:8.4-jdk17 AS builder
    WORKDIR /app
    COPY . /app
    RUN ./gradlew build

    FROM openjdk:17-jdk-slim
    WORKDIR /app
    COPY --from=builder /app/build/libs/myapp.jar /app/app.jar
    ENTRYPOINT ["java", "-jar", "/app/app.jar"]
    ```

    - docker build 할 때마다 <strong>Gradle 빌드가 다시 실행됨</strong> (시간 오래 걸림)

    - 캐싱이 깨질 확률 높음
