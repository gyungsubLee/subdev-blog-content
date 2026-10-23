---
order: 4
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 371eda9b-0fe1-8083-89bf-f052ceff844e
title: N8N 호스팅 - docker compose
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 26deda9b-0fe1-8020-9b16-fdc2892a939e
    title: n8n
  - id: 370eda9b-0fe1-80f5-a06a-e13297a970f7
    title: "바이브코딩 + 자동화 풀 패키지: 21개 프로젝트로 내 인생 자동화 (w. n8n x Claude Code)"
  - id: 371eda9b-0fe1-8083-89bf-f052ceff844e
    title: N8N 호스팅 - docker compose
excerpt: "docker compose 파일 yaml services: postgres: image: postgres:16-alpine containername: n8n-postgres restart: unless-stopped environment: POSTGRESUSER: ${POSTGRESUSER:-n8n} POSTGRESPAS"
cover: null
icon: null
notionProperties: {}
schema_version: 1
parent_id: 370eda9b-0fe1-80f5-a06a-e13297a970f7
created: 2026-05-31T01:32:47.748Z
updated: 2026-05-31T01:38:29.090Z
legacy_path: Main/n8n-fdc2892a939e/바이브코딩 + 자동화 풀 패키지- 21개 프로젝트로 내 인생 자동화 (w. n8n-e13297a970f7/N8N 호스팅 - docker compose-f052ceff844e/index.md
legacy_category: n8n
source_url: https://beautiful-college-c84.notion.site/371eda9b0fe1808389bff052ceff844e
---
<a id="371eda9b0fe18011b33dc429acf90529"></a>

## docker compose 파일

<a id="371eda9b0fe1809f9a1fe0b725bb8e63"></a>

```yaml
services:
  postgres:
    image: postgres:16-alpine
    container_name: n8n-postgres
    restart: unless-stopped
    environment:
      POSTGRES_USER: ${POSTGRES_USER:-n8n}
      POSTGRES_PASSWORD: ${POSTGRES_PASSWORD:-n8n_password}
      POSTGRES_DB: ${POSTGRES_DB:-n8n}
    volumes:
      - postgres_data:/var/lib/postgresql/data
    healthcheck:
      test:
        [
          "CMD-SHELL",
          "pg_isready -U ${POSTGRES_USER:-n8n} -d ${POSTGRES_DB:-n8n}",
        ]
      interval: 10s
      timeout: 5s
      retries: 5

  n8n:
    image: docker.n8n.io/n8nio/n8n:latest
    container_name: n8n
    restart: unless-stopped
    ports:
      - "${N8N_PORT:-5678}:5678"
    environment:
      DB_TYPE: postgresdb
      DB_POSTGRESDB_HOST: postgres
      DB_POSTGRESDB_PORT: 5432
      DB_POSTGRESDB_DATABASE: ${POSTGRES_DB:-n8n}
      DB_POSTGRESDB_USER: ${POSTGRES_USER:-n8n}
      DB_POSTGRESDB_PASSWORD: ${POSTGRES_PASSWORD:-n8n_password}
      N8N_HOST: ${N8N_HOST:-localhost}
      N8N_PORT: 5678
      N8N_PROTOCOL: ${N8N_PROTOCOL:-http}
      N8N_SECURE_COOKIE: ${N8N_SECURE_COOKIE:-false}
      WEBHOOK_URL: ${WEBHOOK_URL:-http://localhost:5678/}
      GENERIC_TIMEZONE: ${GENERIC_TIMEZONE:-Asia/Seoul}
      TZ: ${TZ:-Asia/Seoul}
    volumes:
      - n8n_data:/home/node/.n8n
    depends_on:
      postgres:
        condition: service_healthy

volumes:
  n8n_data:
  postgres_data:
```

<details>
<summary>PostgreSQL을 compose에 붙이면, n8n “애플리케이션 자체의 내부 저장소”로 자동 사용</summary>

> ✏️ 
> 
> <a id="371eda9b0fe180efb0dee6b53c5521c1"></a>
> 
> PostgreSQL을 compose에 붙이면, n8n “애플리케이션 자체의 내부 저장소”로 자동 사용된다&#46; 별도로 n8n UI에서 PostgreSQL credential을 만들거나 Postgres node를 붙일 필요 없다&#46;

- compose의 이 환경변수들이 n8n 서버 부팅 시 DB 연결 설정
    <a id="371eda9b0fe180e7b965c300ea099e09"></a>

    ```yaml
    DB_TYPE: postgresdb
    DB_POSTGRESDB_HOST: postgres
    DB_POSTGRESDB_DATABASE: n8n
    DB_POSTGRESDB_USER: n8n
    DB_POSTGRESDB_PASSWORD: n8n_password
    ```

- n8n이 내부적으로 PostgreSQL에 테이블을 만들고 관리
    - workflows

    - credentials 메타데이터 및 암호화된 값

    - executions

    - users / settings

    - tags, variables 등 n8n 운영 데이터

- 비교
    | <strong>용도</strong> | <strong>설정 위치</strong> | <strong>Node/Credential 필요</strong> |
    | --- | --- | --- |
    | n8n 내부 DB로 PostgreSQL 사용 | docker&#45;compose&#46;yml 환경변수 | 필요 없음 |
    | 워크플로우에서 PostgreSQL 조회/쓰기 | n8n UI의 Credential &#43; Postgres node | 필요함 |

</details>
