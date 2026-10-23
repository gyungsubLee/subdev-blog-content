---
order: 16
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 14beda9b-0fe1-8133-8296-ee5acd84c334
title: JPQL
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 108eda9b-0fe1-80a6-8a2b-c21df3ab9492
    title: 내일 배움 캠프 ( 백엔드 코스 7기)
  - id: 149eda9b-0fe1-8010-9b0f-dc35331888ed
    title: "[sparta] 스프링 심화"
  - id: 14beda9b-0fe1-8133-8296-ee5acd84c334
    title: JPQL
excerpt: JPQL --- 📖 데이터베이스에 질의(Query)를 실행하기 위해 사용하는 객체지향 쿼리 언어 SQL과 유사하지만 DB의 테이블이 아닌 Entity 객체와 필드를 대상으로 작성됨 JPA의 SQL Query 지원 1. JPQL(Java Persistence Query Language) - 객체지향 쿼리 언어 - Enti
cover: null
icon: null
notionProperties:
  subchapter: |-
    • JPQL
    • 동적 쿼리
  상태: 완료
schema_version: 1
parent_id: 149eda9b-0fe1-8010-9b0f-dc35331888ed
created: 2024-11-27T00:37:43.496Z
updated: 2025-05-15T02:46:54.782Z
legacy_path: Main/내일 배움 캠프 ( 백엔드 코스 7기)-c21df3ab9492/[sparta] 스프링 심화-dc35331888ed/JPQL-ee5acd84c334/index.md
legacy_category: 내일 배움 캠프 ( 백엔드 코스 7기)
source_url: https://beautiful-college-c84.notion.site/14beda9b0fe181338296ee5acd84c334
---
<a id="14ceda9b0fe18188b69bff46673992da"></a>

## JPQL

---

> 📖 
> 
> <a id="14ceda9b0fe18186b97cf2038aa1044a"></a>
> 
> <u>데이터베이스에 질의(Query)를 실행</u>하기 위해 사용하는 객체지향 쿼리 언어
> 
> <a id="14ceda9b0fe180dbb624cc5ac8f553f7"></a>
> 
> <u>SQL과 유사</u>하지만 DB의 테이블이 아닌 Entity 객체와 필드를 대상으로 작성됨

<details>
<summary><strong>JPA의 SQL Query 지원</strong></summary>

1. <strong>JPQL(Java Persistence Query Language)</strong>
    - 객체지향 쿼리 언어

    - Entity 객체를 대상으로 SQL Query를 작성할 수 있게 한다&#46;

1. <strong>QueryDSL</strong>
    - Java 기반의 ORM 쿼리 빌더 라이브러리

    - 동적 쿼리를 지원

</details>

<details>
<summary><strong>JPQL의 등장</strong></summary>



</details>

<details>
<summary><strong>JPQL 특징</strong></summary>

- 객체를 대상으로 검색하는 객체 지향 쿼리 ( 테이블 X )

- SQL 추상화  ( DB 종속 X )
    - 다양한 데이터베이스에서 사용 가능

    - JPA 영속성 컨텍스트를 사용하여 1차 캐시, 지연로딩 등의 기능 활용 가능

- 타입 안정성
    - compile 시점에 Entity와 필드의 타입을 확인 &#45; &#62; 오류 ↓

</details>

<details>
<summary><strong>JPQL vs SQL</strong></summary>

|  |  |  |
| --- | --- | --- |
| <strong>특징</strong> | <strong>JPQL</strong> | <strong>SQL</strong> |
| 대상 | Entity와 필드 | 테이블과 컬럼 |
| 표현 방식 | 객체지향 | 관계형 |
| DB 독립성 | 높음 | 특정 DB 종속 |
| 호출 방식 | EntityManager&#46;createQuery() | 직접 DB와 연결 |

</details>

<a id="14ceda9b0fe180899218c708f29f0cfb"></a>

## 동적 쿼리

---

> 📖 
> 
> <a id="2be69b21ecf74926a676ae717429c40a"></a>
> 
> 실행 시점에 <u>특정 조건이나 값</u>에 따라  <u>변화하는 SQL Query를 작성 및 실행</u>하는 방식

> ✏️ 
> 
> <a id="14ceda9b0fe1804582d3eb1aba8c030c"></a>
> 
> JPQL은 SQL 문법과 유사한 <code>SELECT</code>, <code>WHERE</code>, <code>GROUP BY</code>, <code>HAVING</code>, <code>JOIN</code> 등을 지원한다&#46;

<details>
<summary>예시 </summary>

- 특정 조건에 따라서 실행되는 SQL이 변한다&#46;

<a id="14ceda9b0fe18073b3bbcb997a278c77"></a>

```java
String jpql = "SELECT p FROM Product p WHERE 1=1";

if (name != null) {
    jpql += " AND p.name = :name";
}
if (price != null) {
    jpql += " AND p.price = :price";
}
```

</details>

> 🤬 
> 
> <a id="968fa8ec809a4d53aa91616ea3497ffb"></a>
> 
>  JPQL 동적 쿼리
> 
> > JPQL은 <u>정적 쿼리에 최적화</u> 되어있다&#46; 
> 
> <a id="14ceda9b0fe180f49f3ff3ca1ca55e5f"></a>
> 
> JPQL은 <u>문자열 SQL을 직접 다루</u>어야 하기 때문에 <u>문자열을 동적으로 조합</u>해야 한다&#46;
> 
> <a id="14ceda9b0fe1801f9c93d28d32ac2beb"></a>
> 
> 따라서 <u>가독성과 유지보수가 어렵</u>고, <u>오타나 문법 오류가 발생하기 쉽</u>다&#46; 
> 
> <a id="14ceda9b0fe18075931bd83db4c981e4"></a>
> 
>  →  <u>컴파일 오류에서 잡지 못</u><u>한</u>다&#46;  
> 
> <a id="14ceda9b0fe180228c74faa4a0a68fd3"></a>
> 
> <br>조건이 많아지면 많아질수록 <u>JPQL을 사용한 동적쿼리 처리는 한계가 명확</u>하다&#46;
