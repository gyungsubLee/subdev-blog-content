---
order: 0
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1c3eda9b-0fe1-8129-856c-d0370af4a055
title: RabbitMQ 개요, 비동기 아키텍처
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-817c-b119-d6a1706fbaf8
    title: 대규모 시스템 설계
  - id: 1c3eda9b-0fe1-8191-9188-e28e651123f1
    title: RabbitMQ를 이용한 비동기 아키텍처
  - id: 1c3eda9b-0fe1-8129-856c-d0370af4a055
    title: RabbitMQ 개요, 비동기 아키텍처
excerpt: "🗣 대용량 트래픽을 처리하기 위한 기본 아키텍처들이 몇가지 있다. 이런 아키텍처 중 가장 첫 번째로 꼽는 것이 비동기 아키텍처이다. - 그 다음에 Cache 시스템 등이 있다. RabbitMQ --- ✏️ 글로벌 환경이나, 대용량 데이터, 급성장하고 있는 시스템들에서는 MQ와 같은 미들웨어를 사용하여 데이터와 트래픽을 "
cover: null
icon: null
notionProperties:
  Tags: 개념
  Point: 비동기 아키텍처에 대해서 추가 정리 필요함
  중요도: No
  상태: 완료
  다중 선택: Chapter1
schema_version: 1
parent_id: 1c3eda9b-0fe1-8191-9188-e28e651123f1
created: 2025-03-27T07:47:43.049Z
updated: 2026-09-01T11:22:23.007Z
legacy_path: Main/대규모 시스템 설계-d6a1706fbaf8/RabbitMQ를 이용한 비동기 아키텍처-e28e651123f1/RabbitMQ 개요, 비동기 아키텍처-d0370af4a055/index.md
legacy_category: 대규모 시스템 설계
source_url: https://beautiful-college-c84.notion.site/1c3eda9b0fe18129856cd0370af4a055
---
> 🗣 
> 
> <a id="1c3eda9b0fe1810697abeebbb896c72f"></a>
> 
> 대용량 트래픽을 처리하기 위한 기본 아키텍처들이 몇가지 있다&#46;
> 
> <a id="1c3eda9b0fe181038e32f3b8b513a0b4"></a>
> 
> 이런 아키텍처 중 가장 첫 번째로 꼽는 것이 비동기 아키텍처이다&#46;
> 
> - 그 다음에 Cache 시스템 등이 있다&#46;

<a id="1c3eda9b0fe18140b50ad74c0cc9a258"></a>

## RabbitMQ

---

> ✏️ 
> 
> <a id="1c3eda9b0fe181a6b321f0e5f0aaa1bd"></a>
> 
> 글로벌 환경이나, 대용량 데이터, 급성장하고 있는 시스템들에서는<strong><u> MQ와 같은 미들웨어를</u></strong> 사용하여 데<strong><u>이터와 트래픽을 분산 처리</u></strong>하는 것은 필수적이며, 그 중 RadditMQ는 일반적으로 많이 사용되는 기술이다&#46; 
> 
> - Kafka  …

<a id="1c3eda9b0fe1819a8ef6c273196d0d1a"></a>

### 개요

---

<a id="1c3eda9b0fe18130b9d4c9df89b033ad"></a>

RabbitMQ는 <a href="https://namu.wiki/w/Erlang">Erlang</a>으로 만들어진 메세지 전송 브로커 오픈소스이다&#46; (미들웨어)

- 2007년에 처음 릴리즈 되었다&#46; 

<a id="1c3eda9b0fe1812bb60aff27c2a754fc"></a>

시스템 간 비동기 메세징을 가능하게 하여 서비스 간 통신을 안정적이고 효율적으로 처리할 수 있게 해준다&#46; <br>플랫폼 중립적이며, 가볍고 다양한 언어들의 클라이언트 라이브러리를 제공하고, 유연한 성능과 안정성을 제공한다&#46; 

- 과거 RabbitMQ가 나오기 전까지는 JMS(Java Message Service, 자바 전용 API)를 사용했다&#46; 
    - 벤더별로 특정 벤더에 디펜던시가 있는 구현체들이 제공되었다&#46; 
        - IBM, 마이크로소르프, 데이터 기반 큐잉, 플링 방식 …&#46;

- 그러나 rabbitMQ가 나오고 나서 <strong><u>플랫폼 중릭적</u></strong>이고, Python, go, javascript, java 등  다양한 클라이언트 라이브러리들을 지원할 수 있게 되었다&#46; 

<a id="1c3eda9b0fe181eebc36c05155756ac9"></a>

클러스터를 설정할 때 <strong><u>큐</u></strong>를 <code>HA(High Available)</code>로 설정하여 <strong><u>여러 노드에 저장</u></strong>하므로서,<strong><u> 메세지 손실을 방지</u></strong>한다&#46; 또한 쉽게 새로운 기능을 추가할 수 있고, <strong><u>Federation 플러그인을</u></strong> 통해 <strong><u>데이터 동기화</u></strong>와 <strong><u>다중 마스터 복제</u></strong>를 구성할 수 있다&#46; 

<a id="1c3eda9b0fe1817ebc35e202240cbc9f"></a>

<strong><u>최근 </u></strong><strong><u>MSA 환경</u></strong><strong><u>에서 가장 일반적으로 쓰이는 기술</u></strong> 중 하나이며, 대량의 데이터 전송 시 발생할 수 있는 과부하를 분산시키며, 비동기 처리와 지연이 필요한 작업을 효과적으로 관리 해줄 수 있다&#46;  ( 모니터링 가능 )

- 중간에 MQ 같은 미들웨어들을 활용하여 앱 간의 결합성을 낮추고, 비동기적으로 동작할 수 있도록 한다&#46; 

<a id="1c3eda9b0fe1813faf34cecf43464897"></a>

### 대표적인 도메인 활용 사례

- <code>EDA(Event&#45;Driven Architecture)</code>
    - 주문/결제/배송 등 비지니스 도메인을 이벤트 기반의 독립적인 도메인 모듈로 구성

- <code>로그 및 모니터링</code>
    - 로그 수집 및 준 실시간 처리 모니터링 시스템 구축

- <code>채팅 및 알람</code>
    - WebSocket, STOMP 연동 가능

- <code>비동기 데이터 처리</code>
    - <strong><u>대용량 이미지, 비디오</u></strong> 처리에 <strong><u>효율적인 분산 시스템 구축</u></strong> 가능

- <code>여러 디바이스의 요청 처리 </code>
    - IoT와 같은 멀티 디바이스 환경에서의 요청 처리 

<a id="1c3eda9b0fe1817d843fd3a9dae1e556"></a>

### 비동기 아키텍처

<details>
<summary>Reference</summary>

<a id="1c3eda9b0fe1811e8035e0a0944456a4"></a>

‣

-  ‘AWS 리인벤트 2022’ 기조연설 &#45; 버너 보겔스 &#91;아마존닷컴 최고기술책임자(CTO)&#93;

</details>

<a id="1c3eda9b0fe181f6917bff7a97c7362b"></a>

컴퓨터 운영체제의 원시 모델인 <strong><u>유닉스 OS</u></strong>는 비동기식으로 작동한다&#46;

<a id="1c3eda9b0fe1817c952cd9e668c661e5"></a>

<strong>이를 통해,  </strong><strong><u>이상적 컴퓨팅 아키텍처도 </u></strong><strong><u>비동기식</u></strong><strong><u>으로 이뤄져야 자연스러운 것</u></strong>이라 강조했다

<details>
<summary>ex) 겨울철 철새의 이동 → 비동기</summary>

- 한마리의 새가 주변을 관찰하는 상호 작용을 통해 다른 새와 거리, 방향을 유지해 날아간다&#46;

- 새들은 이렇게 피드백 루프를 통해 이동하면서 자율적으로 움직인다
    <a id="1c3eda9b0fe18142b4aceb1f40972cb8"></a>

    ⇒ 전반적인 시스템이 동기적으로 움직이는 듯 보이지만, <strong><u>순수한 비동기식으로 동작</u></strong>된다&#46;

</details>

<a id="1c3eda9b0fe181c89330d9be904150aa"></a>

<code>OS</code>는 디바이스 간 상호작용을 다루는 <strong><u>이벤트 기반의 비동기 시스템</u></strong>이다&#46;

> ☝🏻 
> 
> <a id="1c3eda9b0fe181c9be11d34f34140f54"></a>
> 
> <strong><u>시스템을</u></strong><strong><u> 동기식</u></strong><strong><u>으로 구축</u></strong>하면 <strong><u>단단하게 연결된 시스템을 만</u></strong>들어서 <strong><u>어떤 변화도 할 수 없</u></strong>게 된다
> 
> <a id="1c3eda9b0fe181e09bd3cc302d364f11"></a>
> 
> ⇒<strong><u> 동기식 시스템</u></strong>은 <strong><u>하나만 실패해도 모든 게 실패</u></strong>한다

<a id="1c3eda9b0fe181c79391d01f67539b66"></a>

<strong><code>비동기화된 시스템</code></strong>은 <strong><u>느슨하게 연결</u></strong>돼 <strong><u>단계적으로 진행</u></strong>된다&#46;

<a id="1c3eda9b0fe18131a631f5c0f8a7629b"></a>

다른 요소를 바꾸지 않고 <strong><u>일부만 바꾸거나 추가</u></strong>할 수 있어 <strong><u>진화형 아키텍처</u></strong>를 갖게 된다

<a id="1c3eda9b0fe18166aeefdbe91473c571"></a>

⇒ 시스템을 구축하는데 모든 시스템을 한번에 하지 말고, <strong><u>작게 시작</u></strong>해서 <strong><u>가동</u></strong>하고 그것을 <strong><u>진화</u></strong>시켜서 <strong><u>더 복잡한 전체 시스템으로 개발</u></strong>해야 한다

<a id="1c3eda9b0fe1814784d0e77928939c71"></a>

<br>

> ✏️ 
> 
> <a id="1c3eda9b0fe1816f97bfc93e1e830009"></a>
> 
> <strong>비동기 → 메세징 시스템 → MSA, EDA ⇒ 서버리스 &#91; AWS 람다, … &#93;</strong>

<a id="1c3eda9b0fe181aa8fd7fd4c1b1f6aae"></a>

### <strong>이벤트 드리븐 아키텍처 ( </strong>이벤트 드리븐 프로그래밍)

---

<a id="1c3eda9b0fe181ddaa30c140825bfce6"></a>

<strong><u>이벤트 드리븐 아키텍처</u></strong>는 MSA란 기본 조건 하에서 소프트웨어 기능을 <strong><u>특정 조건(이벤트) 충족 시 일련의 워크플로우를 따라 그 순간 작동</u></strong>시키는 것이다&#46;

- <strong><u>초기 컴퓨터 프로그래밍</u></strong>은 모노리스 아키텍처 형태로 진화했으며, 2010년대 들어서야 <strong><u>코드를 기능별로 쪼개</u></strong><strong> </strong><strong><u>독립적</u></strong>이면서 <strong><u>상호작용</u></strong>하며 작동하게 하는 <strong>마이크로서비스 아키텍처(MSA)</strong>가 주류로 떠올랐다

<a id="1c3eda9b0fe1813f8b73e38927d8d980"></a>

데이터가 끊임없이 흘러가는 가운데 이벤트를 포착하면, 그때 준비해둔 코드 및 마이크로서비스가 사전준비된 시나리오 순서대로 작동해 하나의 완결된 작업을 이뤄낸다&#46;

-  ‘프론트엔드&#45;백엔드&#45;데이터’란 3계층 아키텍처나 객체지향프로그래밍(OOP)과 다른 방식이다&#46;

- 다양한 측면의 고려를 해야 하기 때문에 개발 과정이 쉽지 않다&#46; 시나리오를 생각하고, 각 코드가 일련의 흐름을 따라 상호작용하며 의도한 결과를 내야 하므로 첫 구상단계부터 까다로운 사고가 필요하다&#46;

<a id="1c3eda9b0fe181ed8731dcd967ba56aa"></a>

<strong><u>느슨하게 연결된 시스템</u></strong>은 <strong><u>워크플로우 패턴</u></strong>, 즉 <strong><u>경로</u></strong>가 있어야 하고, <strong><u>순서대로 작업을 처리</u></strong>하고 <strong><u>실패하면 재시도</u></strong>하는 방식으로 만들어진다

<a id="1c3eda9b0fe181f2b1a7c23e34f11fc6"></a>

### AWS &#45; 이벤트 드리븐 아키텍처

---

<a id="1c3eda9b0fe18174be11df2facf39121"></a>

<code>AWS 람다</code>를 사용하여 <strong><u>서버 리스</u></strong><strong><u> 방식으로  코드만 작성</u></strong>해 올리면 <strong><u>실행 조건 상황 발생</u></strong>에 따라 <strong><u>하부 인프라 작동 고민 없이 바로 실행</u></strong>할 수 있다&#46; 

<a id="1c3eda9b0fe18127b160c38324b3ed90"></a>

이로인해 <strong><code>이벤트 드리븐 아키텍처</code></strong>를 자연스럽게 만들 수  있다&#46;

- <strong><u>이벤트 발생에 따라 일련의 코드 워크플로우</u></strong>를 만들 때 <strong><u>AWS 람다</u></strong>로 소프트웨어 기능을 구현할 수 있다&#46;

- <code>AWS 람다</code>나 <code>다이나모 DB</code> 같은 서버리스 관련 서비스들을 여러 흐름 속 적재적소에 배치하고,<code> AWS 스텝펑션</code>으로 연결하면 <strong><u>이벤트 드리븐 아키텍처를 위한 워크플로우</u></strong>를 짤 수 있다

<a id="1c3eda9b0fe181c0ae2efd34820e6698"></a>

큐를 대규모로 관리할 수 있는 <code>아마존 SQS</code>로 <strong><u>방대한 람다 호출을 무리없이 처리</u></strong>하게하고, 서버리스 애플리케이션을 구축하는 프레임워크 <strong><code>서버리스 애플리케이션 모델(SAM)</code></strong>을 모델을 오픈소스 프로젝트로 제공해 <strong>이벤트 드리븐 아키텍처 애플리케이션을 개발</strong>하도록 지원한다&#46;<br><br>글로벌 스케일 시스템은 항상 어떤 방해를 받게 되는데, 인스턴스 활동 실패 문제를 방지하기 위해 비동기 접근법을 써야 한다<br><code>다이나모DB 스트림</code>이란 기능은 복제 시스템의 스트림을 업데이트하고, 그걸 다른 지역으로 배포하게 해준다<br><br>’아마존 빌더스 라이브러리’에서 이벤트 드리븐 아키텍처를 구성하는데 참고할 수 있는 다양한 패턴 지식을 받을 수 있다

- 아마존웹서비스 전문가들의 지식이 논문 형태로 제공됨
