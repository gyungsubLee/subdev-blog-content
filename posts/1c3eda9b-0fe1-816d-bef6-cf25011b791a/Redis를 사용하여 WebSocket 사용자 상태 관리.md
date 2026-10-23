---
order: 5
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1c3eda9b-0fe1-816d-bef6-cf25011b791a
title: Redis를 사용하여 WebSocket 사용자 상태 관리
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-81ae-909e-cd1f71740107
    title: Spring ( Java )
  - id: 1c3eda9b-0fe1-812e-b8ac-c13c536efd00
    title: Spring Boot를 활용한 채팅 서비스 만들어보기
  - id: 1c3eda9b-0fe1-816d-bef6-cf25011b791a
    title: Redis를 사용하여 WebSocket 사용자 상태 관리
excerpt: Redis를 사용하여 WebSocket 사용자 상태 관리 --- 📖 Redis를 사용하면 WebSocket 사용자 상태를 효율적으로 관리할 수 있다. 서버가 여러 대로 구성된 다중 서버 환경에서 Redis는 상태 동기화 문제를 해결하는 데 유용하다. 유저 상태 관리 방식 - 서버에서 유저의 상태를 관리하기 위해 주로 사
cover: null
icon: null
notionProperties:
  Tags: 추가 정리
schema_version: 1
parent_id: 1c3eda9b-0fe1-812e-b8ac-c13c536efd00
created: 2025-03-27T07:53:11.125Z
updated: 2025-03-27T07:53:11.125Z
legacy_path: Main/Spring ( Java )-cd1f71740107/Spring Boot를 활용한 채팅 서비스 만들어보기-c13c536efd00/Redis를 사용하여 WebSocket 사용자 상태 관리-cf25011b791a/index.md
legacy_category: Spring ( Java )
source_url: https://beautiful-college-c84.notion.site/1c3eda9b0fe1816dbef6cf25011b791a
---
<a id="1c3eda9b0fe181faa685dbd2d5269b84"></a>

## Redis를 사용하여 <strong>WebSocket 사용자 상태 관리</strong> 

---

> 📖 
> 
> <a id="1c3eda9b0fe1813e984af04d1ae32632"></a>
> 
> Redis를 사용하면 WebSocket 사용자 상태를 효율적으로 관리할 수 있다&#46; <br>서버가 여러 대로 구성된 <strong><u>다중 서버 환경</u></strong>에서 Redis는 <u>상태 동기화 문제를 해결하는 데 유용하</u>다&#46;

<details>
<summary>유저 상태 관리 방식</summary>

- 서버에서 유저의 상태를 관리하기 위해 주로 사용되는 방법
    - <strong>웹소켓 세션 관리</strong>&#58; 연결된 사용자와 세션 ID를 매핑&#46;

    - <strong>Redis와 같은 외부 저장소 사용</strong>&#58; 다중 서버 환경에서 유저 상태를 관리하려면 Redis를 사용해 유저와 세션 정보를 중앙화&#46;

    - <strong>JWT 기반 인증</strong>&#58; 클라이언트가 연결 시 JWT 토큰을 보내 유저를 인증하고 상태 정보를 확인&#46;

- <strong>중요한 포인트</strong>
    - <strong>클라이언트</strong>는 from과 to 정보를 메시지에 포함하여 전송&#46;

    - <strong>서버</strong>는 from 정보를 세션과 매핑하여 상태를 관리하고, to 정보를 이용해 적절한 대상에게 메시지를 라우팅&#46;

</details>

<details>
<summary>웹소켓(WebSocket)을 사용한 실시간 채팅 기능 구현</summary>

<details>
<summary>클라이언트 </summary>

<a id="1c3eda9b0fe181389b48f7b8b3b17a34"></a>

```javascript
const socket = new WebSocket('ws://localhost:8080/chat');

socket.onopen = function () {
    console.log('Connected to server');
    // 초기 연결 시 from 정보를 서버로 보냄
    socket.send(JSON.stringify({ type: 'INIT', from: 'user123' }));
};

socket.onmessage = function (event) {
    const message = JSON.parse(event.data);
    console.log('Received message:', message);
};

function sendMessage(to, content) {
    // 서버로 메시지 전송
    const message = {
        type: 'MESSAGE',
        from: 'user123', // 송신자 정보
        to: to,         // 수신자 정보
        content: content,
    };
    socket.send(JSON.stringify(message));
}
```

</details>

<details>
<summary>WebSocket Config 설정 &#45; STOMP 서브 프로토콜 사용</summary>

<a id="1c3eda9b0fe18121841fded2874d8655"></a>

```java
@Configuration
@EnableWebSocketMessageBroker
public class WebSocketConfig implements WebSocketMessageBrokerConfigurer {

    @Override
    public void configureMessageBroker(MessageBrokerRegistry registry) {
        registry.enableSimpleBroker("/topic"); // 메시지 브로커
        registry.setApplicationDestinationPrefixes("/app"); // 클라이언트에서 서버로 보내는 prefix
    }

    @Override
    public void registerStompEndpoints(StompEndpointRegistry registry) {
        registry.addEndpoint("/chat").setAllowedOriginPatterns("*").withSockJS(); // 연결 엔드포인트
    }
}
```

</details>

<details>
<summary><strong>WebSocket 핸들러 (유저 세션 관리)</strong></summary>

<a id="1c3eda9b0fe18165b170c6d0c8848a6a"></a>

```java
@Component
public class WebSocketEventListener {

    private final Map<String, WebSocketSession> userSessions = new ConcurrentHashMap<>();

    @EventListener
    public void handleWebSocketConnectListener(SessionConnectEvent event) {
        StompHeaderAccessor accessor = StompHeaderAccessor.wrap(event.getMessage());
        String username = accessor.getFirstNativeHeader("username"); // 클라이언트가 보낸 유저 정보
        WebSocketSession session = accessor.getSessionAttributes();

        if (username != null) {
            userSessions.put(username, session);
        }
    }

    @EventListener
    public void handleWebSocketDisconnectListener(SessionDisconnectEvent event) {
        WebSocketSession session = event.getWebSocketSession();
        userSessions.values().remove(session);
    }

    public void sendMessageToUser(String to, String message) throws IOException {
        WebSocketSession session = userSessions.get(to);
        if (session != null && session.isOpen()) {
            session.sendMessage(new TextMessage(message));
        }
    }
}
```

</details>

<details>
<summary>컨트롤러 ( 메시지 처리 )</summary>

<a id="1c3eda9b0fe181da849eef437e6f67dd"></a>

```java
@Controller
public class ChatController {

    @MessageMapping("/sendMessage") // 클라이언트가 보낸 메시지 처리
    @SendTo("/topic/messages")
    public ChatMessage sendMessage(ChatMessage message) {
        return message; // 받은 메시지를 그대로 브로드캐스트
    }

    @MessageMapping("/privateMessage")
    public void sendPrivateMessage(ChatMessage message) {
        String toUser = message.getTo();
        // 특정 사용자에게 메시지 보내기
        webSocketEventListener.sendMessageToUser(toUser, message.getContent());
    }
}
```

</details>

</details>

<details>
<summary>Redis를 사용하는 이유</summary>

-  <strong>세션 상태의 중앙 집중화</strong>
    - Redis에 유저와 세션 정보를 저장하여 모든 서버에서 접근 가능

- <strong>성능 최적화</strong>
    - Redis는 인메모리 데이터 저장소로 읽기/쓰기 속도가 매우 빠름

- <strong>확장성</strong>
    - 서버가 추가되어도 상태 동기화를 손쉽게 처리&#46;

</details>

<details>
<summary>redis를 사용한 실시간 채팅 기능 구현</summary>

<details>
<summary><strong>1&#46; Redis 의존성 추가</strong></summary>

<a id="1c3eda9b0fe181a18b9dd3331a757079"></a>

```java
implementation 'org.springframework.boot:spring-boot-starter-data-redis'
```

</details>

<details>
<summary>2&#46; Redis config</summary>

<a id="1c3eda9b0fe181dfabc2e962e5f3f4cc"></a>

```java
@Configuration
public class RedisConfig {
	
		@Bean
		public RedisTemplate<String, Object> redisTemplate(RedisConnectionFactory connectionFactory) {
				RedisTemplate<String, Object> template = new RedisTemplate<>();
				template.setConnectionFactory(connectionFactory);
				template.setKeySerializer(new StringRedisSerializer());
				template.setValueSerializer(new GenericJackson2JsonRedisSerializer());
				return template;
		}		
}
```

- RedisTempalte
    - setConnectiomFactory

    - setKeySerializer

    - setValueSerializer

- RedisConnectionFactory

- StringRedisSerializer

- GenericJackson2JsonRedisSerializer

</details>

<details>
<summary>3&#46; WebSocket 상태 저장 로직</summary>

<a id="1c3eda9b0fe181e597a0eae48f0ffe3b"></a>

```java
@Component

```

</details>

</details>
