---
order: 6
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1c3eda9b-0fe1-815b-82d2-f4632514eeb3
title: 스프링 부트, JPA 활용 1 - 웹 애플리케이션 개발
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-81ae-909e-cd1f71740107
    title: Spring ( Java )
  - id: 1c3eda9b-0fe1-815b-82d2-f4632514eeb3
    title: 스프링 부트, JPA 활용 1 - 웹 애플리케이션 개발
excerpt: "✅ 인프런 김영한 JPA 로드맵 - JPA 활용 1편 정리본 기간: 24.08.15 ~ 24.08.17 참고 자료 페이지 페이지 Github - 코드 JAPprac1 Chapter 2. 도메인 분석 설계 3. 애플리케이션 구현 준비 4. 회원 도메인 개발 5. 상품 도메인 개발 6. 주문 도메인 개발 7. 웹 계층 개발 "
cover: null
icon: fc7650157bd0b62e.png
notionProperties: {}
schema_version: 1
parent_id: 1c3eda9b-0fe1-81ae-909e-cd1f71740107
created: 2025-03-27T07:47:30.936Z
updated: 2026-04-04T15:00:31.797Z
legacy_path: Main/Spring ( Java )-cd1f71740107/스프링 부트, JPA 활용 1 - 웹 애플리케이션 개발-f4632514eeb3/index.md
legacy_category: Spring ( Java )
source_url: https://beautiful-college-c84.notion.site/1c3eda9b0fe1815b82d2f4632514eeb3
---
> ✅ <strong>인프런 김영한 JPA 로드맵 &#45; </strong><strong><a href="https://www.inflearn.com/course/%EC%8A%A4%ED%94%84%EB%A7%81%EB%B6%80%ED%8A%B8-JPA-%ED%99%9C%EC%9A%A9-1/dashboard">JPA 활용 1편</a></strong><strong> 정리본 </strong>
> 
> > 기간&#58; 24&#46;08&#46;15 &#126; 24&#46;08&#46;17
> 
> <details>
> <summary>참고 자료</summary>
> 
> <a id="1c3eda9b0fe1819cb9d3dc158810340b"></a>
> 
> <a href="#/post/1c3eda9b-0fe1-8103-b16c-ff13884ad0ba">페이지</a> 
> 
> <a id="1c3eda9b0fe181d6acd6d812e5d3ec69"></a>
> 
> <a href="#/post/1c3eda9b-0fe1-8116-aed4-eb44b8e8c618">페이지</a> 
> 
> </details>

<a id="1c3eda9b0fe1810b90b2f2832d5e6dbf"></a>

### Github &#45; 코드

[JAP_prac1](https://github.com/gyungsubLee/JAP_prac1)

<a id="1c3eda9b0fe1816d8577d1a4ea227dc5"></a>

### Chapter 

[2. 도메인 분석 설계](#/post/1c3eda9b-0fe1-8187-9853-d8afc2f3c113)

[3. 애플리케이션 구현 준비](#/post/1c3eda9b-0fe1-8184-b8ac-cab5554557d6)

[4. 회원 도메인 개발](#/post/1c3eda9b-0fe1-8192-8b2e-c84c1548eb26)

[5. 상품 도메인 개발](#/post/1c3eda9b-0fe1-81c0-a908-d9311e55e372)

[6. 주문 도메인 개발](#/post/1c3eda9b-0fe1-816f-a67d-e3f70549e86b)

[7. 웹 계층 개발](#/post/1c3eda9b-0fe1-816f-868c-ccdba5dd21b6)

<details>
<summary>DI, 의존성 주입  정리</summary>

- 필드 주입

- 생성자 주입

- final 키워드 &#43; 롬복(&#64;RqAguConstructor)

</details>

<details>
<summary>🧐 강의랑 달리 테이블 생성 시, 각 테이블 마다 <code>&#95;seq</code>  테이블이 생성되었음</summary>

> 강의랑 다르게  DB를 MySQL 사용함 (강의에선 h2 사용)

<a id="1c3eda9b0fe181848509f221d36d0c21"></a>

각 테이블 마다 <code>&#95;seq</code>  테이블이 생성된 이유는 <strong><u>테이블 전략</u></strong>이 적용돼서 이다&#46;

<details>
<summary><strong>🧐 왜 TABLE 전략이 선택되었는가?</strong></summary>

- <strong>MySQL에서 시퀀스를 지원하지 않음</strong>
    - MySQL은 기본적으로 오라클이나 PostgreSQL처럼 자체 시퀀스를 지원하지 않기 때문에, Hibernate는 <strong><u>시퀀스 관리용 테이블을 만들어 사용</u></strong>한다&#46;

- <strong>Hibernate 기본 설정</strong>
    - Hibernate는 데이터베이스와의 호환성 문제를 피하기 위해 일부 데이터베이스에서 TABLE 전략을 기본으로 선택할 수 있다&#46;&#46; 이 설정이 AUTO 사용 시 &#95;seq 테이블이 생성되는 이유이다&#46;

</details>

<a id="1c3eda9b0fe1819991d3cd39bf30d25c"></a>

아래와 같이 모든 테이블의 id에 기본값인 <code>GenerationType&#46;AUTO</code>로 설계하였다&#46;

<a id="1c3eda9b0fe181beaa17d9ca1e4dafde"></a>

```java
@Id @GeneratedValue
private Long id;
```

<a id="1c3eda9b0fe181688664d1237e0b02cc"></a>

<code>GenerationType&#46;AUTO</code>는 JPA가 자동으로 최적의 전략을 선택하도록 하는 설정이다&#46;

<a id="1c3eda9b0fe1813d89c1e4c82314af60"></a>

데이터베이스의 종류와 JPA 구현체에 따라 아래와 같이 자동으로 적용된다&#46; 

<a id="1c3eda9b0fe181da9754c912f4c3c915"></a>

MySQL에서는 일반적으로 IDENTITY 전략을 사용하는 것이 일반적이지만, AUTO 설정의 경우 Hibernate가 TABLE 전략을 선택할 수 있으며, 이 때문에 &#95;seq 테이블이 생성될 수 있다&#46;

<a id="1c3eda9b0fe18137b4baed0236f7dc67"></a>

따라서 <code>GenerationType&#46;IDENTITY</code>(AUTO&#95;INCREMENT)로 명시하여 해당 문제를 해결<br>

</details>

<details>
<summary><strong>🧐 EntityManager를 주입 &#45; </strong><strong><code>&#64;PersistenceContext</code></strong><strong>, </strong><strong><code>&#64;Autowired</code></strong></summary>

<details>
<summary><strong><code>&#64;PersistenceContext</code></strong></summary>

<a id="1c3eda9b0fe1814fb432d605daad5a0c"></a>

```java
@PersistenceContext
private EntityManager em;
```

<a id="1c3eda9b0fe181a0863aedc02b49d7a3"></a>

&#64;PersistenceContext는 JPA에서 <strong>EntityManager</strong>를 주입할 때 사용하는 표준적인 방식입니다&#46; 이 어노테이션은 JPA 표준에 의해 제공되며, <strong>트랜잭션 스코프에서 관리되는 EntityManager</strong>를 주입합니다&#46;

- <strong>EntityManager 관리<br></strong>JPA는 트랜잭션 범위 내에서 EntityManager를 관리한다&#46; <br>따라서 트랜잭션이 시작될 때 EntityManager가 생성되고, 트랜잭션이 끝나면 자동으로 제거된다&#46; 

- <strong>Thread&#45;Safe하지 않음<br></strong>트랜잭션 범위 내에서만 사용되므로 스레드마다 각기 다른 EntityManager를 사용한다&#46;<br>이는 여러 스레드에서 동시에 같은 EntityManager를 사용할 수 없다는 것을 말한다&#46; <br>

</details>

<details>
<summary><strong><code>&#64;Autowired</code></strong></summary>

<a id="1c3eda9b0fe181109311d0344cae4469"></a>

```java
@Autowired
private EntityManager em;
```

<a id="1c3eda9b0fe181fbae16f0de6ecd2ddb"></a>

<strong><code>&#64;Autowired</code></strong><strong>는 </strong>스프링에서 의존성 주입을 할 때 사용하는 어노테이션 이다&#46; 

<a id="1c3eda9b0fe181d29595ecc0f5dc5be4"></a>

<strong>EntityManager</strong>도 스프링 컨테이너에 의해 관리될 수 있기 때문에 <code>&#64;Autowired</code>로 주입할 수 있다&#46;

<a id="1c3eda9b0fe181cea06fc25cca7ecaaa"></a>

그러나 스프링은 일반적으로 <strong><u>프록시 객체(스프링이 제공하는 가짜 객체)</u></strong>를 주입하여 트랜잭션 관리를 처리한다&#46;

- <strong>프록시 방식<br></strong>스프링은 실제 EntityManager 대신 <strong>프록시 객체</strong>를 주입한다&#46; <br>이 프록시 객체는 트랜잭션이 시작될 때 진짜 EntityManager를 연결한다&#46; 

- <strong>유연성<br></strong>스프링 컨테이너의 빈 관리 기능을 사용할 수 있기 때문에 다양한 설정이 가능하다&#46; <br>하지만 이 방식은 JPA 표준 방식이 아니다&#46; 

</details>

---

<details>
<summary><strong>정리</strong></summary>

- <strong>JPA 표준을 따르고 싶다면</strong> &#64;PersistenceContext를 사용, 일반적으로 JPA 표준 따른다&#46;

- <strong>스프링의 유연한 기능을 활용하고 싶다면</strong> &#64;Autowired도 사용, 이 경우 스프링에 의존하며 트랜잭션 관리와 같은 세부 동작이 다를 수 있으니 주의해야 한다&#46; <br>

| 항목 | <code>&#64;PersistenceContext</code> | <code>&#64;Autowired</code> |
| --- | --- | --- |
| <strong>표준</strong> | JPA 표준 방식 | 스프링의 의존성 주입 방식 |
| <strong>EntityManager 관리 방식</strong> | JPA에서 직접 관리하며 트랜잭션 범위에 맞춰 생성, 해제 | 스프링에서 프록시를 통해 관리 |
| <strong>트랜잭션 관리</strong> | 자동으로 트랜잭션 범위 내에서 관리 | 프록시 객체를 통해 트랜잭션 시작 시 관리 |
| <strong>호환성</strong> | JPA 표준에 맞춰 다양한 구현체에서 호환됨 | 스프링 환경에서만 주로 사용됨 |

</details>

</details>

<details>
<summary><strong>🧐 JPQL(Java Persistence Query Language)</strong></summary>

- JPQL(Java Persistence Query Language)은 JPA(Java Persistence API)에서 사용하는 쿼리 언어이다&#46;

- SQL과 비슷하지만, JPQL은 데이터베이스 테이블이 아닌 <strong>엔티티(Entity)</strong> 객체를 대상으로 쿼리를 작성한다&#46;

- 이를 통해 객체 지향 프로그래밍과 관계형 테이터 베이스를 연결하는 역할을 한다&#46; 

</details>
