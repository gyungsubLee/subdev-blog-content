---
order: 11
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 348eda9b-0fe1-8018-9d59-d7b52793c63b
title: 매핑(mapping), 데이터 타입(data type), 매핑 특징
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 346eda9b-0fe1-8009-8dce-dab63413d77f
    title: ElasticSearch
  - id: 346eda9b-0fe1-805b-bb2f-c81770700aff
    title: "[인프런] 실전에서 바로 써먹는 Elasticsearch 입문 (검색 최적화편)"
  - id: 348eda9b-0fe1-8018-9d59-d7b52793c63b
    title: 매핑(mapping), 데이터 타입(data type), 매핑 특징
excerpt: "목차 - 매핑(mapping) - 데이터 타입(data type) - 매핑(mapping)의 특징 - null 허용, Array 허용 매핑(mapping) --- 📖 매핑(mapping)이란 도큐먼트(document)의 각 필드가 어떤 데이터 타입을 가지고 있는 지 정의하는 설정을 의미한다. - MySQL에서 테이블을 "
cover: null
icon: null
notionProperties: {}
schema_version: 1
parent_id: 346eda9b-0fe1-805b-bb2f-c81770700aff
created: 2026-04-20T01:37:28.325Z
updated: 2026-04-22T04:54:57.266Z
legacy_path: Main/ElasticSearch-dab63413d77f/[인프런] 실전에서 바로 써먹는 Elasticsearch 입문 (검색 최적화편)-c81770700aff/매핑(mapping), 데이터 타입(data type), 매핑 특징-d7b52793c63b/index.md
legacy_category: ElasticSearch
source_url: https://beautiful-college-c84.notion.site/348eda9b0fe180189d59d7b52793c63b
---
> 
> 
> <a id="348eda9b0fe1804f9b4ecc566779bb0c"></a>
> 
> 목차
> 
> - [ 매핑(mapping)](#348eda9b0fe18055b363e0ce87d4c922)
> - [데이터 타입(data type)](#349eda9b0fe1806fbbe7e6cadb5b7739)
> - [매핑(mapping)의 특징 - null 허용, Array 허용](#349eda9b0fe18080bf46c57d481436e5)

<a id="348eda9b0fe18055b363e0ce87d4c922"></a>

##  매핑(mapping)

---

> 📖 
> 
> <a id="349eda9b0fe1808ba39bffcd712f2888"></a>
> 
> <code>매핑(mapping)</code>이란 <strong>도큐먼트(document)의 </strong><strong><u>각 필드</u></strong><strong>가 </strong><strong><u>어떤 데이터 타입</u></strong><strong>을 가지고 있</strong><strong>는 지 정의</strong>하는 설정을 의미한다&#46; 
> 
> - <strong>MySQ</strong>L에서 테이블을 만들 때 <strong>어떤 유형의 데이터를 넣</strong>을 지 <strong>스키마(schema)를 정의</strong>하는 것처럼
> 
> - <strong>Elasticsearch</strong>에서 <strong><u>인덱스를 만들 때 어떤 유형의 데이터를 넣</u></strong>을 지 <strong><u>매핑(mapping)</u></strong>을 통해 정의한다&#46;

<a id="349eda9b0fe1806fbbe7e6cadb5b7739"></a>

### 데이터 타입(data type)

> 🤔 
> 
> <a id="349eda9b0fe180409921c0842084e25c"></a>
> 
> Elasticsearch에서 데이터 타입의 종류는 아주 많다&#46; <br>그 중 <strong><u>자주 사용하는 데이터 타입</u></strong>에 대해서만 알아본다&#46;

<details>
<summary><strong>숫자</strong></summary>

- <code>integer</code>
    - <strong>10억 이하의 정수</strong>만 저장하면 되는 경우

- <code>long</code>
    - <strong>10억이 넘어가는 정수</strong>를 저장해야 될 수도 있는 경우

    - 실무에서 확장성을 위해 많이 사용

- <code>double</code>
    - <strong>실수(소숫점을 가진 숫자 포함)를 저장</strong>해야 될 수도 있는 경우

</details>

<details>
<summary><strong>문자</strong></summary>

- <code>text</code>
    - 문자열을 <strong>토큰으로 쪼개서 저장</strong>하고 싶은 경우

    - <strong><u>유연한 검색이 필요</u></strong>할 때 사용
        - 완전히 일치하지 않아도 비슷한 데이터를 조회해오는 방식

- <code>keyword</code>
    - 문자열을 토큰으로 쪼개지 않고, <strong>문자열 그대로 저장</strong>하고 싶은 경우

    - <strong><u>정확한 검색이 필요</u></strong>할 때 사용
        - 정확하게 일치할 때만 데이터를 조회해오는 방식

    - ex) 
        - 휴대폰 번호(<code>010&#45;1234&#45;5678</code>)

        - 이메일(<code>jscode&#64;gmail&#46;com</code>)

        - 주문번호(<code>156293920</code>)

        - …

> ⚠️ 
> 
> <a id="349eda9b0fe180a981a3cd1c105c757b"></a>
> 
> <strong>계산에서 쓰는 값이 아니라</strong>면 숫자가 아닌 <strong>문자로 저장</strong>해야 한다&#46; 
> 
> <a id="349eda9b0fe1800daf31cbe925a4e66e"></a>
> 
> 예를 들어, 휴대폰 번호나 주민등록번호에 숫자를 더하거나 빼지 않는다&#46; <br>즉, <strong><u>휴대폰 번호</u></strong>나 <strong><u>주민등록번호</u></strong>는 숫자가 아닌 <strong>문자로 저장</strong>해야 한다&#46; 

</details>

<details>
<summary><strong>기타</strong></summary>

- <code>date</code>
    - 날짜 데이터를 저장해야 하는 경우

- <code>boolean</code>
    - true, false를 저장해야 하는 경우

</details>

<a id="349eda9b0fe18080bf46c57d481436e5"></a>

### 매핑(mapping)의 특징 &#45; <code>null 허용</code>, <code>Array 허용</code>

<details>
<summary><strong>null 허용 (기본적으로 필수로 값을 넣을 필요가 없음)</strong></summary>

> ✏️ 
> 
> <a id="349eda9b0fe180ab8740ef94ae4763b4"></a>
> 
> Elasticsearch는 <strong>매핑을 정의</strong>하더라도 <strong><u>해당 필드가 반드시 존재</u></strong>하거나 <strong><u>null이면 안 된다</u></strong>는 <strong>제약을 두지 않</strong>는다&#46; 

<a id="349eda9b0fe1808f9d25f12e2cfa4ef8"></a>

<strong>인덱스 &#45; 매핑 설정</strong>

<a id="349eda9b0fe180908b4cc1d06990f51c"></a>

```json
"mappings": {
  "properties": {
    "title": { "type": "text" }
    "content": { "type": "text" }
  }
}
```

<a id="349eda9b0fe1805b9aa8fa610d5b9c96"></a>

<strong>데이터 삽입(도큐먼트 생성)</strong>

<a id="349eda9b0fe18007b556fc83ef46a34f"></a>

```json
{ 
  "title": null,
  "content": "산다는 것 그것은 치열한 전투이다."
}
```

<a id="349eda9b0fe180f6bef9e71adaaec225"></a>

```json
{ 
  "content": "산다는 것 그것은 치열한 전투이다."
}
```

- 위와 같이 <code>title</code>을 <strong><u>null</u></strong> 또는 <strong><u>정의하지 않</u></strong>아도 데이터가 정상 삽입된다&#46; 

</details>

<details>
<summary><strong>배열(array) 허용</strong></summary>

> ✏️ 
> 
> <a id="349eda9b0fe18003b521ff386ef5d027"></a>
> 
> Elasticsearch는 <strong>별도의 설정 없</strong>이 <strong><u>배열(array) 형태의 데이터를 삽입</u></strong>할 수 있다&#46; 그리고 <strong>배열(array)에 특화된 매핑 타입(mapping type)이 따로 없</strong>다&#46;

<a id="349eda9b0fe180be8313c4f5e45b2487"></a>

```json
"mappings": {
  "properties": {
    "hashtags": { "type": "text" }
  }
}
```

<a id="349eda9b0fe180f4a0c5ff1cabd2f9c4"></a>

```json
{ 
  "hashtags": "여행"
}
```

<a id="349eda9b0fe180378bcecca342f87bb3"></a>

```json
{ 
  "hashtags": ["여행", "요리"]
}
```

- <code>여행</code>이라는 키워드로 검색하면 위 2가지 데이터 전부 다 조회된다&#46; 

</details>
