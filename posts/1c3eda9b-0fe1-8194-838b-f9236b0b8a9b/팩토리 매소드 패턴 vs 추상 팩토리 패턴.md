---
order: 1
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1c3eda9b-0fe1-8194-838b-f9236b0b8a9b
title: 팩토리 매소드 패턴 vs 추상 팩토리 패턴
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-8188-9ddf-e42c6289f47d
    title: 디자인패턴
  - id: 1c3eda9b-0fe1-81c2-b6ea-c9b4c4c77f6e
    title: "[ 백기선 ] GoF 디자인패턴"
  - id: 1c3eda9b-0fe1-8194-838b-f9236b0b8a9b
    title: 팩토리 매소드 패턴 vs 추상 팩토리 패턴
excerpt: 배경 --- 팩토리 메서드 패턴 예제의 문제점을 추상 팩토리 패턴으로 개선했다. 여기서 아래와 같은 의문점이 들었다. 🧐 질문 1) 팩토리 메서드 패턴을 개선한 패턴이 추상 팩토리 패턴 인가? 질문 2) 그러면 팩토리 메서드 패턴은 사용하지 않는가? 해당 의문점을 학습 후, 해당 포스팅으로 정리한다. 1. 팩토리 메서드
cover: null
icon: null
notionProperties:
  Tags: 추가
  상태: 완료
schema_version: 1
parent_id: 1c3eda9b-0fe1-81c2-b6ea-c9b4c4c77f6e
created: 2025-03-27T07:47:13.030Z
updated: 2026-04-15T14:34:23.765Z
legacy_path: Main/디자인패턴-e42c6289f47d/[ 백기선 ] GoF 디자인패턴-c9b4c4c77f6e/팩토리 매소드 패턴 vs 추상 팩토리 패턴-f9236b0b8a9b/index.md
legacy_category: 디자인패턴
source_url: https://beautiful-college-c84.notion.site/1c3eda9b0fe18194838bf9236b0b8a9b
---
<a id="1c3eda9b0fe1819f82a4f5f3f992e05e"></a>

### 배경

---

<a id="1c3eda9b0fe18130b3a1cab4a0b27794"></a>

팩토리 메서드 패턴 예제의 문제점을 추상 팩토리 패턴으로 개선했다&#46; 

<a id="1c3eda9b0fe181ccb919d2a832539d85"></a>

여기서 아래와 같은 의문점이 들었다&#46; 

> 🧐 
> 
> <a id="1c3eda9b0fe1814485bff9efa79d236f"></a>
> 
> 질문 1) <code>팩토리 메서드 패턴</code>을 개선한 패턴이 <code>추상 팩토리 패턴</code> 인가?
> 
> <a id="1c3eda9b0fe181f2ada5f5a2718819bf"></a>
> 
> 질문 2) 그러면 <code>팩토리 메서드 패턴</code>은 사용하지 않는가?

<a id="1c3eda9b0fe181f58442f8fa2936cc36"></a>

해당 의문점을 학습 후, 해당 포스팅으로 정리한다&#46; 

<a id="1c3eda9b0fe1813381e3f4110631af80"></a>

### <strong>1&#46;  </strong><strong><code>팩토리 메서드 패턴</code></strong><strong> 과 </strong><strong><code>추상 팩토리 패턴</code></strong><strong>은 사용 목적이 다르다&#46; </strong>

---

> ✏️ 
> 
> <a id="1c3eda9b0fe181bea8aeccf340efdbea"></a>
> 
> <strong><code>팩토리 메서드 패턴</code></strong>과 <strong><code>추상 팩토리 패턴</code></strong>은 <strong><u>각각의 역할과 목적이 다르</u></strong><strong><u>며,</u></strong><strong> <br></strong><strong><code>추상 팩토리</code></strong>가 반드시<strong> </strong><strong><code>팩토리 메서드</code></strong>의 <strong>‘개선 버전’은 아니다&#46;</strong>

<a id="1c3eda9b0fe181b1b5b5c2f8597eb88d"></a>

<strong><code>팩토리 메서드 패턴</code></strong>은 <strong>단일 제품 생성</strong><strong>에 있어서 </strong><strong><u>확장성과 테스트 용이성을 갖춘 좋은 패턴</u></strong>이다&#46;

<details>
<summary>ex) 실무 사용 예시</summary>

- Spring의 <code>BeanFactory</code>

- Spring의 <code>FactoryBean&#60;T&#62;</code>

- 자바의 <code>Calendar&#46;getInstance()</code>, <code>Logger&#46;getLogger()</code>, <code>DocumentBuilderFactory&#46;newInstance()</code> 등

</details>

<a id="1c3eda9b0fe181c3be8edb35c7aeaf0f"></a>

### 2&#46; 비교

---

| <strong>구분</strong> | <strong>팩토리 메서드 패턴</strong> | <strong>추상 팩토리 패턴</strong> |
| --- | --- | --- |
| 생성 대상 | <strong>하나의 객체 (제품)</strong> | <strong>관련된 제품군 전체</strong> |
| 책임 분리 수준 | 단일 객체 생성 책임 분리 | 구성 요소(Anchor, Wheel 등)까지 분리 |
| 복잡도 | 비교적 단순 | 더 복잡하고 추상화 수준 높음 |
| 유연성 | 제품 하나 생성만 할 경우 유리 | 관련 제품을 일관되게 생성해야 할 경우 유리 |
| 사용 시기 | 객체 1&#126;2개 만들고 끝일 때 | 관련된 객체 여러 개를 세트로 만들어야 할 때 |

<a id="1c3eda9b0fe181698d0fd4ff41729a66"></a>

즉, <strong><u>단일 객체 생성</u></strong>만으로 충분하면 팩토리 메서드가 더 <strong>간단하고 적합</strong><strong>하다&#46;</strong>

<a id="1c3eda9b0fe181e19054ff6181141cad"></a>

하지만 <strong><u>관련 구성 요소(Anchor, Wheel 등)까지 다양해질 경우</u></strong>에는 추상 팩토리가 더 <strong>강력한 설계 방식</strong>이다

<a id="1c3eda9b0fe181468ba1ceee3456cc6b"></a>

또한 실제 설계에서는 같이 쓰는 경우도 많다&#46; 

<details>
<summary><strong>팩토리 메서드 패턴을 이용해 추상 팩토리 패턴을 구현하는 경우가 많다&#46;</strong></summary>

<a id="1c3eda9b0fe1812ba58ec3ebd09f3f5e"></a>

```java
public interface ShipPartsFactory {
    Anchor createAnchor(); // => 팩토리 메서드
    Wheel createWheel();   // => 팩토리 메서드
}
```

-  <code>추상 팩토리</code>는 <strong><u>여러 개의 팩토리 메서드를 모아둔 상위 개념</u></strong>이라고 볼 수 있다&#46;

</details>

<a id="1c3eda9b0fe1816796fceb818f9f0616"></a>

### 3&#46; 답변 정리

| <strong>질문</strong> | <strong>답변</strong> |
| --- | --- |
| 팩토리 메서드 패턴의 개선책이 추상 팩토리 패턴인가? | ❌ “개선책”이 아니다&#46; 두 패턴의 사용 목적이 다르다&#46; |
| 팩토리 메서드 패턴은 사용되지 않는가? | ❌ 자주 사용한다&#46; 특히 단일 객체 생성 시 유용하다&#46; |
| 언제 추상 팩토리를 사용하는가? | 관련된 여러 객체를 세트로, 일관성 있게 생성할 필요가 있을 때이다&#46; |
