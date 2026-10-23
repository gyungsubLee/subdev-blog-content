---
order: 1
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 23aeda9b-0fe1-8012-a7bb-f67f2645d191
title: PK(기본키), FK(외래키)
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-8114-a6f8-e8c2debc9fa0
    title: DBMS
  - id: 23aeda9b-0fe1-80e8-a9d6-eef83f4e0193
    title: 비전공자도 이해할 수 있는 DB 설계 입문/실전
  - id: 23aeda9b-0fe1-8012-a7bb-f67f2645d191
    title: PK(기본키), FK(외래키)
excerpt: "목차 - PK(기본키) - FK(외래키) - 참조 무결성 PK(기본키) --- 📖 데이터베이스의 테이블에도 수많은 데이터가 저장되어 있다. 사람들을 구별하기 위해 주민등록번호가 필요하듯이, 수많은 데이터들을 구별하기 위해서 PK(Primary Key)라는 걸 사용한다. 즉, PK(Primary Key, 기본키)는 특정 "
cover: fb3b1ee7da4a15e0.webp
icon: 9bed2eae1e079b4b.avif
notionProperties: {}
schema_version: 1
parent_id: 23aeda9b-0fe1-80e8-a9d6-eef83f4e0193
created: 2025-07-24T09:36:39.408Z
updated: 2025-07-25T12:28:06.749Z
legacy_path: Main/DBMS-e8c2debc9fa0/비전공자도 이해할 수 있는 DB 설계 입문-실전-eef83f4e0193/PK(기본키), FK(외래키)-f67f2645d191/index.md
legacy_category: DBMS
source_url: https://beautiful-college-c84.notion.site/23aeda9b0fe18012a7bbf67f2645d191
---
> 
> 
> <a id="23aeda9b0fe181868cc0cf03d40a33de"></a>
> 
> <strong>목차</strong>
> 
> - [PK(기본키)](#23aeda9b0fe181a68ecce7fb469bc6d2)
> - [FK(외래키)](#23beda9b0fe180ef870bcae3dc4f00fb)
> - [참조 무결성](#23beda9b0fe180fba2c6ca510ab9893a)

<a id="23aeda9b0fe181a68ecce7fb469bc6d2"></a>

## PK(기본키)

---

> 📖 
> 
> <a id="23beda9b0fe180f2a0c9c23ff9019856"></a>
> 
> 데이터베이스의 테이블에도 수많은 데이터가 저장되어 있다&#46; 
> 
> <a id="23beda9b0fe18067b024d4d6e0184707"></a>
> 
> 사람들을 구별하기 위해 <strong><u>주민등록번호</u></strong>가 필요하듯이, <strong><u>수많은 데이터들을 구별</u></strong>하기 위해서 <strong><u>PK(Primary Key</u></strong><strong><u>)</u></strong>라는 걸 사용한다&#46; 
> 
> <a id="23beda9b0fe180b89c4ee24fccdfb86a"></a>
> 
> 즉, <strong><u>PK(Primary Key, 기본키)</u></strong>는 <strong><u>특정 데이터를 식별하기 위한 값</u></strong>이다&#46;
> 
> <a id="23beda9b0fe1802c859bcc3bcfa425c8"></a>
> 
> 또한 PK는 <strong><u>중복 되거나, 비어있으면 안</u></strong> 된다&#46; 

- 현업에서는 PK(Primary Key)를 주로 <strong><u>Auto Increment(숫자가 1씩 증가하는 방식</u></strong><u>)</u>나 <strong><u>UUID(랜덤값)</u></strong>로 설정을 많이 한다&#46; 

<a id="23beda9b0fe180ef870bcae3dc4f00fb"></a>

## FK(외래키)

---

> 📖 
> 
> <a id="23beda9b0fe180e68467f31ea2367dff"></a>
> 
> <strong><code>FK ( Foreign Key, 외래키 )</code></strong><strong>&#58; </strong><strong><u>다른 테이블의 데이터와 관계를 연결</u></strong><strong>하기 위한 </strong><strong><u>키</u></strong><strong> 이다&#46; </strong>

<a id="23beda9b0fe180fba2c6ca510ab9893a"></a>

### 참조 무결성

> <strong>&#91; FK 사용 전 &#93;</strong>

- <strong>users ( 사용자 )</strong>
    | <strong>id</strong> | <strong>이름</strong> |
    | --- | --- |
    | 1 | 박재성 |
    | 2 | 김유찬 |

    - posts ( 게시글 )
        | <strong>id</strong> | <strong>제목</strong> |
        | --- | --- |
        | 1 | 개발자 취업 방법 알려드려요&#33; |
        | 2 | 면접 후기 공유합니다 |
        | 3 | TIL &#45; 객체지향 |

> <strong>&#91; FK 사용 후 &#93;</strong>

- <strong>users ( 사용자 )</strong>
    | <strong>id</strong> | <strong>이름</strong> |
    | --- | --- |
    | 1 | 박재성 |
    | 2 | 김유찬 |

- posts ( 게시글 )
    | <strong>id</strong> | <strong>제목</strong> | <strong>user&#95;id ( FK )</strong> |
    | --- | --- | --- |
    | 1 | 개발자 취업 방법 알려드려요&#33; | 2 |
    | 2 | 면접 후기 공유합니다 | 1 |
    | 3 | TIL &#45; 객체지향 | <del><strong>20 ( Error )</strong></del> |

<a id="23beda9b0fe1809ab08ce5deef0bb7fb"></a>

FK ( 외래키 )를 설정했을 때, <strong>적절하지 않은 FK가 할당</strong>되는 <strong>DB</strong><strong>에서 </strong><strong>에러를 발생</strong>시킨다&#46; 

<a id="23beda9b0fe180f3b9c5dd674a497f14"></a>

즉, 이를 통해 <strong><u>FK 값으로 적절하지 않는 값이 할당되는 것을 방지</u></strong>해준다&#46; 

<a id="23beda9b0fe18057a995de40fc83eaf4"></a>

이를 <strong><u>참조 무결성</u></strong> 이라고 한다&#46; 

<a id="23beda9b0fe1806da515cfdb28f54f68"></a>

말 그대로 <strong><u>결점(모순되는 점)이 없도록 유지</u></strong>하는 특성을 의미한다&#46; 

> ✏️ 
> 
> <a id="23beda9b0fe18086b0dec96e2b8dc675"></a>
> 
> 데이터베이스에서 <code>무결성</code>이라는 단어가 많이 사용된다&#46;
> 
> - ex) 참조 무결성, 도메인 무결성, 엔티티 무결성 등 …
> 
> <a id="23beda9b0fe180e2a896f62a911316d2"></a>
> 
> 하지만 각 무결성이 무엇인지 외울 필요가 없다&#46; 실제 DB 설계 시 크게 중요하지 않다&#46; 
> 
> <a id="23beda9b0fe180b59876c7f5bb708bc6"></a>
> 
> 그러나 많이 사용되는 단어이니, 따로 나만의 언어로 정리할 필요가 있다&#46;
