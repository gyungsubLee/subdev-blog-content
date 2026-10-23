---
order: 0
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1c3eda9b-0fe1-8105-a3f8-d4212be1b8e6
title: SQL function 호출
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-81ae-909e-cd1f71740107
    title: Spring ( Java )
  - id: 1c3eda9b-0fe1-8156-b449-f8e742a95d76
    title: "[ Inflearn ] Querydsl"
  - id: 1c3eda9b-0fe1-8105-a3f8-d4212be1b8e6
    title: SQL function 호출
excerpt: SQL function 호출 --- 📖 SQL function은 JPA와 같이 Dialect(방언)에 등록된 내용만 호출할 수 있다. - 문자 - .stringTemplate()사용 - Expressions.stringTemplate(…) - 숫자 - .numberTemplate() 사용 - Expressions.num
cover: null
icon: null
notionProperties:
  중요도: Yes
  상태: 완료
schema_version: 1
parent_id: 1c3eda9b-0fe1-8156-b449-f8e742a95d76
created: 2025-03-27T07:53:11.116Z
updated: 2026-04-04T13:51:21.433Z
legacy_path: Main/Spring ( Java )-cd1f71740107/[ Inflearn ] Querydsl-f8e742a95d76/SQL function 호출-d4212be1b8e6/index.md
legacy_category: Spring ( Java )
source_url: https://beautiful-college-c84.notion.site/1c3eda9b0fe18105a3f8d4212be1b8e6
---
<a id="1c3eda9b0fe181d2bf29c8a9d631b02a"></a>

## SQL function 호출

---

> 📖 
> 
> <a id="1c3eda9b0fe181f2a03be68479ca4875"></a>
> 
> <code>SQL function</code>은 JPA와 같이 <u>Dialect(방언)에 등록된 내용</u>만 호출할 수 있다&#46;
> 
> - 문자 &#45;  <code>&#46;stringTemplate()</code>사용
>     - <code>Expressions&#46;stringTemplate(…)</code>
> 
> - 숫자 &#45;  <code>&#46;numberTemplate()</code> 사용
>     - <code>Expressions&#46;numberTemplate(…)</code>
> 
> - 함수 &#45; “function()

<details>
<summary>Case1)  &#91; <code>replace</code>&#93;  member → M으로 변경, Member</summary>

<a id="1c3eda9b0fe1817d9693e62cdb386cc8"></a>

```java
@Test
public void sqlFunction() {
    queryFactory
            .select(Expressions.stringTemplate(
                    "function('replate', {0}, {1}, {2}",
                    member.username, "member", "M"))
            .from(member)
            .fetchFirst();
}
```

</details>

<details>
<summary>Case2)  &#91; <code>lower</code>&#93;  소문자 변경</summary>

<a id="1c3eda9b0fe181f69192e29e645bd47a"></a>

```java
@Test
public void sqlFunction() {
    queryFactory
            .select(member.username)
            .from(member)
            .where(member.username.eq(Expressions.stringTemplate(
			            "function('lower', {0})"
			            ,member.username)))
            .fetchFirst();
}
```

- lower 같은 ansi 표준 함수들은 querydsl이 상당부분 내장하고 있다&#46;<br>따라서 아래와 같이 처리해도 결과는 같다&#46; 
    <a id="1c3eda9b0fe181988528ea05c2c78a2b"></a>

    ```java
    .where(member.username.eq(member.username.lower()))
    ```

</details>

<details>
<summary>함수 커스텀으로 정의 가능</summary>

- Direct 상속해서 처리

</details>
