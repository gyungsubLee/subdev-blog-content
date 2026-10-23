---
order: 4
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 24beda9b-0fe1-8077-86e2-fc150d2dd630
title: Gateways
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 226eda9b-0fe1-802b-a035-c3a886768c4d
    title: Nest.js
  - id: 227eda9b-0fe1-80e1-8036-d4fc3e106054
    title: 탄탄한 백엔드 NestJS, 기초부터 심화까지 ( 중지 )
  - id: 24beda9b-0fe1-8077-86e2-fc150d2dd630
    title: Gateways
excerpt: "[Documentation | NestJS - A progressive Node.js framework]() 📖 NestJS에서 말하는 Gateway @WebSocketGateway()가 붙은 클래스를 의미한다. HTTP, WebSocket, Microservices를 동일한 프로그래밍 모델(DI, 🧐 ”동일한 프로그"
cover: null
icon: null
notionProperties: {}
schema_version: 1
parent_id: 227eda9b-0fe1-80e1-8036-d4fc3e106054
created: 2025-08-10T04:08:35.151Z
updated: 2025-09-06T12:14:34.747Z
legacy_path: Main/Nest.js-c3a886768c4d/탄탄한 백엔드 NestJS, 기초부터 심화까지 ( 중지 )-d4fc3e106054/Gateways-fc150d2dd630/index.md
legacy_category: Nest.js
source_url: https://beautiful-college-c84.notion.site/24beda9b0fe1807786e2fc150d2dd630
---
[Documentation &#124; NestJS &#45; A progressive Node&#46;js framework]()

> 📖 
> 
> <a id="24beda9b0fe180ebb55df6be138f6a0a"></a>
> 
> NestJS에서 말하는 Gateway <code>&#64;WebSocketGateway()</code>가 붙은 클래스를 의미한다&#46; 
> 
> <a id="24beda9b0fe180ba83e4de8ced018a51"></a>
> 
> HTTP, WebSocket, Microservices를 동일한 프로그래밍 모델(DI, 

<details>
<summary>🧐 ”동일한 프로그래밍 모델”의 의미</summary>

<a id="24beda9b0fe180a48fade10d3f1c605a"></a>

<code>Nest</code>는 세 가지 서로 다른 플랫폼을 지원한다&#46; 

1. <code>HTTP</code>&#58; <strong><code>&#64;Controller()</code></strong><strong>, </strong><strong><code>&#64;Get()</code></strong><strong>, </strong><strong><code>&#64;Post()</code></strong><strong> …</strong>

1. <code>WebSocket</code>&#58;<strong> </strong><strong><code>&#64;WebSocketGateway()</code></strong><strong>, </strong><strong><code>&#64;SubscribeMessage()</code></strong><strong> …</strong>

1. <code>Microservice</code>&#58; <strong><code>&#64;MessagePettern()</code></strong><strong> …</strong>

<a id="24beda9b0fe1801e8522d5efd7d6f9df"></a>

위 세 플랫폼은 네트워크 프로토콜, 라이프사이클, 라이브러리가 다르지만, NestJS는 이를 추상화하여 동일한 코딩 모델을 제공한다&#46; 

| <strong>기능</strong> | <strong><code>HTTP 컨트롤러</code></strong> | <strong><code>WS Gateway</code></strong> | <strong><code>Microservice</code></strong> |
| --- | --- | --- | --- |
| <code>DI(의존성 주입)</code> | ✅ | ✅ | ✅ |
| <code>데코레이터 기반 라우팅</code> | ✅ | ✅ | ✅ |
| <code>Pipe(검증/변환)</code> | ✅ | ✅ | ✅ |
| <code>Guard(권한 체크)</code> | ✅ | ✅ | ✅ |
| <code>Interceptor(로깅/변환)</code> | ✅ | ✅ | ✅ |
| <code>Filter(예외 처리)</code> | ✅ | ✅ | ✅ |

- <strong>전송 방식만 다를 뿐</strong><u> 개발자가 느끼는 코드 구조는 거의 같</u><strong>게</strong> Nest에서 추상화하여 제공한다&#46; 

<a id="24beda9b0fe18005b2b5c7a0ab244fe2"></a>

### 정리

- HTTP, WS, Microservice에서도 DI, 데코레이터, 파이프, 가드, 인터셉터, 필터를 똑같이 적용 가능

- <strong>Gateway 메서드 실행 전후에 Guard, Interceptor, Filter가 끼어드는 구조</strong>

<a id="24beda9b0fe180478bbdfab1c27e7c97"></a>

<br><br>

</details>

<a id="24beda9b0fe180d4b631ff8589f5e949"></a>

### <code>&#64;WebSocketGateway()</code>
