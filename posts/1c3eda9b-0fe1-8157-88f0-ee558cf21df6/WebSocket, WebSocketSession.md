---
order: 42
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1c3eda9b-0fe1-8157-88f0-ee558cf21df6
title: WebSocket, WebSocketSession
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-81ae-909e-cd1f71740107
    title: Spring ( Java )
  - id: 1c3eda9b-0fe1-812e-b8ac-c13c536efd00
    title: Spring Boot를 활용한 채팅 서비스 만들어보기
  - id: 1c3eda9b-0fe1-8157-88f0-ee558cf21df6
    title: WebSocket, WebSocketSession
excerpt: "WebSocket --- 📖 WebSocket의 통신 방식 1. WebSocket은 HTTP 요청을 통해 핸드셰이크(handshake) 과정을 거쳐 연결 1. 핸드셰이크가 성공하면, HTTP 연결이 업그레이드되어 WebSocket 프로토콜로 전환 1. 이후, 클라이언트와 서버는 양방향 통신을 지속하며 데이터를 주고받음 "
cover: null
icon: null
notionProperties:
  Tags: 추가 - WebSocket,websocket
  상태: 진행 중
schema_version: 1
parent_id: 1c3eda9b-0fe1-812e-b8ac-c13c536efd00
created: 2025-03-27T07:53:11.122Z
updated: 2025-03-27T07:53:11.122Z
legacy_path: Main/Spring ( Java )-cd1f71740107/Spring Boot를 활용한 채팅 서비스 만들어보기-c13c536efd00/WebSocket, WebSocketSession-ee558cf21df6/index.md
legacy_category: Spring ( Java )
source_url: https://beautiful-college-c84.notion.site/1c3eda9b0fe1815788f0ee558cf21df6
---
<a id="1c3eda9b0fe181c58640d91a9179c268"></a>

## WebSocket

---

> 📖 

<details>
<summary><strong>WebSocket의 통신 방식</strong></summary>

1. WebSocket은 HTTP 요청을 통해 <strong>핸드셰이크(handshake)</strong> 과정을 거쳐 연결

1. 핸드셰이크가 성공하면, <strong>HTTP 연결이 업그레이드되어 WebSocket 프로토콜로 전환</strong>

1. 이후, 클라이언트와 서버는 <strong>양방향 통신</strong>을 지속하며 데이터를 주고받음
    - 해당 통신은 <strong><u>하나의 지속적인 TCP 연결</u></strong> 위에서 이루어지며, 기본적으로 <strong><u>상태를 유지</u></strong>한다

</details>

<a id="1c3eda9b0fe18178a2c0d1c3543809e4"></a>

## <strong>WebSocketSession</strong>

> 📖 

<details>
<summary><strong>WebSocketSession</strong></summary>

<a id="1c3eda9b0fe181deb059ce7bc92c76e9"></a>

WebSocket 연결 세션을 나타내는 추상화 클래스이다&#46;

<a id="1c3eda9b0fe181669b8ee732d341a94c"></a>

이 객체를 통해 WebSocket 연결의 상태를 관리하고 메시지를 주고받을 수 있다&#46;

- <strong>주요 기능</strong>
    - <strong>클라이언트 정보 관리&#58; </strong>연결된 클라이언트의 ID, IP 주소, URI 등의 정보 제공

    - <strong>메시지 전송&#58; sendMessage() 메서드를 통해 클라이언트로 데이터 전송</strong>

    - <strong>속성 관리&#58; getAttributes()를 통해 연결된 사용자와 관련된 추가 데이터를 저장하거나 조회 관리</strong>

<a id="1c3eda9b0fe181d5b708df1e96792fa6"></a>

```javascript
String sessionId = session.getId(); // 세션 ID 가져오기
String uri = session.getUri().toString(); // 연결 URI 확인
session.sendMessage(new TextMessage("Welcome!")); // 클라이언트로 메시지 전송
```

</details>

<details>
<summary>🧐 <strong>WebSocketSession?, 세션 기반 통신?</strong></summary>

<a id="1c3eda9b0fe18111a28ef11a619daaed"></a>

WebSocket이 WebSocketSession을 통해 세션 객체를 사용하는 것은 맞지만, <strong>WebSocket 자체가 “세션 기반 통신”이라고 보기에는 정확한 표현이 아니다&#46;</strong>

<a id="1c3eda9b0fe181ab928cf786bba6e4ea"></a>

WebSocket은 기본적으로 <strong>상태를 유지하는 지속적인 연결을 기반으로</strong> 작동한다&#46;

<a id="1c3eda9b0fe1811992a5f40cc8ff6fe7"></a>

WebSocketSession은 HTTP 세션과는 다르게, <strong>WebSocket 연결이 활성화되어 있는 동안에만 유효하다&#46;</strong>

<a id="1c3eda9b0fe181b19c02e30bcf8fb967"></a>

별도의 세션 ID를 필요로 하지 않으며, 연결 자체가 상태를 나타낸다&#46;

</details>
