---
order: 1
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 2a0eda9b-0fe1-80df-8885-d4c8d7e98d67
title: N8N 호스팅
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 26deda9b-0fe1-8020-9b16-fdc2892a939e
    title: n8n
  - id: 2a0eda9b-0fe1-8056-b9aa-f1e83985284b
    title: 수익형 AI Agent n8n 전문가 강의, 블로그·쇼츠 자동화
  - id: 2a0eda9b-0fe1-80df-8885-d4c8d7e98d67
    title: N8N 호스팅
excerpt: '도커 이미지 기반 로컬 환경 빌드 - compose.yml 파일 생성 bash services: n8n: image: docker.n8n.io/n8nio/n8n containername: n8n ports: - "5678:5678" volumes: - n8ndata:/home/node/.n8n restart: unless'
cover: null
icon: null
notionProperties: {}
schema_version: 1
parent_id: 2a0eda9b-0fe1-8056-b9aa-f1e83985284b
created: 2025-11-03T10:32:39.040Z
updated: 2025-11-03T11:24:21.773Z
legacy_path: Main/n8n-fdc2892a939e/수익형 AI Agent n8n 전문가 강의, 블로그·쇼츠 자동화-f1e83985284b/N8N 호스팅-d4c8d7e98d67/index.md
legacy_category: n8n
source_url: https://beautiful-college-c84.notion.site/2a0eda9b0fe180df8885d4c8d7e98d67
---
<a id="2a0eda9b0fe18049ad56c32b45a919f0"></a>

### 도커 이미지 기반 로컬 환경 빌드

- <code>compose&#46;yml</code> 파일 생성
    <a id="2a0eda9b0fe180c1bd3eda1f80fce1b4"></a>

    ```bash
    services:
      n8n:
        image: docker.n8n.io/n8nio/n8n
        container_name: n8n
        ports:
          - "5678:5678"
        volumes:
          - n8n_data:/home/node/.n8n
        restart: unless-stopped

    volumes:
      n8n_data:

    ```

- docker compose 실행
    <a id="2a0eda9b0fe180cd9a20ef70d69f25df"></a>

    ```bash
    docker compose up -d
    ```

- n8n 이미지 실행 확인
    - docker cli 확인
        <a id="2a0eda9b0fe18078953acf4dd3adcff6"></a>

        ```bash
        docker compsoe ps
        ```

        ![](de3587a2e643bc86.webp)

    - docker desktop 확인
        ![](7f140acdfd979b94.webp)
