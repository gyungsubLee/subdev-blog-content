---
order: 8
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 21ceda9b-0fe1-80fc-81eb-fec44dbfee1d
title: "[ 추가 ]  Netty 와 이벤트 루프 동작 원리"
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-81ae-909e-cd1f71740107
    title: Spring ( Java )
  - id: 210eda9b-0fe1-8058-abd9-eceec7820379
    title: Spring WebFlux + LLM 실전 구현
  - id: 21ceda9b-0fe1-80fc-81eb-fec44dbfee1d
    title: "[ 추가 ]  Netty 와 이벤트 루프 동작 원리"
excerpt: "Netty --- 📖 Netty는 Java NIO( Non-blocking I/O )를 기반으로 동작하는 비동기 이벤트 기반 네트워크 프레임워크이다. 내부적으로 EventLoop 와 Selector, Channel, Pipeline 등의 구조로 동작한다. - 주요 특징: Non-blocking I/O, Selector "
cover: null
icon: null
notionProperties:
  상태: 진행 중
schema_version: 1
parent_id: 210eda9b-0fe1-8058-abd9-eceec7820379
created: 2025-06-24T15:37:33.012Z
updated: 2025-06-28T08:20:18.176Z
legacy_path: Main/Spring ( Java )-cd1f71740107/Spring WebFlux + LLM 실전 구현-eceec7820379/[ 추가 ]  Netty 와 이벤트 루프 동작 원리-fec44dbfee1d/index.md
legacy_category: Spring ( Java )
source_url: https://beautiful-college-c84.notion.site/21ceda9b0fe180fc81ebfec44dbfee1d
---
<a id="21ceda9b0fe180cbb55ed63a87b4474d"></a>

## <strong>Netty</strong>

---

> 📖 
> 
> <a id="21ceda9b0fe180169f37ca6f4f776fad"></a>
> 
> <code>Netty</code>는 <strong><u>Java NIO( Non&#45;blocking I/O )를 기반</u></strong>으로 동작하는 <strong><u>비동기 이벤트 기반 네트워크 프레임워크</u></strong>이다&#46;  
> 
> <a id="21ceda9b0fe1808c841cc9ee215a8567"></a>
> 
> 내부적으로 EventLoop 와 Selector, Channel, Pipeline 등의 구조로 동작한다&#46;
> 
> - 주요 특징&#58; <code>Non&#45;blocking I/O</code>, <code>Selector 기반 multiplexing</code>, <code>이벤트 기반 </code>

<a id="21ceda9b0fe180b89d42c554de390a59"></a>

### <strong>1&#46; Netty의 이벤트 루프 동작 원리 (EventLoop &#43; Selector)</strong>

<a id="21ceda9b0fe1801b93b9d8bc7e24917b"></a>

```java
[OS 커널]
  └── epoll/kqueue/IOCP 등으로 이벤트 대기
       └── 완료된 이벤트 저장

[Netty]
  └── EventLoop (스레드)
       ├── Selector.select()
       ├── 이벤트 조회
       └── 각 채널에 등록된 작업 실행 (ChannelHandler 호출)
```

<a id="21ceda9b0fe18041b7a4ca011da79236"></a>

<strong><br></strong>

<a id="21ceda9b0fe180249bc6f316cafd8687"></a>

### <strong>2&#46;  단계별 동작 흐름</strong>

1. 서버 시작
    - Netty는 서버 소켓에 대해 ServerSocketChannel을 생성하고, 이를 Selector에 등록한다&#46; 

    - 여러 EventLoop가 생성되고, 각 스레ㅐ드는 하나의 Selector를 관리한다&#46; 

1. 클라이언트 연결/요청
    - 클라이언트가 서버에 요청을 보낼 때, OS 커널은 해당 소켓에 이벤트가 발생했음을 epoll 등의 방식으로 감지한다&#46;

    - 이 이벤트는 OS 커널의 이벤트 큐에 쌓인다&#46; 
        - <strong>여기서 “OS가 쌓아둔다”는 표현은 정확히는 커널이 이벤트 상태를 감지하고 Selector가 이를 조회 가능하게 만든다는 뜻이다&#46;</strong>

1. <strong>Netty의 EventLoop 작동</strong>
    <a id="21ceda9b0fe1800d9860fcbb90717243"></a>

    ```java
    while (true) {
        int readyChannels = selector.select();  // 💡 이벤트가 올 때까지 blocking or timeout 설정
        Set<SelectionKey> keys = selector.selectedKeys(); // 💡 이벤트 모음 (읽기, 쓰기 등)
        for (SelectionKey key : keys) {
            if (key.isReadable()) {
                // Read 이벤트 처리 (예: channel.pipeline().fireChannelRead())
            }
            if (key.isAcceptable()) {
                // 새 연결 수락 및 워크 채널 등록
            }
            // 기타 처리 ...
        }
        keys.clear(); // 처리 완료한 키 제거
    }
    ```

    1. <code>selector&#46;select()</code> 호출 → OS 커널의 이벤트 큐에서 발생한 이벤트가 있는지 확인

    1. 이벤트 존재 → 등록된 <code>ChannelHandler</code>(read/write 등)를 실행

    1. 이후 다음 이벤트를 기다리기 위해 루프 반복

<a id="21ceda9b0fe18052be12f8790dae3d98"></a>

### 3&#46; 실무 팁

- Netty는 <strong>적은 수의 스레드(EventLoop)</strong> 로 수천 개의 클라이언트를 처리할 수 있다&#46;

- 하지만, <strong><u>EventLoop 내에서 블로킹 작업(예&#58; DB 쿼리, 파일 I/O 등)</u></strong><strong>은 절대 피해야</strong> 한다&#46;<br>이는 <strong>해당 스레드 전체가 멈추는 결과</strong>를 낳기 때문입니다&#46;

- <strong><u>블로킹 작업</u></strong>은 <strong>EventLoopGroup과는 분리</strong>된 <strong>Worker ThreadPool 또는 TaskExecutor에서 처리</strong>하는 것이 권장된다&#46;
