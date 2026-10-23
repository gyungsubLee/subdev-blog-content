---
order: 7
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1c3eda9b-0fe1-813f-b674-c1136625b5eb
title: 내가 작성한 SQL 문
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-81ae-909e-cd1f71740107
    title: Spring ( Java )
  - id: 1c3eda9b-0fe1-8125-825d-ea3785de29e5
    title: 스프링 입문 - 코드로 배우는 스프링 부트, 웹 MVC, DB 접근 기술
  - id: 1c3eda9b-0fe1-813f-b674-c1136625b5eb
    title: 내가 작성한 SQL 문
excerpt: FK 값 생성 시 추가로 제약조건을 주거나 제약조건 명칭을 한번에 추가하는 방법을 몰라 이전에 ALTER에서 정리한 SQL을 참조하여 작성함 sql CREATE TABLE if not exists MANAGER ( id bigint primary key comment 'PK', name varchar(100) not nu
cover: null
icon: null
notionProperties: {}
schema_version: 1
parent_id: 1c3eda9b-0fe1-8125-825d-ea3785de29e5
created: 2025-03-27T07:50:08.212Z
updated: 2025-03-27T07:50:08.212Z
legacy_path: Main/Spring ( Java )-cd1f71740107/스프링 입문 - 코드로 배우는 스프링 부트, 웹 MVC, DB 접근 기술-ea3785de29e5/내가 작성한 SQL 문-c1136625b5eb/index.md
legacy_category: Spring ( Java )
source_url: https://beautiful-college-c84.notion.site/1c3eda9b0fe1813fb674c1136625b5eb
---
<a id="1c3eda9b0fe181c695a7cb25b676e8e6"></a>

<strong>FK 값 생성</strong> 시 <strong>추가로 제약조건을 주</strong>거나 <strong>제약조건 명칭</strong><strong>을 </strong><strong>한번에 추가하는 방법을 몰</strong>라 이전에 <u>ALTER에서 정리한 SQL을 참조하여 작성</u>함

<a id="1c3eda9b0fe181499469c6b6b6fed582"></a>

```sql
CREATE TABLE if not exists MANAGER
(
    id bigint primary key comment 'PK',
    name varchar(100) not null comment '학생 이름',
    student_code varchar(1) not null comment "FK"
);

ALTER TABLE MANAGER ADD CONSTRAINT manager_fk_student_code FOREIGN KEY(student_code) REFERENCES STUDENT(student_code);
```

<a id="1c3eda9b0fe181dabb26ec64f93d85f2"></a>

아래와 같이 테이블 생성 확인 및 참조값(FK) 생성 확인함

![](18dd92c77d4a6a98.webp)
