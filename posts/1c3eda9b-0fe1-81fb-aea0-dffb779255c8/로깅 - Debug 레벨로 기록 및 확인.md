---
order: 14
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1c3eda9b-0fe1-81fb-aea0-dffb779255c8
title: 로깅 - Debug 레벨로 기록 및 확인
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-817c-b119-d6a1706fbaf8
    title: 대규모 시스템 설계
  - id: 1c3eda9b-0fe1-8191-9188-e28e651123f1
    title: RabbitMQ를 이용한 비동기 아키텍처
  - id: 1c3eda9b-0fe1-81fb-aea0-dffb779255c8
    title: 로깅 - Debug 레벨로 기록 및 확인
excerpt: 로깅 --- 로그 레벨 | 로그 레벨 | 설명 | 사용 예시 | | --- | --- | --- | | TRACE | 가장 상세한 로그 | 메서드 실행 흐름, 값 변화 확인 | | DEBUG | 개발 및 디버깅용 | 특정 변수 값 확인, 비즈니스 로직 검증 | | INFO | 일반 정보 | 서비스 실행, API 호출 기록
cover: null
icon: null
notionProperties:
  Tags: 추가
  상태: 완료
schema_version: 1
parent_id: 1c3eda9b-0fe1-8191-9188-e28e651123f1
created: 2025-03-27T07:47:43.051Z
updated: 2025-03-27T07:47:43.051Z
legacy_path: Main/대규모 시스템 설계-d6a1706fbaf8/RabbitMQ를 이용한 비동기 아키텍처-e28e651123f1/로깅 - Debug 레벨로 기록 및 확인-dffb779255c8/index.md
legacy_category: 대규모 시스템 설계
source_url: https://beautiful-college-c84.notion.site/1c3eda9b0fe181fbaea0dffb779255c8
---
<a id="1c3eda9b0fe181c19ee8c5b16446576d"></a>

## 로깅

---

<details>
<summary>로그 레벨</summary>

| 로그 레벨 | 설명 | 사용 예시 |
| --- | --- | --- |
| <code>TRACE</code> | 가장 상세한 로그 | 메서드 실행 흐름, 값 변화 확인 |
| <code>DEBUG</code> | 개발 및 디버깅용 | 특정 변수 값 확인, 비즈니스 로직 검증 |
| <code>INFO</code> | 일반 정보 | 서비스 실행, API 호출 기록 |
| <code>WARN</code> | 경고 (문제 가능성) | 성능 저하, 리소스 부족, 예상치 못한 값 |
| <code>ERROR</code> | 심각한 오류 | 예외 발생, 장애 발생 |

</details>

<details>
<summary>로깅 메세지(<code>String</code>)에 <strong><u>변수 값 추가</u></strong> 시 <code>&#43;</code>자 대신<code> </code><u><code>{}</code></u><u>를 활용</u>한다&#46; </summary>

<details>
<summary><strong>잘못된 방식&#58; </strong><strong><code>&#43;</code></strong><strong> 사용</strong></summary>

- <strong><code>&#43;</code></strong><strong>(문자열 연결 연산자) 사용 시, 불필요한 문자열 연산이 발생되어 성능이 저하된다&#46;</strong>
    - <code>&#43;</code> 연산자 사용 시, <strong><u>문자열이 먼저 연결</u></strong><strong>된 후 </strong><strong><u>로그 메서드가 호출</u></strong>

    - 즉, 로그 레벨이 <code>DEBUG</code>인데 설정이 <u><code>INFO</code></u><u> 이상이라 DEBUG 로그가 출력되지 않</u>더라도 <strong>문자열 연산이 수행</strong><strong>된다&#46;</strong>

- <strong>ex)</strong>
    <a id="1c3eda9b0fe181dbb829d473c584a977"></a>

    ```java
    log.info("사용자 ID: " + userId + ", 주문 ID: " + orderId);
    ```

</details>

<details>
<summary><strong>올바른 방식&#58; </strong><strong><code>{}</code></strong><strong> 사용</strong></summary>

- <strong><code>{}</code></strong><strong>(Placeholder)를 사용하면 </strong><strong><u>필요할 때만 값이 변환</u></strong><strong>된다&#46; (Lazy Evaluation)</strong>
    - <strong>로그 레벨이 활성화된 경우에만 값 변환이 일어남</strong>

    - 즉, <strong><u>로그가 출력될 때</u></strong> SLF4J 내부적으로 <u>toString()을 호출</u>하여 <strong>변수 값을 문자열로 변환</strong>한다&#46;

- <strong>ex)</strong>
    <a id="1c3eda9b0fe1813e9febe773a6d27f47"></a>

    ```java
    log.debug("사용자 ID: {}, 주문 ID: {}", userId, orderId);
    ```

    - 로그 레벨이 INFO 이상이면 debug 로그 자체가 실행되지 않으므로 <strong>문자열 변환 연산도 수행되지 않음</strong> 

    <a id="1c3eda9b0fe18161b8a7ebe75366029e"></a>

             → <strong>성능 최적화</strong>

</details>

</details>

<details>
<summary>lombok&#58; <code>&#64;Slf4j</code></summary>

1. 롬복 의존성 추가
    <a id="1c3eda9b0fe181f5ae61da635dcb13eb"></a>

    ```groovy
    compileOnly 'org.projectlombok:lombok'
    annotationProcessor 'org.projectlombok:lombok'
    ```

1. 로그를 출력하려는 클래스에 <code>&#64;Slf4j</code> 선언
    <a id="1c3eda9b0fe181dbbc06eb6a1a48b6ee"></a>

    ```java
    @Slf4j
    public class ... {
    ```

1. 로그 기록&#58; <code>log&#46;level(” {}”, 변수)</code>
    <a id="1c3eda9b0fe1812a811dcd21a627544a"></a>

    ```java
    // DEBUG 레벨: 디버깅 시 활용할 상세 내역을 적는다. 실제 운영 상황에서는 성능을 잡아먹기 때문에 사용하지 않는다. 
    log.debug();

    // INFO 레벨
    log.info()
    ```

1. debug 레벨 활성화
    - <strong>application&#46;yml</strong>

    <a id="1c3eda9b0fe18124a5fae21f69a6c679"></a>

    ```yaml
    logging:
      level:
        root: DEBUG  # 기본 로그 레벨: DEBUG, INFO, WARN, ERROR
        # com.prac.rabbimq: DEBUG  # 특정 패키지에 대해 DEBUG 로그 활성화
    ```

</details>
