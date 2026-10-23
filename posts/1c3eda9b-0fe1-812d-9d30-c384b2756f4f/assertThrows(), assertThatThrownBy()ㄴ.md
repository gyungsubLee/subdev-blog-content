---
order: 24
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1c3eda9b-0fe1-812d-9d30-c384b2756f4f
title: assertThrows(), assertThatThrownBy()ㄴ
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-817c-b119-d6a1706fbaf8
    title: 대규모 시스템 설계
  - id: 1c3eda9b-0fe1-8151-a9bf-f4bde443f283
    title: 대규모 시스템 설계 - 게시판
  - id: 1c3eda9b-0fe1-812d-9d30-c384b2756f4f
    title: assertThrows(), assertThatThrownBy()ㄴ
excerpt: "[ 🧐 비교 ] assertThrows() vs assertThatThrownBy() --- 📖 assertThrows() 와 assertThatThrownBy() 는 둘 다 예외를 테스트할 수 있지만, 사용하는 방식과 기능 측면에서 약간의 차이점이 있다. 1. assertThrows() [ JUnit ] java a"
cover: null
icon: null
notionProperties:
  Tags: 추가
  상태: 완료
schema_version: 1
parent_id: 1c3eda9b-0fe1-8151-a9bf-f4bde443f283
created: 2025-03-27T07:52:18.506Z
updated: 2025-03-27T07:52:18.506Z
legacy_path: Main/대규모 시스템 설계-d6a1706fbaf8/대규모 시스템 설계 - 게시판-f4bde443f283/assertThrows(), assertThatThrownBy()ㄴ-c384b2756f4f/index.md
legacy_category: 대규모 시스템 설계
source_url: https://beautiful-college-c84.notion.site/1c3eda9b0fe1812d9d30c384b2756f4f
---
<a id="1c3eda9b0fe18127a82feff2cb23e35c"></a>

## <strong>&#91; 🧐 비교 &#93; </strong><strong><code>assertThrows</code></strong><strong><code>()</code></strong><strong> vs </strong><strong><code>assertThatThrownBy</code></strong><strong><code>()</code></strong><strong> </strong>

---

> 📖 
> 
> <a id="1c3eda9b0fe181f8b3b1e8ea4083d0e5"></a>
> 
> <code>assertThrows()</code> 와 <code>assertThatThrownBy()</code> 는 <strong>둘 다 예외를 테스트</strong>할 수 있지만,<br> 사용하는 방식과 기능 측면에서 <strong>약간의 차이점</strong>이 있다&#46;

<a id="1c3eda9b0fe18173b40bf53606851527"></a>

### <strong>1&#46; </strong><strong><code> </code></strong><strong><code>assertThrows</code></strong><strong><code>()</code></strong><strong> &#91; JUnit &#93;</strong>

<a id="1c3eda9b0fe1811ca17ff1fa684fc259"></a>

```java
assertThrows(IllegalArgumentException.class,
    () -> CommentPath.create("zzzzz".repeat(5)).createChildCommentPath(null));
```

<details>
<summary>특징</summary>

- <strong>JUnit5</strong> 표준 API

- 기대한 예외가 <strong>정확히 발생하는지 확인</strong>만 함

<details>
<summary><strong>예외 객체를 반환</strong>받을 수도 있음</summary>

<a id="1c3eda9b0fe181339f79f5679ad0e9b4"></a>

```java
IllegalArgumentException ex = assertThrows(IllegalArgumentException.class, () -> {
    ...
});
assertEquals("depth overflowed", ex.getMessage());
```

</details>

</details>

<a id="1c3eda9b0fe181b5b9e1cc79912b3dc2"></a>

### 2&#46; <strong> </strong><strong><code>assertThatThrownBy</code></strong><strong><code>()</code></strong><strong> &#91; AssertJ &#93;</strong>

<a id="1c3eda9b0fe1811da405dd6286d452e7"></a>

```java
assertThatThrownBy(() -> CommentPath.create("zzzzz".repeat(5)).createChildCommentPath(null))
    .isInstanceOf(IllegalArgumentException.class);
```

<details>
<summary>특징</summary>

- <strong>AssertJ</strong> 라이브러리의 fluent assertion

- assertThat()처럼 <strong>체이닝 문법(fluent API)</strong> 사용 가능

<details>
<summary>예외의 종류, 메시지, 원인 등 여러 가지를 <strong>더 세밀하게 검사 가능</strong></summary>

<a id="1c3eda9b0fe1810aa78dc7b437a16a30"></a>

```java
assertThatThrownBy(() -> { ... })
    .isInstanceOf(IllegalArgumentException.class)
    .hasMessage("depth overflowed")
    .hasNoCause();
```

</details>

</details>

<a id="1c3eda9b0fe18117a7befdbf9dc52af7"></a>

<strong>정리</strong>

| <strong>항목</strong> | assertThrows | assertThatThrownBy |
| --- | --- | --- |
| 소속 | J<strong>U</strong>nit5 | AssertJ |
| 주 용도 | 예외 발생 여부 확인 | 예외 타입, 메시지 등 상세 체크 |
| 반환값 | 예외 객체 | AbstractThrowableAssert (체이닝 가능) |
| 문법 스타일 | 간결 | 유창(fluent), 가독성 ↑ |
| 의존성 | JUnit만 있으면 됨 | AssertJ 추가 필요 |

> ✏️ 
> 
> - <strong>심플한 테스트&#58; </strong><code>assertThrows</code>
>     - <strong> 간단한 예외 확인만 필요할 때,</strong><code>assertThrows</code> 사용
> 
> - <strong>정교한 조건까지 확인하는 테스트&#58; </strong><code>assertThatThrownBy</code>
>     -  <strong>예외 메시지까지 체크하거나, 여러 조건을 체이닝으로 검증</strong>하고 싶다면, <code>assertThatThrownBy</code> 사용

<a id="1c3eda9b0fe181d0b1d3d2d539e80707"></a>

## 자주쓰는 패턴 정리

---

<a id="1c3eda9b0fe18156a873d0dd5591d3f2"></a>

### 1&#46; <strong> </strong><strong><code>assertThrows</code></strong><strong> 실전 예제 (</strong><strong><code>JUnit5</code></strong><strong>)</strong>

- 기본 패턴
    <a id="1c3eda9b0fe1816290d1c0588fd35c7b"></a>

    ```java
    @Test
    void shouldThrowExceptionWhenInputIsInvalid() {
        assertThrows(IllegalArgumentException.class, () -> {
            someService.doSomething(null);
        });
    }
    ```

- <strong> 예외 메시지까지 검증</strong>
    <a id="1c3eda9b0fe18160984ee4c3e72ce657"></a>

    ```java
    @Test
    void shouldThrowWithCorrectMessage() {
        IllegalArgumentException ex = assertThrows(IllegalArgumentException.class, () -> {
            someService.doSomething("bad input");
        });

        assertEquals("invalid input provided", ex.getMessage());
    }
    ```

- <strong>장점</strong>
    - 단순하고 직관적

    - 테스트 중 try&#45;catch 없이 깔끔

<a id="1c3eda9b0fe1816f9702d79ada3f8ce9"></a>

### 2&#46; <strong> </strong><strong><code>assertThatThrownBy</code></strong><strong> 실전 예제 (</strong><strong><code>AssertJ</code></strong><strong>)</strong>

- <strong>AssertJ 의존성 (Gradle)</strong>
    <a id="1c3eda9b0fe1810db5ece18ee5e68b1e"></a>

    ```java
    // build.gradle
    testImplementation 'org.assertj:assertj-core:3.25.1' // 최신 버전 확인 권장
    ```

- 기본 패턴
    <a id="1c3eda9b0fe181afb621cfe96f8954d8"></a>

    ```java
    @Test
    void shouldThrowUsingAssertJ() {
        assertThatThrownBy(() -> {
            someService.doSomething(null);
        }).isInstanceOf(IllegalArgumentException.class);
    }
    ```

- <strong> 예외 메시지 검증</strong>
    <a id="1c3eda9b0fe181a79c0cc4aaef09ab86"></a>

    ```java
    @Test
    void shouldThrowWithDetailedChecks() {
        assertThatThrownBy(() -> {
            someService.doSomething("wrong");
        })
        .isInstanceOf(IllegalArgumentException.class)
        .hasMessage("invalid input")
        .hasNoCause();
    }
    ```

- <strong>예외 체이닝 (원인 확인)</strong>
    <a id="1c3eda9b0fe181b5bc1fd614ab44a8f2"></a>

    ```java
    @Test
    void shouldHaveCause() {
        assertThatThrownBy(() -> {
            throw new RuntimeException("outer", new IllegalArgumentException("inner"));
        })
        .isInstanceOf(RuntimeException.class)
        .hasCauseInstanceOf(IllegalArgumentException.class)
        .hasRootCauseMessage("inner");
    }
    ```
