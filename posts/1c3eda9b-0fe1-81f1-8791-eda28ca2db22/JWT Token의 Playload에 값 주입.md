---
order: 3
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1c3eda9b-0fe1-81f1-8791-eda28ca2db22
title: JWT Token의 Playload에 값 주입
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-81ae-909e-cd1f71740107
    title: Spring ( Java )
  - id: 1c3eda9b-0fe1-812e-b8ac-c13c536efd00
    title: Spring Boot를 활용한 채팅 서비스 만들어보기
  - id: 1c3eda9b-0fe1-81f1-8791-eda28ca2db22
    title: JWT Token의 Playload에 값 주입
excerpt: JWT --- 📖 JWT - package com.auth0.jwt; JWTCreator java public static String createToken(String name) { return JWT.create() .withSubject(name) .withIssuedAt(new Date()) .withExpire
cover: null
icon: null
notionProperties:
  상태: 진행 중
schema_version: 1
parent_id: 1c3eda9b-0fe1-812e-b8ac-c13c536efd00
created: 2025-03-27T07:53:11.125Z
updated: 2025-03-27T07:53:11.125Z
legacy_path: Main/Spring ( Java )-cd1f71740107/Spring Boot를 활용한 채팅 서비스 만들어보기-c13c536efd00/JWT Token의 Playload에 값 주입-eda28ca2db22/index.md
legacy_category: Spring ( Java )
source_url: https://beautiful-college-c84.notion.site/1c3eda9b0fe181f18791eda28ca2db22
---
<a id="1c3eda9b0fe181838bb8d7bf58a71fb8"></a>

## JWT

---

> 📖 

<details>
<summary>JWT</summary>

- <em><code>package </code></em><code>com&#46;auth0&#46;jwt;</code>

</details>

<details>
<summary>JWTCreator</summary>

<a id="1c3eda9b0fe1813f8ac8d134f7aaa294"></a>

```java
public static String createToken(String name) {
    return JWT.create()
            .withSubject(name)
            .withIssuedAt(new Date())
            .withExpiresAt(new Date(System.currentTimeMillis() + tokenTimeForMinute * Constants.ON_MINUTE_TO_MILLITS))
            .sign(Algorithm.HMAC256(secretKey));
}
```

- withIssuedAt&#58; 생성 일자 설정

- withExpiresAt&#58; 만료 일자 설정

- sing(Algorithm&#46;<code>XXX</code>(secretkey));
    - 해당 알고리즘과 시크릿 키를 활용하여 JWT signature 생성 

    - <code>XXX</code>&#58; 사용하려는 암호화 알고리즘

<details>
<summary><code>withSubjcet()</code></summary>

- 데이터 값을 넣고 싶다

![](2b0993b5feb1c055.webp)

</details>

</details>

<details>
<summary>Base64</summary>

- <code>org&#46;apache&#46;commons&#46;codec&#46;binary&#46;Base64;</code>

</details>

<details>
<summary>HMAC256</summary>



</details>
