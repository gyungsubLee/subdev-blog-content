---
order: 3
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1c3eda9b-0fe1-812e-b8ac-c13c536efd00
title: Spring Boot를 활용한 채팅 서비스 만들어보기
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-81ae-909e-cd1f71740107
    title: Spring ( Java )
  - id: 1c3eda9b-0fe1-812e-b8ac-c13c536efd00
    title: Spring Boot를 활용한 채팅 서비스 만들어보기
excerpt: "📌 Sring Boot를 활용한 채팅 서비스 만들어보기 - ‣ - 주요 기술: JWT, Web Socket reference ‣ ‣ ‣ ‣ ‣ ‣ ‣ - repository InflearnChattingBasicwithSpring Websocket - 클라이언트로부터 메세지를 받아오는 엔드포인트 설정 - @Message"
cover: null
icon: 986876fc42aafa45.svg
notionProperties: {}
schema_version: 1
parent_id: 1c3eda9b-0fe1-81ae-909e-cd1f71740107
created: 2025-03-27T07:47:13.041Z
updated: 2026-04-04T15:50:35.158Z
legacy_path: Main/Spring ( Java )-cd1f71740107/Spring Boot를 활용한 채팅 서비스 만들어보기-c13c536efd00/index.md
legacy_category: Spring ( Java )
source_url: https://beautiful-college-c84.notion.site/1c3eda9b0fe1812eb8acc13c536efd00
---
> 📌 
> 
> <a id="1c3eda9b0fe18103ab7feb1751b1656e"></a>
> 
> <strong>Sring Boot를 활용한 채팅 서비스 만들어보기</strong>
> 
> - ‣
> 
> - 주요 기술&#58; JWT, Web Socket

<details>
<summary>reference</summary>

<a id="1c3eda9b0fe181e98b69d306875aa10f"></a>

‣

<a id="1c3eda9b0fe181e7ac13f1899e0c63c5"></a>

‣

<a id="1c3eda9b0fe181ce86cde943cede5806"></a>

‣

<a id="1c3eda9b0fe18195aa46d82ed2438d9f"></a>

‣

<a id="1c3eda9b0fe181f38f1eeb4318d88718"></a>

‣

<a id="1c3eda9b0fe1818382d7c3176894a7da"></a>

‣

<a id="1c3eda9b0fe1810da04ff4409dd76864"></a>

‣

</details>

- repository
    [Inflearn_Chatting_Basic_withSpring](https://github.com/gyungsubLee/Inflearn_Chatting_Basic_withSpring)

<details>
<summary>Websocket</summary>

- 클라이언트로부터 메세지를 받아오는 엔드포인트 설정
    - <code>&#64;MessageMapping</code> 

- 목적지 variable  ( = PathVariable )
    - <code>&#64;DestinationVariable</code>

- RequestBody 
    - 생략 

- 구독된 모든 클라이언트에게 브로드캐스트 처리하는 엔드포인트 설정
    - <code>&#64;SubcribeMapping</code>

    - <code>&#64;SendTo</code>

<details>
<summary>ex)</summary>

<a id="1c3eda9b0fe181dab593d74c9aad6188"></a>

```java
@MessageMapping("/chat/message/{from}")
@SendTo("/sub/chat")
public Message receivedMessage(
        @DestinationVariable String from,
				Message msg
) {
    log.info("Message Received -> From: {}, to: {}, msg: {}", from, msg.getTo(), msg.getFrom());
    chatServiceV1.saveChatMessage(msg);
    return msg;
}
```

</details>

</details>

<a id="1c3eda9b0fe18113b579cf61ce532592"></a>

## Chapter

[initializer, dependencies](#/post/1c3eda9b-0fe1-8194-b5d9-c6c8565a13f2)

[yaml을 활용한 서버 환경 관리](#/post/1c3eda9b-0fe1-81fb-a66c-d2c60b668b1d)

[MySQL Transaction Manager Config](#/post/1c3eda9b-0fe1-8175-85df-f9ab42f97167)

[WebMvcConfigurer- CORS](#/post/1c3eda9b-0fe1-817a-accd-e09433b6369d)

[WebSocketConfigurer - WebSocket 설정](#/post/1c3eda9b-0fe1-8175-b16f-d7647ef7fc47)

[Swagger](#/post/1c3eda9b-0fe1-81ec-be29-c44db50db0a3)

[Entity, Lazy Fetch](#/post/1c3eda9b-0fe1-812a-a16b-e91b90d6c7e9)

[JPA, Service 구성](#/post/1c3eda9b-0fe1-8153-9ed0-da786d166b7b)

[SHA-256을 활용한 Password 해싱](#/post/1c3eda9b-0fe1-817c-91be-eddc56e018ec)

[RumTimeException에 대한 Customizing](#/post/1c3eda9b-0fe1-8161-93c2-ce49012593b1)

[Auth API 기본적인 마무리](#/post/1c3eda9b-0fe1-8105-81cd-e6f6028f68eb)

[JWT - 면접 대비, 기능 개발](#/post/1c3eda9b-0fe1-8183-aec5-e5f08625c8e5)

[JWT 설정 -  factory Annotition 활용](#/post/1c3eda9b-0fe1-817a-a360-c9dc31236d1b)

[JWT Token의 Playload에 값 주입](#/post/1c3eda9b-0fe1-81f1-8791-eda28ca2db22)

[JWT Verity(검증), 에러 핸들링](#/post/1c3eda9b-0fe1-8123-8385-ca5b7350fe48)

[JWT 디코딩 - DecodedJWT](#/post/1c3eda9b-0fe1-815e-a560-d8db8512c098)

[HTTP Protocol에 대한 로직 마무리](#/post/1c3eda9b-0fe1-813d-8232-cb4b21cdc5f4)

[WebSocket 이론](#/post/1c3eda9b-0fe1-810a-ba32-ce4772b66c46)

[Redis를 사용하여 WebSocket 사용자 상태 관리](#/post/1c3eda9b-0fe1-816d-bef6-cf25011b791a)

[TextSocketHandler를 활용한 Raw Level 코드 작성](#/post/1c3eda9b-0fe1-8122-9298-dfb034176370)

[Protocol을 적용하는 WebSocket 및 Long Poiing](#/post/1c3eda9b-0fe1-811e-bc6d-f0d440af36d8)

[MessageMapping Annotation](#/post/1c3eda9b-0fe1-81bd-bc5e-ed5b06b64edc)

[JPA 네이밍을 통한 쿼리 처리, @Query](#/post/1c3eda9b-0fe1-81b4-ba76-c0eae02c213b)

[Transaction Manager를 활용한 WebSocket 경계 설정](#/post/1c3eda9b-0fe1-818d-8a43-c6b917e3ee6d)

[JDBC, JPA](#/post/1c3eda9b-0fe1-81b2-ba0f-de5bf6e513ca)

[기능을 위한 부수적인 API 작성 ( Entity → DTO )](#/post/1c3eda9b-0fe1-81c2-b366-ed6457263452)

[Request Header 정보 추출, MySQL - Like Search](#/post/1c3eda9b-0fe1-8136-893c-c0d42424263d)

[서비스 구동하여 테스트, 디버깅 하기](#/post/1c3eda9b-0fe1-8138-8491-fbee866f8ddd)

[StreamOffset](#/post/1c3eda9b-0fe1-81f5-9c76-c406241c89e1)

<a id="1c3eda9b0fe181ff945fc5de8abdf5fe"></a>

## 추가 정리

<details>
<summary>build gradle</summary>

<a id="1c3eda9b0fe18180b423fe66c8b50c6a"></a>

```bash
./gradlew clean build
```

<a id="1c3eda9b0fe181a58da4c2f758ad63ff"></a>

위 cmd를 통해 libs 등 자동으로 build 된다&#46;

<a id="1c3eda9b0fe1812fb077cd68182a8485"></a>

Spring Boot 실행 시, libs 내부에 있는 jar 파일을 싱핼한다&#46; 

</details>

<details>
<summary>명령어 custom</summary>

1. <code>&#46;sh</code> 파일 생성
    - ex) start&#46;sh

1. <code>&#46;sh</code> 파일 정의
    <a id="1c3eda9b0fe181d6b5eaee190fe03efc"></a>

    ```bash
    echo "Build Project"

    ./gradlew clean build

    echo "Start Server"

    cd ./build/libs
    java -jar demo-0.0.1-SNAPSHOT.jar
    ```

- 실행 &#45; 만든 파일 명 입력
    <a id="1c3eda9b0fe18149a03bfc4605de4573"></a>

    ```bash
    ./start.sh
    ```

</details>

[WebSocket, WebSocketSession](#/post/1c3eda9b-0fe1-8157-88f0-ee558cf21df6)

[WebSocketHandler](#/post/1c3eda9b-0fe1-8162-a64a-d7f8c3a0f783)

[WebSocketMessageBrokerConfigurer](#/post/1c3eda9b-0fe1-8164-b8cc-c9c380f6530f)

[SessionConnectEvent, SessionConnectedEvent, SessionDisconnectEvent](#/post/1c3eda9b-0fe1-81b2-aa86-dc264da09a14)

[RedisTemplate](#/post/1c3eda9b-0fe1-81fd-885c-f7b3a1038403)

[RedisConnectionFactory](#/post/1c3eda9b-0fe1-8122-bebb-c5ab7d56e20e)

[RedisMessageListenerContainer](#/post/1c3eda9b-0fe1-8187-b231-f35961e67e1f)

[MessageListenerAdapter](#/post/1c3eda9b-0fe1-8143-b70b-e4efb0a74220)

[ChannelTopic](#/post/1c3eda9b-0fe1-8188-9fbe-ec67044699cd)

[SimpMessagingTemplate](#/post/1c3eda9b-0fe1-81b7-9bd1-d343e1fc49ea)

[Redis Streams](#/post/1c3eda9b-0fe1-814e-991e-d931522d3f79)

[Redis Cache](#/post/1c3eda9b-0fe1-812a-a764-e38ac0c593db)

[스프링 스케줄링](#/post/1c3eda9b-0fe1-8150-a98e-f17c19b8f65f)

[AtomicInteger](#/post/1c3eda9b-0fe1-81ad-92c8-f9f6bfe07cae)

[WebSocket, 메세지브로커(STOMP)  실습](#/post/1c3eda9b-0fe1-8138-8d24-fa5be66ba1d2)

[Redis를 사용한 메세징 서비스  실습](#/post/1c3eda9b-0fe1-81aa-a0a9-f1fc85fcfd5a)
