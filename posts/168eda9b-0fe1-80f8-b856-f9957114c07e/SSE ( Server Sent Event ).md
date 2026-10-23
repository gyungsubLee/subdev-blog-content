---
order: 82
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 168eda9b-0fe1-80f8-b856-f9957114c07e
title: SSE ( Server Sent Event )
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 108eda9b-0fe1-80a6-8a2b-c21df3ab9492
    title: 내일 배움 캠프 ( 백엔드 코스 7기)
  - id: 168eda9b-0fe1-80f8-b856-f9957114c07e
    title: SSE ( Server Sent Event )
excerpt: "reference ‣ ‣ 서버에서 추가된 알람을 클라이언트에게 알려주는 방식은 크게 3가지가 존재한 - 폴링 방식 : 클라이언트 사이드에서 주기적인 요청을 통해 구현 - 웹소켓 방식: 효율적인 양방향 실시간 통신을 위해 새로운 프로토골을 사용하여 통신하는 웹소켓 방식 - SSE(Server-Sent-Events): 서버가"
cover: null
icon: null
notionProperties: {}
schema_version: 1
parent_id: 108eda9b-0fe1-80a6-8a2b-c21df3ab9492
created: 2024-12-26T12:09:20.039Z
updated: 2024-12-26T13:04:04.757Z
legacy_path: Main/내일 배움 캠프 ( 백엔드 코스 7기)-c21df3ab9492/SSE ( Server Sent Event )-f9957114c07e/index.md
legacy_category: 내일 배움 캠프 ( 백엔드 코스 7기)
source_url: https://beautiful-college-c84.notion.site/168eda9b0fe180f8b856f9957114c07e
---
<details>
<summary>reference</summary>

<a id="168eda9b0fe18031bed2f5e2a98f6a70"></a>

‣

<a id="168eda9b0fe180c5a63fc47b806cb9f2"></a>

‣

</details>

<a id="168eda9b0fe180d1af70c7f6298e6af0"></a>

서버에서 추가된 알람을 클라이언트에게 알려주는 방식은 크게 3가지가 존재한

- <strong><code>폴링 방식</code></strong> &#58; <u>클라이언트</u> 사이드에서 <u>주기적인 요청</u>을 통해 구현

- <code>웹소켓 방식</code>&#58; 효율적인 <u>양방향 실시간 통신</u>을 위해 새로운 프로토골을 사용하여 통신하는 웹소켓 방식

- SSE(Server&#45;Sent&#45;Events)&#58; 서버가 클라이언트로 실시간 정보를 자동으로 보낼 수 있도록 하는 기술

<a id="168eda9b0fe18053b60adb9ec82a45b4"></a>

## SSE

![](ffa38e6500fde3f1.webp)

<a id="168eda9b0fe1801488e5cc5e7277aa7b"></a>

이름 그대로 서버가 클라이언트로 실시간 정보를 자동으로 보낼 수 있도록 하는 기술이다&#46; 

<a id="168eda9b0fe18057981ce1991212b90d"></a>

첫 구독 정보를 갱신 후, 이후 클라이언트에서 요청이 없이 응답값을 전송할 수 있다&#46; 

<a id="168eda9b0fe180959226f215cc0d8f8a"></a>

이를 알람 기능에 사용한다면,  첫 구독 요청 이후 계속 connetion을 유지하여 트리거 설정한 이벤트가 발생 시 해당하는 알람 응답값을  클라이언트에서의 요청없이 보낼 수 있다&#46; 

<a id="168eda9b0fe180cc84b0f18ca7052c7b"></a>

그렇다면 여기서 아래와 같은 기술 구현에 있어서 고려해야 될 사항이 있는데,

- 어떻게 클라이언트로 부터 처음 구독 정보를 갱신 받는가?

- 어떤 이벤트를 트리거로써 다루는가?

- 어떤 메세지 정보를 생성해야 하는가?

- 어떻게, 언제까지 connection을 유지하는가? 

- 또한 이후 재요청은 어떤 방식으로 갱신되는가?  

>  비동기 통신에 대한 부분은 해당 기술에서 다룸  &#45; <a href="https://beautiful-college-c84.notion.site/168eda9b0fe18002927efec89a5a8b58">페이지</a> 

<a id="168eda9b0fe18058913cca8306f3e7d1"></a>

로 볼수 있다&#46; 

<a id="168eda9b0fe180229c04d8b988371f86"></a>

### 질문 1 &#45; 어떻게 클라이언트로 부터 첫 구독 정보를 갱신 받는가?

---

> 첫 구독에 대한 엔드포인트를 어떻게 생성하고 서버로 보내는가?

![](40631152f46b7d7b.webp)

![](f0f16021b3709cb7.webp)

![](3281b9bc54d29ee3.webp)

<a id="168eda9b0fe1804d96a2cc8e14f3c82a"></a>

해당 의문점에 대해서 서칭해본 결과, 위와 같이<strong><u> 알람에 대한 요청을 허용</u></strong> 시,이를 구독에 대한 트리거로 판단하여

<a id="168eda9b0fe180d99c4bdebd8fbd3cff"></a>

이후 클라이언트 측에서 엔드포인트 URL 과 키를 생성해서 서버로 보낸다고 한다&#46;
