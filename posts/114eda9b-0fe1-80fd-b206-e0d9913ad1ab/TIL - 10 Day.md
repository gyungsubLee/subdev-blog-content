---
order: 50
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 114eda9b-0fe1-80fd-b206-e0d9913ad1ab
title: TIL - 10 Day
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 108eda9b-0fe1-80a6-8a2b-c21df3ab9492
    title: 내일 배움 캠프 ( 백엔드 코스 7기)
  - id: 10aeda9b-0fe1-8045-a8c4-f10918253453
    title: TIL
  - id: 114eda9b-0fe1-80fd-b206-e0d9913ad1ab
    title: TIL - 10 Day
excerpt: 💡 PDS 다이어리 참조 PlAN ( 오늘 학습할 내용들 ) --- - [ ] 스프링 MVC - 멀티 쓰레드 ( 정리 중 ) DO ( 오늘 공부한 내용) --- 멑티 쓰레드 페이지 - 페이지 - 멀티쓰레드 - 단일 요청 - 쓰레드 1개 - 다중 요청 - 쓰레드 1개 - 다중 요청 - 요청마다 쓰레드 생성 - 다중요청 -
cover: null
icon: null
notionProperties:
  날짜: 2024-10-03
  Category: TIL
  Keyword: "• 멀티 쓰레드 "
schema_version: 1
parent_id: 10aeda9b-0fe1-8045-a8c4-f10918253453
created: 2024-10-03T14:37:12.053Z
updated: 2024-10-18T04:52:31.781Z
legacy_path: Main/내일 배움 캠프 ( 백엔드 코스 7기)-c21df3ab9492/TIL-f10918253453/TIL - 10 Day-e0d9913ad1ab/index.md
legacy_category: 내일 배움 캠프 ( 백엔드 코스 7기)
source_url: https://beautiful-college-c84.notion.site/114eda9b0fe180fdb206e0d9913ad1ab
---
> 💡 
> 
> <a id="114eda9b0fe1812692abf83a1c3adcac"></a>
> 
> PDS 다이어리 참조

<a id="114eda9b0fe18184b47bd940f9ae1a9c"></a>

### PlAN ( 오늘 학습할 내용들 )

---

- [ ] 스프링 MVC &#45; 멀티 쓰레드  ( 정리 중 )

<a id="114eda9b0fe181ada2bdd5d539c96ccf"></a>

### DO ( 오늘 공부한 내용)

---

<details>
<summary>멑티 쓰레드</summary>

> <a href="https://beautiful-college-c84.notion.site/1b7f90570a2b4ef3bb0a1d3d8969c6c3">페이지</a> &#45; <a href="https://beautiful-college-c84.notion.site/aab961c4454048bead11c7980a27862a">페이지</a> &#45; 멀티쓰레드

- 단일 요청  &#45; 쓰레드 1개

- 다중 요청 &#45; 쓰레드 1개

- 다중 요청  &#45; 요청마다 쓰레드 생성

- 다중요청  &#45; 쓰레드 풀
    - 보통 WAS에 쓰레드 풀이 구현되어 있다&#46; 

<details>
<summary>🧐 WAS의 주요 튜닝 표인트는 거의 <code>Max Thread</code> 이다&#46;</summary>

<a id="114eda9b0fe18079bc5ffcd3fca28343"></a>

Max Thread 튜닝 시, 극적인 효과를 볼 확률이 높으나, 너무 높거나 낮게 설정하면 아래와 같은 문제가 발생 될 수 있다&#46;

- max thread 값을 너무 <strong><u>낮</u></strong>게 설정
    - 동시 요청이 많으면, 서버 리소스는 여유롭지만, 클라이언트에게 받아오는 응답들이 지연된다&#46;

- max thread 값을 너무 <strong><u>높</u></strong>게 설정
    - 동시 요청이 많으면 CPU, 메모리 리소스의 임계점이 초과되어 서버가 다운된다&#46;

</details>

<details>
<summary>🧐 스프링 부트 톰캣 <code>Max Thread</code> 설정</summary>

<a id="114eda9b0fe180a3bdc6c03beacd33b4"></a>

스프링부트에는 기본적으로 내장된 톰캣 서버가 존재하기에, <code>application&#46;properties</code>, <code>application&#46;yml</code>에서 Tomcat 설정을 쉽게 조정 할 수 있다&#46; 

<details>
<summary>1) application&#46;properties &#45; max thread</summary>

<a id="bdeebd55418c4ebe907494c36ba512a6"></a>

```javascript
server.tomcat.max-threads=300
```

</details>

<details>
<summary>2) <strong>application&#46;yml</strong></summary>

<a id="114eda9b0fe180edbf50eeea730e955d"></a>

```javascript
server:
  tomcat:
    max-threads: 300
```

</details>

<details>
<summary>3) Tomcat 커넥터 직접 설정</summary>

<a id="114eda9b0fe180c5bba3ee61201b9bf2"></a>

더 세부적인 설정이 필요한 경우, TomcatServletWebServerFactory 빈을 사용해 직접 설정할 수 있다&#46; 

<details>
<summary><strong>ex) TomcatServletWebServerFactory 빈을 통한 세부 설정</strong></summary>

- <code>maxThreads</code>&#58; 최대 쓰레드 수

<details>
<summary><code>minSpareThreads</code></summary>

- 최소 스레드 수를 설정

- 서버가 항상 유지하는 대기 스레드 수를 의미하며 요청이 없을 때에도 일정 수의 스레드를 유지한다&#46;

</details>

<details>
<summary><code>acceptCount</code></summary>

- maxThreads가 모두 사용 중일 때 대기할 수 있는 최대 요청 수를 설정

- 이 수를 초과하면 클라이언트는 연결을 거부 당할 수 있다&#46; 

</details>

<a id="862d401bd94d426b8e80db50fe3229c5"></a>

```javascript
import org.springframework.boot.web.embedded.tomcat.TomcatServletWebServerFactory;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;

@Configuration
public class TomcatConfig {

    @Bean
    public TomcatServletWebServerFactory tomcatFactory() {
        TomcatServletWebServerFactory factory = new TomcatServletWebServerFactory();
        factory.addConnectorCustomizers(connector -> {
            connector.setProperty("maxThreads", "300");  // 최대 스레드 수 설정
            connector.setProperty("minSpareThreads", "20");  // 최소 대기 스레드 수 설정
            connector.setProperty("acceptCount", "100");  // 대기 큐에서 기다릴 수 있는 최대 요청 수
        });
        return factory;
    }
}
```

- 최대 쓰래드 수는 ‘300’개 이고, (<code>maxTheads = 300</code>)

-  최소  20개의 쓰레드를 대기 상태로 유지하여 즉시 요청을 처리할 수 있도록 준비한다&#46; (<code>minSpareTheads = 20</code>)

- 300개의 쓰레드가 모두 사용 중일 때, 추가로 100개의 요청을 대기 큐에 넣는다&#46; (<code>acceptCount = 100</code>)

</details>

</details>

</details>

</details>

<a id="114eda9b0fe1810e8765e73e2450793e"></a>

### SEE ( 피드백 )

---

- 멀티쓰레드… 공부하면서 모르는게 너무 많아서 계속 파고 들어갔다… 추가 공부 필수다

- 오랜만에 거의 오후까지 잤고 운동도 하고 카페가서 맛있는 거도 먹음 → 힐링 제대로함
