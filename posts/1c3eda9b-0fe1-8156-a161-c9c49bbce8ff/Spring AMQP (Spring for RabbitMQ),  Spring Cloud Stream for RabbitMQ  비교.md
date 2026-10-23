---
order: 6
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1c3eda9b-0fe1-8156-a161-c9c49bbce8ff
title: Spring AMQP (Spring for RabbitMQ),  Spring Cloud Stream for RabbitMQ  비교
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-817c-b119-d6a1706fbaf8
    title: 대규모 시스템 설계
  - id: 1c3eda9b-0fe1-8191-9188-e28e651123f1
    title: RabbitMQ를 이용한 비동기 아키텍처
  - id: 1c3eda9b-0fe1-8156-a161-c9c49bbce8ff
    title: Spring AMQP (Spring for RabbitMQ),  Spring Cloud Stream for RabbitMQ  비교
excerpt: Spring for RabbitMQ, Spring Cloud Stream for RabbitMQ 비교 --- Spring for RabbitMQ (Spring AMQP ) ✏️ Spring AMQP는 RabbitMQ와 직접 통신하는 로우 레벨 API를 제공하는 라이브러리이디. 특징 - Spring이 제공하는 RabbitT
cover: null
icon: null
notionProperties:
  Tags: 추가
  상태: 완료
  다중 선택: 추가 정리
schema_version: 1
parent_id: 1c3eda9b-0fe1-8191-9188-e28e651123f1
created: 2025-03-27T07:47:43.049Z
updated: 2026-03-25T03:19:58.669Z
legacy_path: Main/대규모 시스템 설계-d6a1706fbaf8/RabbitMQ를 이용한 비동기 아키텍처-e28e651123f1/Spring AMQP (Spring for RabbitMQ),  Spring Cl-c9c49bbce8ff/index.md
legacy_category: 대규모 시스템 설계
source_url: https://beautiful-college-c84.notion.site/1c3eda9b0fe18156a161c9c49bbce8ff
---
<a id="1c3eda9b0fe1818fb464c600d4780d67"></a>

## <strong> </strong><code>Spring for RabbitMQ</code>,  <strong><code>Spring Cloud Stream for RabbitMQ</code></strong><strong>  비교</strong>

---

<a id="1c3eda9b0fe18174a599f0050bbc8b38"></a>

### <strong>Spring for RabbitMQ (Spring AMQP )</strong>

> ✏️ 
> 
> <a id="1c3eda9b0fe1810ca521e306b67bcbd7"></a>
> 
> <strong>Spring AMQP</strong>는 <u>RabbitMQ와 직접 통신</u>하는 <strong><u>로우 레벨 API</u></strong>를 제공하는 라이브러리이디&#46;

<details>
<summary>특징</summary>

- Spring이 제공하는 RabbitTemplate을 사용하여 <strong>직접 메시지를 송수신 가능</strong>

- <code>&#64;RabbitListener</code>를 사용하여 메시지를 처리 가능

- <strong>RabbitMQ의 모든 기능 제어 가능</strong> (Exchange, Queue, Routing Key 등)

- <strong>코드를 직접 관리</strong>
    - 생산자/소비자를 직접 구현

</details>

<details>
<summary>장점</summary>

- <strong>RabbitMQ의 고급 기능 사용 가능</strong> (Exchange 타입, Routing Key, TTL 등)
    - 커스터마이징이 가능하여 <strong>세밀한 설정이 필요할 때 적합</strong>하다&#46;

</details>

<details>
<summary>단점</summary>

- 직접 RabbitMQ 설정을 다뤄야 하므로 <strong>구현할 코드가 많음</strong>
    - 유지보수 측면이 증가함

- RabbitMQ에 강하게 종속됨
    - <strong>추후 메시지 브로커 변경 시 수정 비용 증가함</strong>

</details>

<details>
<summary>사용 예시</summary>

<details>
<summary><strong>Producer ( 메세지 전송 )</strong></summary>

<a id="1c3eda9b0fe181739c28ccfb54f1040b"></a>

```java
@RestController
@RequiredArgsConstructor
public class MessageProducer {
    
    private final RabbitTemplate rabbitTemplate;

    @PostMapping("/send")
    public String sendMessage(@RequestParam String message) {
        rabbitTemplate.convertAndSend("my-exchange", "my-routing-key", message);
        return "Message sent!";
    }
}
```

</details>

<details>
<summary><strong> Consumer ( 메시지 수신 )</strong></summary>

<a id="1c3eda9b0fe18151affbf27fdd458736"></a>

```java
@Component
public class MessageConsumer {

    @RabbitListener(queues = "my-queue")
    public void receiveMessage(String message) {
        System.out.println("Received: " + message);
    }
}
```

</details>

</details>

<a id="1c3eda9b0fe1816a8fcfd6a89ffd6f7f"></a>

### <strong>Spring Cloud Stream for RabbitMQ</strong>

---

> ✏️ 
> 
> <a id="1c3eda9b0fe181f5a5f1cc17cd360dbd"></a>
> 
> <strong>Spring Cloud Stream</strong>은 <strong><u>메시지 브로커를 추상화</u></strong>하여 RabbitMQ, Kafka 등을 쉽게 연동할 수 있다&#46;

<details>
<summary>장점</summary>

- <strong><u>메시지 브로커</u></strong>(RabbitMQ, Kafka 등)를 <strong>유연하게 변경 가능</strong>
    - <strong>설정만 변경하면 메시징 시스템을 변경할 수 있어</strong><strong><u> 유지보수성이 뛰어남</u></strong>
        - <strong>메시징 코드를 간단하게 유지 가능</strong>

        <a id="1c3eda9b0fe1819492c9edb56ffab78f"></a>

              &#45;&#62; <code>&#64;EnableBinding</code>, <code>&#64;StreamListener</code> 사용

- <strong><u>생산자/소비자 간</u></strong><strong> </strong><strong><u>결합도가 낮</u></strong><strong>아</strong> 서비스 간 독립성이 높아짐

- 애플리케이션이 <u>특정 메시지 브로커(RabbitMQ)에 종속되지 않</u>도록 설계 가능

</details>

<details>
<summary>단점</summary>

- <strong>RabbitMQ의 세부 설정을 직접 다루기 어려움</strong>

- <strong>고급 기능(TTL, Dead Letter Queue 등) 사용이 제한적</strong>&#46;

</details>

<details>
<summary>예시 </summary>

<details>
<summary><strong>application&#46;yml</strong></summary>

<a id="1c3eda9b0fe181db8d0dd7d4b203afdf"></a>

```yaml
spring:
  cloud:
    stream:
      bindings:
        output:  # 메시지 전송 채널
          destination: my-queue
          binder: rabbit
        input:   # 메시지 수신 채널
          destination: my-queue
          binder: rabbit
      rabbit:
        bindings:
          input:
            consumer:
              auto-bind-dlq: true
```

</details>

<details>
<summary><strong>Producer ( 메세지 전송 )</strong></summary>

<a id="1c3eda9b0fe1813f9597ea3386ad69b2"></a>

```java
@EnableBinding(Source.class)
@RestController
@RequiredArgsConstructor
public class StreamProducer {

    private final MessageChannel output;

    @PostMapping("/send")
    public String sendMessage(@RequestParam String message) {
        output.send(MessageBuilder.withPayload(message).build());
        return "Message sent!";
    }
}
```

</details>

<details>
<summary><strong> Consumer ( 메시지 수신 )</strong></summary>

<a id="1c3eda9b0fe181b9856fd1d70c9c7f23"></a>

```java
@EnableBinding(Sink.class)
@Component
public class StreamConsumer {

    @StreamListener(Sink.INPUT)
    public void receiveMessage(String message) {
        System.out.println("Received: " + message);
    }
}
```

</details>

</details>

<a id="1c3eda9b0fe1811597f9ca0d6404dd7e"></a>

### 비교

| 비교 항목 | <strong>Spring AMQP (RabbitMQ)</strong> | <strong>Spring Cloud Stream (RabbitMQ Stream)</strong> |
| --- | --- | --- |
| <strong>사용 목적</strong> | RabbitMQ와 직접 통신 | 메시지 브로커 추상화 |
| <strong>설정 방식</strong> | <code>RabbitTemplate</code>, <code>&#64;RabbitListener</code> | <code>&#64;EnableBinding</code>, <code>&#64;StreamListener</code> |
| <strong>메시지 브로커</strong> | RabbitMQ에 종속 | RabbitMQ, Kafka 등 유연하게 변경 가능 |
| <strong>구현 난이도</strong> | 직접 구현해야 함 | 간결한 코드로 메시지 처리 가능 |
| <strong>확장성</strong> | RabbitMQ에 최적화됨 | 다양한 메시지 브로커 지원 |
| <strong>고급 기능 사용</strong> | 가능 (Exchange, TTL, Dead Letter 등) | 제한적 |

<a id="1c3eda9b0fe1814f9168f7f21a1ffee2"></a>

### 사용 권장

| 사용 사례 | <strong>Spring AMQP</strong> | <strong>Spring Cloud Stream</strong> |
| --- | --- | --- |
| <strong>RabbitMQ의 고급 기능 사용 (Exchange, Routing 등)</strong> | ✅ 추천 | ❌ 제한적 |
| <strong>RabbitMQ 전용 애플리케이션 개발</strong> | ✅ 추천 | ❌ 비추천 |
| <strong>메시지 브로커 유연성 필요 (Kafka, RabbitMQ 변경 가능성 있음)</strong> | ❌ 비추천 | ✅ 추천 |
| <strong>간단한 메시징 시스템 구현</strong> | ❌ 직접 구현해야 함 | ✅ 간단하게 구현 |
