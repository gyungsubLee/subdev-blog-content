---
order: 4
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1c3eda9b-0fe1-8191-9188-e28e651123f1
title: RabbitMQ를 이용한 비동기 아키텍처
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-817c-b119-d6a1706fbaf8
    title: 대규모 시스템 설계
  - id: 1c3eda9b-0fe1-8191-9188-e28e651123f1
    title: RabbitMQ를 이용한 비동기 아키텍처
excerpt: /icons/push-pingreen.svg [인프런] RabbitMQ를 이용한 비동기 아키텍처 한방에 해결하기 - 정리본 reference ‣ ‣ ‣ ‣ ‣ ‣ ‣ Source Code RabbitMQprac RabbitMQ 개요, 비동기 아키텍처 RabbitMQ 설치 AMQP의 이해 주요 용어, Exchage 기본 비
cover: aff6944ba2f49bd8.jpg
icon: fbc5abdb68adb4ef.png
notionProperties: {}
schema_version: 1
parent_id: 1c3eda9b-0fe1-817c-b119-d6a1706fbaf8
created: 2025-03-27T07:47:12.309Z
updated: 2025-03-27T14:40:07.407Z
legacy_path: Main/대규모 시스템 설계-d6a1706fbaf8/RabbitMQ를 이용한 비동기 아키텍처-e28e651123f1/index.md
legacy_category: 대규모 시스템 설계
source_url: https://beautiful-college-c84.notion.site/1c3eda9b0fe181919188e28e651123f1
---
> /icons/push-pin_green.svg 
> 
> <a id="1c3eda9b0fe181018040efde14477b0d"></a>
> 
> &#91;인프런&#93; <strong>RabbitMQ를 이용한 비동기 아키텍처 한방에 해결하기 &#45; 정리본</strong>
> 
> <details>
> <summary>reference</summary>
> 
> <a id="1c3eda9b0fe1813c8dc6d7865a2ccadc"></a>
> 
>  ‣
> 
> <a id="1c3eda9b0fe18193aa4cf67746b69702"></a>
> 
> ‣
> 
> <a id="1c3eda9b0fe1814c95c1cb611ba37751"></a>
> 
> ‣
> 
> <a id="1c3eda9b0fe1817da051e02010984cfb"></a>
> 
> ‣
> 
> <a id="1c3eda9b0fe1819f873bd618692e5db3"></a>
> 
> ‣
> 
> <a id="1c3eda9b0fe181c791ead6b69cde73a4"></a>
> 
> ‣<br>‣
> 
> </details>

<a id="1c3eda9b0fe18139bb28e4e6bb759881"></a>

### Source Code

[RabbitMQ_prac](https://github.com/gyungsubLee/RabbitMQ_prac)

[RabbitMQ 개요, 비동기 아키텍처](#/post/1c3eda9b-0fe1-8129-856c-d0370af4a055)

[RabbitMQ 설치](#/post/1c3eda9b-0fe1-81bf-98f6-c1bdc362b705)

[AMQP의 이해](#/post/1c3eda9b-0fe1-81fc-8ffc-ed6c8c0ee92c)

[주요 용어, Exchage](#/post/1c3eda9b-0fe1-8137-a6ea-c9f4140c81aa)

[기본 비동기 메세지 전송](#/post/1c3eda9b-0fe1-81a0-be8e-cdda13740753)

[Consumer 간 작업 분배 - Work Queue ( 경쟁 소비자 패턴 )](#/post/1c3eda9b-0fe1-81a5-81de-c1417c38c7b6)

[Consumer 간 작업 분배 - Work Queue](#/post/1c3eda9b-0fe1-819f-ba52-cabcf5ec598f)

[Publish / Subscribe 모델](#/post/1c3eda9b-0fe1-81c9-9c67-f04287601241)

[Pub/Sub 모델을 이용한 실시간 알림 ( WebSocket, STOMP 이용)](#/post/1c3eda9b-0fe1-819d-8913-d076464598f9)

[Pub/Sub 모델을 이용한 뉴스레터 구독 예제](#/post/1c3eda9b-0fe1-8128-b927-eaa90390ab5b)

[Routing 모델 및 Log 수집: Direct, Topic](#/post/1c3eda9b-0fe1-81c6-8678-c31e7955aa3f)

[DeadLetterQueue, DeadLetterExchange  이해](#/post/1c3eda9b-0fe1-8110-89a1-ff7d7b058a42)

[DeadLetterQueue를 이용한 재처리](#/post/1c3eda9b-0fe1-81f1-b8c2-c712ce1df7a5)

[RetryTemplate을 이용한 DeadLetter 재처리](#/post/1c3eda9b-0fe1-8193-872c-c4bfbdff6f90)

[Retry 설정을 통한 DeadLetter 재처리](#/post/1c3eda9b-0fe1-8170-afe8-e701ce6038b9)

[DB 연동, RabbitMQ의 Transaction 처리](#/post/1c3eda9b-0fe1-81b1-813d-d572d9b86b80)

[1. DB 연동 메시지 큐의 Transaction  처리  [ 권장 ❌ ]](#/post/1c3eda9b-0fe1-810b-8930-d3bd4910e4b5)

[2. Publisher-confirms을 이용한 트랜잭션 처리](#/post/1c3eda9b-0fe1-81a9-9e3d-e4f60dd1e2f7)

[트랜잭션 처리의 확장 - TCC의 이해](#/post/1c3eda9b-0fe1-814e-b000-d40d6c269abe)

[Spring AMQP (Spring for RabbitMQ),  Spring Cloud Stream for RabbitMQ  비교](#/post/1c3eda9b-0fe1-8156-a161-c9c49bbce8ff)

[docker 커스텀 shell](#/post/1c3eda9b-0fe1-810d-a24b-c5a7e4baface)

[rabbitmqctl 로 exchage, queue, binding 정보 확인](#/post/1c3eda9b-0fe1-8142-8dac-f241058a4e9c)

[롬복 사용 시, 인텔리제이 기본 설정](#/post/1c3eda9b-0fe1-8173-84dc-da309c275855)

[스프링 h2 연동](#/post/1c3eda9b-0fe1-817a-a71a-d45979eaa48e)

[로깅 - Debug 레벨로 기록 및 확인](#/post/1c3eda9b-0fe1-81fb-aea0-dffb779255c8)

[Pub/Sub 과 Producer / consumer의 차이점](#/post/1c3eda9b-0fe1-81da-ae4d-c38a21156a23)
