---
order: 5
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 231eda9b-0fe1-804e-ad05-ff5449463e91
title: WebSocket with NestJS
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 226eda9b-0fe1-802b-a035-c3a886768c4d
    title: Nest.js
  - id: 227eda9b-0fe1-80e1-8036-d4fc3e106054
    title: 탄탄한 백엔드 NestJS, 기초부터 심화까지 ( 중지 )
  - id: 231eda9b-0fe1-804e-ad05-ff5449463e91
    title: WebSocket with NestJS
excerpt: "목차 - 데코레이터 - 1. 기본 프로젝트 세팅 - 로컬 개발 환경 구성 - 기본 의존성 설치 - 코드 - 2. 유니캐스팅 ( Unicasing ) : emit & on - 메세지 수신 - 메세지 발행 - 3. 네임스페이스 이해, Gateway 생명주기 - 의문 - 답변 - 4. 브로드캐스팅 ( Broadcasting )"
cover: fb3b1ee7da4a15e0.webp
icon: 9bed2eae1e079b4b.avif
notionProperties: {}
schema_version: 1
parent_id: 227eda9b-0fe1-80e1-8036-d4fc3e106054
created: 2025-07-15T11:18:35.531Z
updated: 2025-08-17T06:30:01.533Z
legacy_path: Main/Nest.js-c3a886768c4d/탄탄한 백엔드 NestJS, 기초부터 심화까지 ( 중지 )-d4fc3e106054/WebSocket with NestJS-ff5449463e91/index.md
legacy_category: Nest.js
source_url: https://beautiful-college-c84.notion.site/231eda9b0fe1804ead05ff5449463e91
---
> 
> 
> <a id="231eda9b0fe180b6a028cf930ec3cc1f"></a>
> 
> <strong>목차</strong>
> 
> - [데코레이터](#250eda9b0fe180428ae4f0cd0afcfd56)
> - [1.  기본 프로젝트 세팅](#250eda9b0fe180a99972dee233e9d349)
> - [로컬  개발 환경 구성](#250eda9b0fe18066a5e7f1be046ac097)
> - [기본 의존성 설치](#250eda9b0fe18081ba2ecefee5232579)
> - [코드](#250eda9b0fe180a097c7d286643fe754)
> - [2. 유니캐스팅  ( Unicasing ) : emit & on](#231eda9b0fe1801fb129cd095ab16d1f)
> - [메세지 수신](#250eda9b0fe180a5a885cda24a149e5c)
> - [메세지 발행](#250eda9b0fe1807c857af0274e82d07a)
> - [3. 네임스페이스 이해, Gateway 생명주기](#250eda9b0fe180c0acf7ed94d80c3be1)
> - [의문](#252eda9b0fe180ad97e5e063036752d8)
> - [답변](#252eda9b0fe18012a11be613b2c8f938)
> - [4. 브로드캐스팅 ( Broadcasting )](#250eda9b0fe180dd9102d9f0d339ba5f)
> - [5. 이벤트 설계, 기본 서비스 로직 완성](#250eda9b0fe1807399d8daa782f48b5c)

[Documentation &#124; NestJS &#45; A progressive Node&#46;js framework]()

<a id="250eda9b0fe180428ae4f0cd0afcfd56"></a>

### 데코레이터

- <code>&#64;WebSocketGateway()</code>

- <code>&#64;SubscribeMessage()</code>

- <code>&#64;MessageBody()</code>

<details>
<summary><strong><code>&#64;ConnectedSocket()</code></strong><strong> vs </strong><strong><code>&#64;WebSocketServer()</code></strong></summary>

| <strong>데코레이터</strong> | <strong>주입 대상</strong> | <strong>주로 쓰이는 상황</strong> | <strong>범위</strong> |
| --- | --- | --- | --- |
| <strong><code>&#64;ConnectedSocket()</code></strong> | 이벤트를 발생시킨 <strong>특정 클라이언트 소켓(Socket)</strong> | 어떤 메시지를 보낸 클라이언트에게만 응답 / 특정 클라이언트에 개별 동작 실행 | 단일 소켓(1&#58;1) |
| <strong><code>&#64;WebSocketServer()</code></strong> | Gateway가 사용하는 <strong>서버 전체 인스턴스(Server)</strong> | 모든 연결된 클라이언트에게 브로드캐스트 / 방(room) 관리 | 전체 서버(1&#58;N)<br> |

<details>
<summary>ex)</summary>

<a id="250eda9b0fe1805ab4e4e129c2616df0"></a>

```typescript
import {
  WebSocketGateway,
  SubscribeMessage,
  MessageBody,
  ConnectedSocket,
  WebSocketServer,
} from '@nestjs/websockets';
import { Server, Socket } from 'socket.io';

@WebSocketGateway()
export class ChatGateway {
  // 서버 전체 인스턴스 (모든 연결 클라이언트 제어 가능)
  @WebSocketServer()
  server: Server;

  @SubscribeMessage('sendMessage')
  handleMessage(
    @MessageBody() message: string,
    @ConnectedSocket() client: Socket, // 메시지를 보낸 '그' 클라이언트
  ) {
    // 1) 보낸 클라이언트에게만 응답
    client.emit('message', `You said: ${message}`);

    // 2) 모든 클라이언트에게 브로드캐스트
    this.server.emit('message', `Broadcast: ${message}`);
  }
}
```

</details>

</details>

<a id="250eda9b0fe180a99972dee233e9d349"></a>

## 1&#46;  기본 프로젝트 세팅

---

![](41d7c355c3e0a2f9.webp)

<a id="250eda9b0fe18066a5e7f1be046ac097"></a>

### 로컬  <strong>개발 환경 구성</strong>

<details>
<summary>NestJS  프로젝트 생성</summary>

<a id="250eda9b0fe180b8b146e8c60b97e781"></a>

```bash
nest new lecture
```

</details>

<details>
<summary>compose 파일 ( mongoDB 세팅 )</summary>

<a id="250eda9b0fe18068bbc9c416f072ff7d"></a>

```yaml
services:
  db:
    container_name: mongo
    image: mongo:7.0
    ports:
      - '27017:27017'
    environment:
      MONGO_INITDB_ROOT_USERNAME: ${MONGODB_USERNAME}
      MONGO_INITDB_ROOT_PASSWORD: ${MONGODB_PASSWORD}
    volumes:
      - db_data:/data/db

volumes:
  db_data:
```

</details>

<details>
<summary><code>&#46;env</code> 파일</summary>

<a id="250eda9b0fe180ae969ee0424e0c643b"></a>

```bash
MODE=dev
MONGODB_URL="mongodb://admin:admin123@localhost:27017/nest?authSource=admin"
MONGODB_USERNAME=admin
MONGODB_PASSWORD=admin123
```

</details>

<a id="250eda9b0fe18081ba2ecefee5232579"></a>

### <strong>기본 의존성 설치</strong>

> ✏️ 
> 
> <a id="250eda9b0fe1807ab697e4a66e7d4d11"></a>
> 
> <strong>WebSocket 패키지</strong>
> 
> > <strong>NestJS WebSockets 패키지</strong>
> 
> <details>
> <summary><strong><code>&#64;nestjs/websockets</code></strong></summary>
> 
> - NestJS에서 WebSocket Gateway, 데코레이터(<code>&#64;WebSocketGateway</code>, <code>&#64;ConnectedSocket</code>, <code>&#64;MessageBody</code>) 등을 제공하는 핵심 모듈
> 
> - 내부적으로 다양한 어댑터(Socket&#46;IO, ws 등)를 지원
> 
> </details>
> 
> <details>
> <summary><strong><code>&#64;nestjs/platform&#45;socket&#46;io</code></strong></summary>
> 
> - 기본 어댑터로 <code>Socket&#46;IO</code>를 사용하는 경우 필요한 패키지
> 
> - <code>&#64;WebSocketServer()</code>가 주입하는 Server 인스턴스가 여기서 제공됨
> 
> </details>
> 
> > <strong>Socket&#46;IO 패키지</strong>
> 
> <details>
> <summary><code>socket&#46;io</code></summary>
> 
> - Socket&#46;IO의 서버 엔진
> 
> - NestJS의 <code>&#64;WebSocketServer()</code>나 <code>&#64;ConnectedSocket()</code>이 주입하는 타입(Server, Sokcet)은 <strong><code>&#64;nestjs/platform&#45;socket&#46;io</code></strong><strong>를 통해 </strong>해당 패키지에서 제공됨
> 
> - Room 관리, broadcast, namespace 등 기능을 제공
> 
> </details>

<a id="250eda9b0fe1804d9f03e7bfe11c9fee"></a>

```bash
# hbs - html 렌더링 엔진
pnpm add hbs

# config
pnpm add --save @nestjs/config

# mongoDB
pnpm add --save @nestjs/mongoose mongoose

# WebSocket
pnpm add --save @nestjs/websockets @nestjs/platform-socket.io socket.io
	
```

<a id="250eda9b0fe180a097c7d286643fe754"></a>

### 코드

[feat: project basic settings](https://github.com/gyungsubLee/lecture_nestJS_websocket/commit/793c9676c6bf44b77154db66ecd4e9eb646555c3)

<a id="231eda9b0fe1801fb129cd095ab16d1f"></a>

## 2&#46; 유니캐스팅  ( Unicasing ) &#58; <code>emit</code> &#38; <code>on</code>

---

> 📖 
> 
> <a id="231eda9b0fe180e09949e30e9f72dbd4"></a>
> 
> NestJS에서는 WebSocket 메세지를 <strong><u>이벤트</u></strong><strong> 기반으로 식별한다&#46; </strong>
> 
> - <code>첫번째 인자</code>로 <strong><u>식별하는 이벤트(Topic)를 가르키는 </u></strong><strong><u>문자열</u></strong><strong><u>을 넘</u></strong>긴다&#46; 
> 
> - <code>두번째 인자</code>로 <strong><u>전달하려는 데이터</u></strong>를 넘긴다&#46; 
> 
> - <code>세번째 인자</code>는 <strong><u>반환되는 데이터를 받는 콜백 함수</u></strong>를 넘긴다&#46;

<a id="250eda9b0fe180a5a885cda24a149e5c"></a>

### 메세지 수신

> ✏️ 
> 
> <a id="250eda9b0fe18034a09ff490a863d4eb"></a>
> 
> 클라이언트에서 설정한 <strong><u>topic</u></strong>로 식별하여 메세지를 받아온다 &#46;
> 
> - 프론트&#58; <strong><code>socket&#46;</code></strong><strong><code>emit</code></strong><code>(topic, data);</code>
> 
> - 서버&#58; 
>     - <strong><code>&#64;SubscribeMessage</code></strong><code>(topic)</code>
> 
>     - <strong><code>&#64;MessageBody()</code></strong><code> data&#58; type</code>

<details>
<summary>프론트</summary>

<a id="250eda9b0fe180d78ea5f03be614b6d9"></a>

```javascript
const socket = io('/');

const getElementById = (id) => document.getElementById(id) || null;

//* get DOM element
const helloStrangerElement = getElementById('hello_stranger');
const chattingBoxElement = getElementById('chatting_box');
const formElement = getElementById('chat_form');

function helloUser() {
  const username = prompt('What is your name?');
  // 'new_username' 이라는 문자열로 이벤트를 식별한다.  ( 쉽게 말해, topic이라 생각하면 된다. )
  socket.emit('new_username', username);
}

function init() {
  helloUser();
}

init();
```

</details>

<details>
<summary>서버</summary>

<a id="250eda9b0fe180b1be59fd976202557a"></a>

```typescript
import { Logger } from '@nestjs/common';
import {
  MessageBody,
  SubscribeMessage,
  WebSocketGateway,
} from '@nestjs/websockets';

@WebSocketGateway()
export class ChatGateWay {
  private readonly logger = new Logger(ChatGateWay.name);

  @SubscribeMessage('new_username')
  handleMessage(@MessageBody() username: string): string {
    this.logger.log(`Receive message: ${username}`);
    return 'hello ' + username;
  }
}
```

- 클라이언트에서 설정한 이벤트 식별자를 <code>&#64;SubscibeMessage</code>로 구독하여 메세지를 수신한다&#46;

</details>

> 🗣 
> 
> <a id="250eda9b0fe1809fae82d4fa25e3d414"></a>
> 
> 새로고침 이후, 기존 socket 연결은 끊기고 새로운 socket 연결이 시작된다&#46; 
> 
> <details>
> <summary>새로고침 이후 <code>socket&#46;id</code> 값이 변함</summary>
> 
> > 새로고침 이후, 출력되는 <code>socket&#46;id</code> 값이 변하는 것을 확인할 수있다&#46; 이로인해 매번 소캣이 재연결 되는 것을 알 수 있다&#46;
> 
> ![](4f9667fe2dfa2e5c.webp)
> 
> <a id="250eda9b0fe1807db91fe357fc6c7984"></a>
> 
> ```typescript
> import { Logger } from '@nestjs/common';
> import {
>   ConnectedSocket,
>   MessageBody,
>   SubscribeMessage,
>   WebSocketGateway,
> } from '@nestjs/websockets';
> import { Socket } from 'socket.io';
> 
> @WebSocketGateway()
> export class ChatGateWay {
>   private readonly logger = new Logger(ChatGateWay.name);
> 
>   @SubscribeMessage('new_username')
>   receiveMessage(
>     @MessageBody() username: string,
>     @ConnectedSocket() socket: Socket,
>   ) {
>     console.log(socket.id);
>     this.logger.log(`Receive message: ${username}`);
>   }
> }
> ```
> 
> </details>

<a id="250eda9b0fe1807c857af0274e82d07a"></a>

### 메세지 발행

> ✏️ 
> 
> <a id="250eda9b0fe180bcbeb7f8e0769f6b85"></a>
> 
> 클라이언트에서 설정한 <strong><u>이벤트(topic)</u></strong>로 식별하여 메세지를 받아온다 &#46;
> 
> <details>
> <summary><strong>Case 1)</strong> 수신 받은 topic을 통해 서버에 return 값으로 다시 데이터를 보낼 수 있다&#46; </summary>
> 
> - 프론트&#58; <strong><code>socket&#46;</code></strong><strong><code>emit</code></strong><strong><code>(topic, data, callback(data));</code></strong>
> 
> - 서버&#58; 해당 topic 으로 메세지 수신 후 <code>return</code> 
> 
> </details>
> 
> <details>
> <summary><strong>Case 2)</strong> <code>&#64;ConnectedSocket()</code>으로 받아온 인스턴스의 <code>&#46;emit()</code> 메서드를 통해 서버에서 메세지를 발행할 수 있다&#46; </summary>
> 
> - 프론트&#58; <strong><code>socket&#46;</code></strong><strong><code>on</code></strong><code>(topic, data);</code>
> 
> - 서버&#58; <strong><code>socket&#46;</code></strong><strong><code>emit</code></strong><strong><code>(topic, data);</code></strong>
> 
> </details>

<details>
<summary>프론트</summary>

<a id="250eda9b0fe180e5beede7035be6ac1e"></a>

```javascript
const socket = io('/');

const getElementById = (id) => document.getElementById(id) || null;

const helloStrangerElement = getElementById('hello_stranger');
const chattingBoxElement = getElementById('chatting_box');
const formElement = getElementById('chat_form');

function helloUser() {
  const username = prompt('What is your name?');
  console.log(username);
  
  // 메세지 발행 후 서버에서 return 값이 있을 시, callback으로 받아올 수 있다. 
  socket.emit('topic1', username, (data) => {
    console.log(data);
  });
	
		// 메세지 수신: on(이벤트, callback(데이터))
  socket.on('topic2', (data) => {
    console.log(data);
  });
}

function init() {
  helloUser();
}

init();
```

</details>

<details>
<summary>서버</summary>

<a id="250eda9b0fe180e1b2e2e0a2ad9106ab"></a>

```typescript
import { Logger } from '@nestjs/common';
import {
  ConnectedSocket,
  MessageBody,
  SubscribeMessage,
  WebSocketGateway,
} from '@nestjs/websockets';
import { Socket } from 'socket.io';

@WebSocketGateway()
export class ChatGateWay {

  @SubscribeMessage('topic1')
  receiveMessage(
    @MessageBody() username: string,
    @ConnectedSocket() socket: Socket,
  ) {
    console.log(socket.id);
    console.log(`topic1 테스트: ${username}`);
    
    // 설정한 topic 으로 메세지 발행
    socket.emit('topic2', 'topic2 테스트');
		
		// 수신 받은 topic 으로 return 데이터 발행
    return 'topic1 return 테스트';
  }
}
```

- 클라이언트에서 설정한 이벤트 식별자를 <code>&#64;SubscibeMessage</code>로 구독하여 메세지를 수신한다&#46;

</details>

> ⚠️ 
> 
> <a id="250eda9b0fe1804095d3dcbb5223f376"></a>
> 
> <code>&#64;ConnectedSocket()</code>을 통해 가져오는  socket 인스턴스는 클라이언트에서 받아오는 socket 수신 정보를 통해 connection이 이뤄진다&#46; 
> 
> - 클라이언트에서 <code>socekt&#46;emit(topic, 메세지)</code>으로 메세지가 발행되고 서버에서 <code>&#64;SubscribeMessage(topic)</code> 으로 메세지가 수신되는 과정이 한번 이뤄져야 connection이 이뤄진다&#46; 
> 
> <a id="250eda9b0fe18091b11ede51cbe8787f"></a>
> 
> 따라서 <strong>수신 없이 서버에서만 인스턴스를 생성하여 메세지 발행</strong> 시 <strong><u>오류가 발생</u></strong>된다&#46; 
> 
> <details>
> <summary>ex)</summary>
> 
> <details>
> <summary>클라이언트</summary>
> 
> <a id="250eda9b0fe18038bad2ebc82a340b89"></a>
> 
> ```typescript
> const socket = io('/');
> 
> const getElementById = (id) => document.getElementById(id) || null;
> 
> //* get DOM element
> const helloStrangerElement = getElementById('hello_stranger');
> const chattingBoxElement = getElementById('chatting_box');
> const formElement = getElementById('chat_form');
> 
> function helloUser() {
>   const username = prompt('What is your name?');
>   console.log(username);
>   socket.emit('topic1', username, (data) => {
>     console.log(data);
>   });
> 
>   socket.on('topic2', (data) => {
>     console.log(data);
>   });
> 	
> 	// 
>   socket.on('topic3', (data) => {
>     console.log(data);
>   });
> }
> 
> function init() {
>   helloUser();
> }
> 
> init();
> ```
> 
> </details>
> 
> <details>
> <summary>서버</summary>
> 
> <a id="250eda9b0fe1803a97dbe5bcc8f04247"></a>
> 
> ```typescript
> import { Logger } from '@nestjs/common';
> import {
>   ConnectedSocket,
>   MessageBody,
>   SubscribeMessage,
>   WebSocketGateway,
> } from '@nestjs/websockets';
> import { Socket } from 'socket.io';
> 
> @WebSocketGateway()
> export class ChatGateWay {
>   @SubscribeMessage('topic1')
>   receiveMessage(
>     @MessageBody() username: string,
>     @ConnectedSocket() socket: Socket,
>   ) {
>     console.log(socket.id);
>     console.log(`topic1 테스트: ${username}`);
>     socket.emit('topic2', 'topic2 테스트');
> 
>     return 'topic1 return 테스트';
>   }
> 	
> 	// 클라이언트 발행을 통해 connection이 식별된다. 
> 	// 따라서 위와 같이 클라이언트에서 구독만하는 경우, 
> 	// 메세지 발행이 정상적으로 이뤄지지 않는다. 
>   @SubscribeMessage('topic3')
>   publishMessgae(@ConnectedSocket() socket: Socket) {
>     socket.emit('topic3', '테스트용 메세지 발행');
>   }
> }
> 
> ```
> 
> </details>
> 
> </details>

<a id="250eda9b0fe180c0acf7ed94d80c3be1"></a>

## 3&#46; 네임스페이스 이해, Gateway 생명주기

---

[Documentation &#124; NestJS &#45; A progressive Node&#46;js framework]()

> 📖 
> 
> <a id="252eda9b0fe1806f8d01d1df6df4b0e1"></a>
> 
> HTTP에서 사용되는 Controller와 같다고 생각하면된다&#46; 
> 
> <a id="252eda9b0fe1808abf65c07669b30654"></a>
> 
> Controller에서 엔드포인트로 각 도메인을 구분해서 설계 하듯이 
> 
> <a id="252eda9b0fe180b49e81ece958d9dea8"></a>
> 
> <code>Websocket</code>에서는 <strong><u>Gateway를 </u></strong><strong><u>‘네임스페이스’</u></strong><strong><u>로 구분</u></strong>해 설계할 수 있다&#46;

<details>
<summary>Protocol Switching &#91; <code>HTTP</code> → <code>WebSocket</code> &#93;</summary>

![](ce2edfd8c0db4cbb.webp)

- 위와 같이 최초 WebSocket 연결이 이뤄질 때, HTTP로 Protocol Switching 요청이 이뤄지는 것을 확인할 수 있다&#46;  

</details>

<details>
<summary><code>Socket&#46;io</code> 라이브러리</summary>

> ✏️ 
> 
> <a id="252eda9b0fe180879909e409f9a46df9"></a>
> 
> WebSocket의 경우, Explorer 같은 옛날 브라우저의 경우 지원되지 않을 수 있다&#46;<br> 이렇게 WebSocket이 지원되지 않는 경우, <code>Socket&#46;io</code> 라이브러리 사용 시 자동으로 폴링 방식을 지원하여 거의 모든 브라우저에서 소켓 프로그래밍이 가능토록 해준다&#46; 

![](686b65e5682e6257.webp)

- 위와 같이 WebSocket 연결 시, websocket 통신 외 <strong><u>polling 방식으로도 통신</u></strong>이 되는 것을 확인할 수 있다&#46;

</details>

<details>
<summary>🧐 네임스페이스로 구분하여 socket을 통신 시, socket 연결이 중복으로 생성되어 병목이 발생되지 않는가?</summary>

[Namespaces &#124; Socket&#46;IO]()

<a id="252eda9b0fe180ad97e5e063036752d8"></a>

### 의문

> ❔ 
> 
> <a id="252eda9b0fe18072af0fc564212e66ad"></a>
> 
> 각 namespace마다 io 인스턴스를 생성하여 socket 연결 시 메모리에서 socket 연결 정보가 중첩으로 생성되어 병목이 발생되지 않는가?

<details>
<summary><strong>Server</strong></summary>

<a id="252eda9b0fe180479a0fc26089bb39e3"></a>

```typescript
@WebSocketGateway({ namespace: '/devices' })
...

@WebSocketGateway({ namespace: '/games' })
...
```

</details>

<details>
<summary><strong>Client</strong></summary>

<a id="252eda9b0fe1807a805bf26d481344a9"></a>

```typescript

import { io, Socket } from "socket.io-client";

const devices = io("/devices"); // namespace: '/devices'
const games   = io("/games");   // namespace: '/games'

devices.on("device:update", console.log);
games.emit("game:join", { gameId: "g1" });
```

</details>

<a id="252eda9b0fe18012a11be613b2c8f938"></a>

### 답변

> 🗣 
> 
> <a id="252eda9b0fe1808c97dbf4486a54728f"></a>
> 
> <strong><u>같은 ‘호스트/경로’, ‘path’(socket&#46;io …)</u></strong><strong><u>로 연결</u></strong>시 Socket&#46;IO는  한 개의 WebSocket(Engine&#46;io) 연결을 <code>멀티플렉싱</code>해서 쓴다&#46;
> 
> <a id="252eda9b0fe180a5a319f930e460c3a0"></a>
> 
> 즉, <strong><u>namespace를 여러 개 설정</u></strong>해도 <strong><u>TCP/WebSocket 커넥션이 중복으로 생겨 병목이 발생되지 </u></strong><strong><u>않</u></strong>는다&#46; 
> 
> - 각 네임스페이스마다 <strong><u>논리적 Socket 객체만 추</u></strong>가한다&#46;

<details>
<summary> ⚠️ <strong>WebSocket 연결이 새로 생성되는 경우 </strong></summary>

- 다른 호스트/포트/프로토콜(https ↔ http) 로 접속 시

- 다른 path 옵션 사용 시 ( default&#58; <code>/socket&#46;io</code> )

- 클라이언트 옵션이 달라 서로 다른 Manager가 생성되는 경우 <br>( forceNew&#58; true 등 )

</details>

</details>

<a id="250eda9b0fe180dd9102d9f0d339ba5f"></a>

## 4&#46; 브로드캐스팅 ( Broadcasting )

---

> 📖 

<a id="250eda9b0fe1807399d8daa782f48b5c"></a>

## 5&#46; 이벤트 설계, 기본 서비스 로직 완성

---

> 📖
