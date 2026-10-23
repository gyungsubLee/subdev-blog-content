---
order: 40
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 22aeda9b-0fe1-80ef-8f53-faed71ec3bf9
title: "[ 의문점 ] Node.js, Netty(Spring WebFlux) 비교"
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 226eda9b-0fe1-802b-a035-c3a886768c4d
    title: Nest.js
  - id: 227eda9b-0fe1-80e1-8036-d4fc3e106054
    title: 탄탄한 백엔드 NestJS, 기초부터 심화까지 ( 중지 )
  - id: 22aeda9b-0fe1-80ef-8f53-faed71ec3bf9
    title: "[ 의문점 ] Node.js, Netty(Spring WebFlux) 비교"
excerpt: "목차 - 공통점: 이벤트 루프 기반 비동기 I/O 모델 - 차이점: 스레드 모델과 이벤트 루프 - 정리 - Reference 💬 Node.js와 Netty(Spring WebFlux)는 둘 다 이벤트 루프 기반이지만 스레드 수, 컨텍스트 스위칭 전략, 실행 모델에서 중요한 차이점이 있다. 공통점: 이벤트 루프 기반 비동"
cover: null
icon: 🧐
notionProperties: {}
schema_version: 1
parent_id: 227eda9b-0fe1-80e1-8036-d4fc3e106054
created: 2025-07-08T14:32:39.621Z
updated: 2025-07-10T04:17:10.035Z
legacy_path: Main/Nest.js-c3a886768c4d/탄탄한 백엔드 NestJS, 기초부터 심화까지 ( 중지 )-d4fc3e106054/[ 의문점 ] Node.js, Netty(Spring WebFlux) 비교-faed71ec3bf9/index.md
legacy_category: Nest.js
source_url: https://beautiful-college-c84.notion.site/22aeda9b0fe180ef8f53faed71ec3bf9
---
> 
> 
> <a id="22aeda9b0fe1813e8564ea4975e72290"></a>
> 
> <strong>목차</strong>
> 
> - [공통점: 이벤트 루프 기반 비동기 I/O 모델](#22aeda9b0fe1806bbc25d1338a41662f)
> - [차이점: 스레드 모델과 이벤트 루프 ](#22aeda9b0fe180718314f8d04afc98ca)
> - [정리](#22beda9b0fe180438245cf46991b4d81)
> - [Reference](#22beda9b0fe18048be25fe4d97dc8770)

> 💬 
> 
> <a id="22aeda9b0fe180d1aad1c4d67b3dd24c"></a>
> 
> <code>Node&#46;js</code>와 <code>Netty</code>(Spring WebFlux)는 둘 다 <strong><u>이벤트 루프 기반</u></strong>이지만 <strong><u>스레드 수, 컨텍스트 스위칭 전략, 실행 모델</u></strong>에서 중요한 차이점이 있다&#46;

<a id="22aeda9b0fe1806bbc25d1338a41662f"></a>

### 공통점&#58; <strong>이벤트 루프 기반 비동기 I/O 모델</strong>

> ✏️ 
> 
> <a id="22aeda9b0fe18099a3b8c261428d27eb"></a>
> 
> 둘 다 <strong>블로킹 I/O 문제 해결</strong>, <strong>컨텍스트 스위칭 최소화</strong>, <strong>리소스 효율성 극대화</strong>라는 동일한 목적을 가진다&#46;

| <strong>항목</strong> | <strong><code>Node&#46;js</code></strong> | <strong><code>Netty</code></strong><strong> ( Spring WebFlux )</strong> |
| --- | --- | --- |
| 핵심 실행 모델 | 싱글 이벤트 루프 <br>(단일 스레드) | 멀티 이벤트 루프 <br>(멀티 스레드) |
| 동작 원리 | Non&#45;blocking, <br>event&#45;driven | Non&#45;blocking, reactive <br>(Reactor 기반) |
| 목적 | I/O 처리 병목 해소 | 블로킹 자원을 줄이고 고성능 처리 |
| 기반 기술 | libuv <br>(C 기반 이벤트 루프) | Netty <br>(Java NIO 기반) |

<a id="22aeda9b0fe180718314f8d04afc98ca"></a>

### <strong>차이점&#58; 스레드 모델과 이벤트 루프 </strong>

> <strong>Node&#46;js</strong>

> ✏️ 
> 
> <a id="22beda9b0fe1807dbc05e0e75a18f801"></a>
> 
> <code>Node&#46;js</code> 자체는 “<strong><u>CPU 코어 수만큼 스레드를 사용하지는 않</u></strong>는다
> 
> <a id="22beda9b0fe1809387fec4acc0d29c90"></a>
> 
> 하지만, <strong>멀티 프로세스나 cluster 모드로 확장 가능하다&#46;</strong>
> 
> - <strong><u>단일 이벤트 루프 스레드</u></strong> &#43; <strong><u>필요 시 libuv의 Worker Thread Pool 사용</u></strong>

- JavaScript 코드 자체는 1개의 스레드에서 실행됨
    - 기본적으로는 <strong>메인 스레드 1개</strong>만 사용

- CPU 코어 수와 관계없이 Node&#46;js는 기본적으로 하나의 이벤트 루프만 실행함

- Worker Threads, child&#95;process, clustrer, pm2 등을 통해 멀티 프로세싱 가능
    - <strong>libuv의 worker pool</strong>은 내부적으로 최대 4개까지 작업을 병렬 처리 가능 (디폴트 값)
        <a id="22beda9b0fe18024a06cd7400cf8a079"></a>

        ```java
        process.env.UV_THREADPOOL_SIZE = 8; // 수동 설정 가능
        ```

> <strong> Netty ( Spring WebFlux )</strong>

- 기본적으로 Netty는 CPU 코어 수만큼 이벤트 루프 스레드(NioEventLoopGrop)를 생성
    <a id="22beda9b0fe1800c8a76d0a706e56ceb"></a>

    ```javascript
    new NioEventLoopGroup() // 디폴트: Runtime.getRuntime().availableProcessors()
    ```

    - ex) CPU 8 코어 → 8 개의 이벤트 루프 스레드로 병렬 요청 처리 가능

-  요청&#45;응답 자체는 <strong>Non&#45;blocking</strong>이지만, CPU&#45;bound 작업을 처리할 <strong>Scheduler/Worker 쓰레드</strong>는 별도로 동작함
    <a id="22beda9b0fe180f399cdd9e0287cfe07"></a>

    ```java
    Schedulers.boundedElastic() // 블로킹 연산 처리용 스레드 풀
    ```

    - 추가적인 boundedElastic, parallel, immediate 같은 Scheduler를 통해 <strong>추가적인 쓰레드 풀</strong>에서 작업 수행 가능

<a id="22beda9b0fe180438245cf46991b4d81"></a>

### 정리

| <strong>질문</strong> | <strong>답변</strong> |
| --- | --- |
| Node&#46;js는 Netty와 구조가 비슷한가? | ✅ 둘 다 이벤트 루프 기반의 Non&#45;blocking I/O 구조이다&#46; |
| Node&#46;js도 CPU 수만큼 스레드를 사용하나? | ❌ 기본적으로는 하나의 이벤트 루프 스레드만 사용한다&#46; (멀티 프로세싱은 수동 구성 필요) |
| Netty는 CPU 수만큼 스레드를 사용하나? | ✅ 기본적으로 Runtime&#46;getRuntime()&#46;availableProcessors() 수만큼의 이벤트 루프 스레드 사용 |
| 컨텍스트 스위칭 비용을 줄이기 위한 새로운 패러다임인가? | ✅  Netty, Node&#46;js 모두 전통적인 Thread&#45;per&#45;request 방식의 대안으로 등장 |

<a id="22beda9b0fe18048be25fe4d97dc8770"></a>

### Reference

[Node&#46;js — The Node&#46;js Event Loop]()

[Spring WebFlux &#58;&#58; Spring Framework]()

[Cluster &#124; Node&#46;js v24&#46;3&#46;0 Documentation]()
