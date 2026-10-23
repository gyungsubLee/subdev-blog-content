---
order: 0
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 23aeda9b-0fe1-80d1-a91e-ff449013349f
title: DB 네이밍 규칙
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-8114-a6f8-e8c2debc9fa0
    title: DBMS
  - id: 23aeda9b-0fe1-80e8-a9d6-eef83f4e0193
    title: 비전공자도 이해할 수 있는 DB 설계 입문/실전
  - id: 23aeda9b-0fe1-80d1-a91e-ff449013349f
    title: DB 네이밍 규칙
excerpt: 목차 - [[ 규칙 1 ] 테이블명, 컬럼명 - 소문자 작성](23aeda9b0fe18179bbffd78312bc9833) - [[ 규칙 2 ] snakecase ](23beda9b0fe1801bb0efc1767f630d58) - [[ 규칙 3 ] 축약어 사용 ❌ ](23beda9b0fe180ba9052fb643f3966
cover: fb3b1ee7da4a15e0.webp
icon: 9bed2eae1e079b4b.avif
notionProperties: {}
schema_version: 1
parent_id: 23aeda9b-0fe1-80e8-a9d6-eef83f4e0193
created: 2025-07-24T09:42:35.384Z
updated: 2025-07-25T12:46:00.089Z
legacy_path: Main/DBMS-e8c2debc9fa0/비전공자도 이해할 수 있는 DB 설계 입문-실전-eef83f4e0193/DB 네이밍 규칙-ff449013349f/index.md
legacy_category: DBMS
source_url: https://beautiful-college-c84.notion.site/23aeda9b0fe180d1a91eff449013349f
---
> 
> 
> <a id="23aeda9b0fe1815594efe65951763919"></a>
> 
> <strong>목차</strong>
> 
> - [[ 규칙 1 ] 테이블명, 컬럼명 - 소문자 작성](#23aeda9b0fe18179bbffd78312bc9833)
> - [[ 규칙 2 ]  snake_case ](#23beda9b0fe1801bb0efc1767f630d58)
> - [[ 규칙 3 ]  축약어 사용 ❌ ](#23beda9b0fe180ba9052fb643f396654)
> - [[ 규칙 4 ]  SQL에서 예약어만 대문자로 표현](#23beda9b0fe180489c3fc2cc5db67ff6)
> - [[ 규칙 5 ] 테이블명을 지을 때, 복수형 사용 ( 선택 )](#23beda9b0fe1807087dad579784a6689)

<a id="23aeda9b0fe18179bbffd78312bc9833"></a>

## &#91; 규칙 1 &#93; 테이블명, 컬럼명 &#45; <code>소문자</code> 작성

---

> 📖 
> 
> <a id="23beda9b0fe180d9a9c3e1ab4d47002c"></a>
> 
>  테이블명, 컬럼명을<em> </em><em><strong><u>소문자 </u></strong></em><em><strong> </strong></em>로<strong>만</strong> 작성한다&#46;
> 
> - MySQL에서는 운영체제에 따라 대소문자를 구분해서 해석하기도 하고, 대소문자를 구분하지 않고 해석하기도 한다&#46; 따라서 <strong><u>운영 체제에 따라 잘못 작동되는 걸 방지</u></strong>하려면 <strong>대소문자를 섞어쓰지 않</strong>아야 한다&#46;

<a id="23beda9b0fe180e787b8e92bc5ebf353"></a>

```plaintext
first_name // ✅ (snake 케이스)

firstName // ❌ (camel 케이스)
```

<a id="23beda9b0fe1801bb0efc1767f630d58"></a>

## &#91; 규칙 2 &#93;  <code>snake&#95;case</code> 

---

> 📖 
> 
> <a id="23beda9b0fe1804c877ad172bb597484"></a>
> 
> <strong>테이블명, 컬럼명</strong>을 구성할 때 <em><strong><u>띄워쓰기 </u></strong></em>가 필요한 경우 <strong><code>snake&#95;case</code></strong>를 사용한다&#46;<strong> </strong>
> 
> - 대소문자 섞어 썼을 때의 단점이 명확하다&#46; 이를 피하기 위해<code> snake&#95;case</code>를 통해 구분한다&#46;

<a id="23beda9b0fe18040b74ac95822d2c733"></a>

```plaintext
first_name // ✅ (snake 케이스)

firstName // ❌ (camel 케이스)
```

<a id="23beda9b0fe180ba9052fb643f396654"></a>

## &#91; 규칙 3 &#93;  축약어 사용 ❌ 

---

> 📖 
> 
> <a id="23beda9b0fe180b19433d22c1e712342"></a>
> 
> 보통 실무에서 개발은 팀 단위로 이뤄진다&#46;  
> 
> <a id="23beda9b0fe18068bcceef8fa9e61dbe"></a>
> 
> 따라서 네이밍 규칙에서의 가장 중요한 포인트는 <code>가독성</code>이다&#46; 
> 
> <a id="23beda9b0fe180449b93d3a8bcf87ccc"></a>
> 
> 따라서 <strong><u>축약된 표현을 사용하지 않</u></strong>는다&#46; 

<a id="23beda9b0fe1809cb33debfb2a4aa655"></a>

```plaintext
first_name // ✅ (snake 케이스)

fst_nm // ❌ (camel 케이스)
```

<a id="23beda9b0fe180489c3fc2cc5db67ff6"></a>

## &#91; 규칙 4 &#93;  SQL에서 <strong><u>예약어만 대문자</u></strong>로 표현

---

> 📖 
> 
> <a id="23beda9b0fe18044896bfa9d2bdc6bb3"></a>
> 
> SQL 문법 자체는 대소문자를 따로 구분하지 않는다&#46; 
> 
> <a id="23beda9b0fe180ba9a18d36a9f9d3742"></a>
> 
> 그러나 SQL문의 <strong><u>가독성</u></strong>을 위해 <strong>예약어만 </strong><strong><u>대문자</u></strong><strong>로 작성</strong>한다&#46; 

<a id="23beda9b0fe18035a146cb8c349d6da7"></a>

```sql
SELECT name, age 
FROM users
WHERE age = 20
AND name = '재성';
```

<a id="23beda9b0fe1807087dad579784a6689"></a>

## &#91; 규칙 5 &#93; 테이블명을 지을 때, 복수형 사용 ( 선택 )

---

> 📖 
> 
> <a id="23beda9b0fe1803181e2f28b9b5dbde7"></a>
> 
> 복수형을 명시하는 것은 여러개의 데이터를 가지고 있음을 나타내기 위함이다&#46;
> 
> <a id="23beda9b0fe180548e3ffdc9a8b0e68a"></a>
> 
> 이 규칙은 회사마다 많이 다르다&#46; 즉, 테이블명을 지을 때 단수형을 사용하는 회사도 많다&#46; 
> 
> <a id="23beda9b0fe180e08107c50887efcfa3"></a>
> 
> 여기서 중요한 것은 <strong><u>일관성</u></strong>이다&#46; 따라서  해당 집단의 컨벤션을 따라 일관성 있게 작성하는 것이 무엇보다 중요하다&#46; 

<a id="23beda9b0fe18030947dd9196d18c48c"></a>

```plaintext
user
users

post 
posts
```
