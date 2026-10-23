---
order: 6
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1c3eda9b-0fe1-818d-8a43-c6b917e3ee6d
title: Transaction Manager를 활용한 WebSocket 경계 설정
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-81ae-909e-cd1f71740107
    title: Spring ( Java )
  - id: 1c3eda9b-0fe1-812e-b8ac-c13c536efd00
    title: Spring Boot를 활용한 채팅 서비스 만들어보기
  - id: 1c3eda9b-0fe1-818d-8a43-c6b917e3ee6d
    title: Transaction Manager를 활용한 WebSocket 경계 설정
excerpt: 일반적인 HTTP 요청 같은 경우, 기본적으로 커넥션을 일관성 있게 처리할 수 있다. 즉, 경계가 명확하다. 그러나 웹소캣의 경우는 하나의 커넥션 즉, 세션을 하나에 계속 공유하면서 사용하기 때문에 경계가 명확하지 않는 경우가 있다. - 기본 WebSocket, STOMP 동일 따라서 웹소캣 연결 중, chat에 대한 내
cover: null
icon: null
notionProperties:
  상태: 진행 중
schema_version: 1
parent_id: 1c3eda9b-0fe1-812e-b8ac-c13c536efd00
created: 2025-03-27T07:53:11.125Z
updated: 2025-03-27T07:53:11.125Z
legacy_path: Main/Spring ( Java )-cd1f71740107/Spring Boot를 활용한 채팅 서비스 만들어보기-c13c536efd00/Transaction Manager를 활용한 WebSocket 경계 설정-c6b917e3ee6d/index.md
legacy_category: Spring ( Java )
source_url: https://beautiful-college-c84.notion.site/1c3eda9b0fe1818d8a43c6b917e3ee6d
---
<a id="1c3eda9b0fe18169bcc6e08011d475b4"></a>

일반적인 HTTP 요청 같은 경우, 기본적으로 커넥션을 일관성 있게 처리할 수 있다&#46;

<a id="1c3eda9b0fe1819bbbc2e2d7736d7275"></a>

즉, 경계가 명확하다&#46; 

<a id="1c3eda9b0fe1818bb2a7d8513d3e070c"></a>

그러나 웹소캣의 경우는 하나의 커넥션 즉, 세션을 하나에 계속 공유하면서 사용하기 때문에 <br>경계가 명확하지 않는 경우가 있다&#46; 

- 기본 WebSocket, STOMP  동일

<a id="1c3eda9b0fe18121afa1e25a0737eaa4"></a>

따라서 웹소캣 연결 중, chat에 대한 내용을 DB에 저장하는 Save 로직이 정상적으로 동작하지 않는다&#46;

<a id="1c3eda9b0fe181a39260d730302cda05"></a>

또한 이를 flush를 해서 해결한다고 한다면, 에러가 발생된다&#46; 

- flush는 기본적으로 JPA에서 다루고자 하는 트랜잭션이 담겨있어야 하는데, <br>웹소캣에서는 트랜잭션이 담겨있지 않아 에러가 발생된다&#46; 

- 웹소캣은 하나의 통신으로 공유를 하기 때문에, 경계가 명확하지 않아 JPA에서 일반적으로 트랜잭션을 잘 인식하지 못하고 잘 넣어주지 못한다&#46; 

<a id="1c3eda9b0fe1815f9963fe3cd9cbece4"></a>

커스텀하게 MySQL config를 구현하면 스프링에서 자동으로 Transaction 처리를 해주지 않는다&#46; 

<a id="1c3eda9b0fe1812897ddd3f2732dfb6c"></a>

이를, 가능케 하기 위해서는 

<a id="1c3eda9b0fe1819ea143e4708a300656"></a>

// 엔티티를 정확하게 넣어준다&#46;
