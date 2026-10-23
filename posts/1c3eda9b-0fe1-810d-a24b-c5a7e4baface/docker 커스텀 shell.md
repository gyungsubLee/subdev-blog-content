---
order: 17
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1c3eda9b-0fe1-810d-a24b-c5a7e4baface
title: docker 커스텀 shell
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-817c-b119-d6a1706fbaf8
    title: 대규모 시스템 설계
  - id: 1c3eda9b-0fe1-8191-9188-e28e651123f1
    title: RabbitMQ를 이용한 비동기 아키텍처
  - id: 1c3eda9b-0fe1-810d-a24b-c5a7e4baface
    title: docker 커스텀 shell
excerpt: 'start.sh: gradle build + docker compose 실행 docker !/bin/bash 현재 스크립트가 위치한 디렉토리로 이동 (어디서 실행해도 정상 동작) cd "$(dirname "$0")" echo "🔨 Gradle Build 시작..." ./gradlew clean build -x test '
cover: null
icon: null
notionProperties:
  Tags: 추가
  상태: 완료
schema_version: 1
parent_id: 1c3eda9b-0fe1-8191-9188-e28e651123f1
created: 2025-03-27T07:47:43.050Z
updated: 2025-03-27T07:47:43.050Z
legacy_path: Main/대규모 시스템 설계-d6a1706fbaf8/RabbitMQ를 이용한 비동기 아키텍처-e28e651123f1/docker 커스텀 shell-c5a7e4baface/index.md
legacy_category: 대규모 시스템 설계
source_url: https://beautiful-college-c84.notion.site/1c3eda9b0fe1810da24bc5a7e4baface
---
<a id="1c3eda9b0fe181ceb968eb5626801600"></a>

### <code>start&#46;sh</code>&#58; gradle build &#43; docker compose 실행

<a id="1c3eda9b0fe18191b1b7cf0c2084527b"></a>

```docker
#!/bin/bash

# 현재 스크립트가 위치한 디렉토리로 이동 (어디서 실행해도 정상 동작)
cd "$(dirname "$0")"

echo "🔨 Gradle Build 시작..."
./gradlew clean build -x test || { echo "❌ Gradle Build 실패!"; exit 1; }

echo "🚀 Docker Compose 실행..."
docker compose up -d --build

echo "📋 Docker compose ps 실행..."
docker compose ps

# 실행 전  권한 부여 필요
# chmod +x start.sh

# 실행
# ./start.sh
```

<a id="1c3eda9b0fe18169b7b2e7c7ac33b43d"></a>

### <code>restart&#46;sh</code>&#58; compose 종료  &#43; gradle build &#43; compose 재실행

<a id="1c3eda9b0fe181e9baebd5f7c33596c5"></a>

```docker
#!/bin/bash

# 현재 스크립트가 위치한 디렉토리로 이동 (어디서 실행해도 정상 동작)
cd "$(dirname "$0")"

# 현재 실행 중인 컨테이너 종료
echo "🔨 compose 종료..."
docker compose down || { echo "❌ compose 종료 실패!"; exit 1; }

# start.sh 실행
echo "🔨 compose 재실행..."
./start.sh


# 실행 전  권한 부여 필요
# chmod +x restart.sh

# 실행 cmd
# ./restart.sh
```
