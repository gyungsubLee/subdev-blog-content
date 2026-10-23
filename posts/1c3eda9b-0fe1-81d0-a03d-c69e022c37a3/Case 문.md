---
order: 19
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1c3eda9b-0fe1-81d0-a03d-c69e022c37a3
title: Case 문
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-81ae-909e-cd1f71740107
    title: Spring ( Java )
  - id: 1c3eda9b-0fe1-8156-b449-f8e742a95d76
    title: "[ Inflearn ] Querydsl"
  - id: 1c3eda9b-0fe1-81d0-a03d-c69e022c37a3
    title: Case 문
excerpt: 'Case 문 --- 📖 select, 조건절(where), order by에서 사용 가능하다 - .when(조건).then(값): 분기 나눔 - .otherwise(”기타”): ELSE 단순한 조건 java List result = queryFactory .select(member.age .when(10).then("열'
cover: null
icon: null
notionProperties:
  ZOVW: Yes
  상태: 완료
schema_version: 1
parent_id: 1c3eda9b-0fe1-8156-b449-f8e742a95d76
created: 2025-03-27T07:53:11.118Z
updated: 2025-03-27T07:53:11.118Z
legacy_path: Main/Spring ( Java )-cd1f71740107/[ Inflearn ] Querydsl-f8e742a95d76/Case 문-c69e022c37a3/index.md
legacy_category: Spring ( Java )
source_url: https://beautiful-college-c84.notion.site/1c3eda9b0fe181d0a03dc69e022c37a3
---
<a id="1c3eda9b0fe1815480bbf2bf2661e2d9"></a>

## Case <strong>문</strong>

---

> 📖 
> 
> <a id="1c3eda9b0fe181419561c79bc775ae07"></a>
> 
> <code>select</code>, <code>조건절(where)</code>, <code>order by</code>에서 사용 가능하다
> 
> - <code>&#46;when(조건)&#46;then(값)</code>&#58; 분기 나눔
> 
> - <code>&#46;otherwise(”기타”)</code>&#58; ELSE

<details>
<summary>단순한 조건</summary>

<a id="1c3eda9b0fe181548b72c7858e21e3a8"></a>

```java
List<String> result = queryFactory
							.select(member.age
							        .when(10).then("열살")
							        .when(20).then("스무살") 
							        .otherwise("기타"))
							.from(member)
							.fetch();
```

</details>

<details>
<summary>복잡한 조건 &#45; <code>new CaseBuilder()</code></summary>

- when 내부 값이 아닌 범위 조건을 추가하는 경우, <code>new CaseBuilder()</code>를  사용해야 한다&#46;

<a id="1c3eda9b0fe181f1b696ed3a02f61325"></a>

```java
List<String> result = queryFactory
							.select(new CaseBuilder()
							        .when(member.age.between(0, 20)).then("0~20살")
							        .when(member.age.between(0, 20)).then("0~20살")
							        .otherwise("기타"))
							.from(member)
							.fetch();
```

</details>

<details>
<summary>orderBy에서 Case 문 함께 사용</summary>

- 아래와 같이 임의의 순서로 회원을 출력
    1. <code>0&#126;30 살</code>이 <u>아닌 회원</u>을 가장 먼저 출력

    1. <code>0&#126;20 살</code> <u>회원 출력</u>

    1. <code>21&#126;30 살</code> <u>회원 출력</u>

- case 문 정의
    <a id="1c3eda9b0fe181308fcaffd598be563b"></a>

    ```java
    NumberExpression<Integer> rankPath = new CaseBuilder()
           .when(member.age.between(0, 20)).then(2)
           .when(member.age.between(21, 30)).then(1)
           .otherwise(3);
    ```

    - <code>&#46;then()</code> &#58; 순번 정의

    - <code>new CaseBuilder()</code>의 반환 타입&#58; <code>NumberExpression</code>

- 쿼리 실행
    <a id="1c3eda9b0fe181d1ba23de7a258ba9d4"></a>

    ```java
    List<Tuple> result = queryFactory
             .select(member.username, member.age, rankPath)
             .from(member)
             .orderBy(rankPath.desc())
             .fetch();
    ```

- 출력값 확인
    <a id="1c3eda9b0fe1811d9be5e795547c4536"></a>

    ```java
     for (Tuple tuple : result) {
         String username = tuple.get(member.username);
         Integer age = tuple.get(member.age);
         Integer rank = tuple.get(rankPath);
         System.out.println("username = " + username + " age = " + age + " rank = " +rank); }
    ```

    <a id="1c3eda9b0fe181568d90f9966fb12b49"></a>

    ```java
    // 결과
    username = member4 age = 40 rank = 3
    username = member1 age = 10 rank = 2
    username = member2 age = 20 rank = 2
    username = member3 age = 30 rank = 1
    ```

</details>

> ✏️ 
> 
> <a id="1c3eda9b0fe1815180d6c225d8981ff4"></a>
> 
> Querydsl은 <u>자바 코드로 작성</u>하기 때문에 <code>rankPath</code> 처럼 <u>복잡한 조건을 변수로 선언</u>해서 <u><code>select</code></u><u> 절, </u><u><code>orderBy</code></u><u> 절에서 함께 사용</u>할 수 있다&#46;
