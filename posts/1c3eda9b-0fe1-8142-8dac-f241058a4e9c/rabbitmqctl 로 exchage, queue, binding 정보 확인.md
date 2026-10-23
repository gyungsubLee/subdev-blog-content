---
order: 18
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1c3eda9b-0fe1-8142-8dac-f241058a4e9c
title: rabbitmqctl 로 exchage, queue, binding 정보 확인
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-817c-b119-d6a1706fbaf8
    title: 대규모 시스템 설계
  - id: 1c3eda9b-0fe1-8191-9188-e28e651123f1
    title: RabbitMQ를 이용한 비동기 아키텍처
  - id: 1c3eda9b-0fe1-8142-8dac-f241058a4e9c
    title: rabbitmqctl 로 exchage, queue, binding 정보 확인
excerpt: "- docker 실행 시, rabbitmq 컨테이너 내부 bash 접속 bash docker exec -it [RabbitMQ 컨테이너 ID] bash - exchange 확인 bash rabbitmqctl listqueues - queue 확인 bash rabbimqctl listqueues - binding 정보 확인"
cover: null
icon: null
notionProperties:
  Tags: 추가
  상태: 완료
schema_version: 1
parent_id: 1c3eda9b-0fe1-8191-9188-e28e651123f1
created: 2025-03-27T07:47:43.050Z
updated: 2025-03-27T07:47:43.050Z
legacy_path: Main/대규모 시스템 설계-d6a1706fbaf8/RabbitMQ를 이용한 비동기 아키텍처-e28e651123f1/rabbitmqctl 로 exchage, queue, binding 정보 확인-f241058a4e9c/index.md
legacy_category: 대규모 시스템 설계
source_url: https://beautiful-college-c84.notion.site/1c3eda9b0fe181428dacf241058a4e9c
---
- docker 실행 시, rabbitmq 컨테이너 내부 bash 접속
    <a id="1c3eda9b0fe181188056c843c68fe5dc"></a>

    ```bash
    docker exec -it [RabbitMQ 컨테이너 ID] bash
    ```

- exchange 확인
    <a id="1c3eda9b0fe18189bfcce74be90282d6"></a>

    ```bash
    rabbitmqctl list_queues
    ```

    ![](3389c1dab1b068a7.webp)

- queue 확인
    <a id="1c3eda9b0fe181b08ad4df2f44200699"></a>

    ```bash
    rabbimqctl list_queues
    ```

    ![](b654437ad5c7e685.webp)

- binding 정보 확인
    <a id="1c3eda9b0fe181a49bc4cbd0da96dc5a"></a>

    ```bash
    rabbitmqctl list_exchagnes
    ```

    ![](a712f2212a0949d2.webp)
