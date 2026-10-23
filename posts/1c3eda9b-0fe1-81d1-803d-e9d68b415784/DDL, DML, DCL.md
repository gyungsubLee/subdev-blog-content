---
order: 13
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1c3eda9b-0fe1-81d1-803d-e9d68b415784
title: DDL, DML, DCL
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-81ae-909e-cd1f71740107
    title: Spring ( Java )
  - id: 1c3eda9b-0fe1-8103-b16c-ff13884ad0ba
    title: 자바 ORM 표준 JPA 프로그래밍 - 기본
  - id: 1c3eda9b-0fe1-81d1-803d-e9d68b415784
    title: DDL, DML, DCL
excerpt: "📌 Reference) https://brownbears.tistory.com/180 https://cbw1030.tistory.com/71 /icons/checkmark-linepink.svg 정리 DDL: 데이터베이스, 테이블 생성 및 변경, 제거 DML: 생성된 테이블 내 데이터(행, 열) 입력, 변경, 수정 DC"
cover: null
icon: ➕
notionProperties:
  상태: 완료
schema_version: 1
parent_id: 1c3eda9b-0fe1-8103-b16c-ff13884ad0ba
created: 2025-03-27T07:53:11.119Z
updated: 2025-03-27T07:53:11.119Z
legacy_path: Main/Spring ( Java )-cd1f71740107/자바 ORM 표준 JPA 프로그래밍 - 기본-ff13884ad0ba/DDL, DML, DCL-e9d68b415784/index.md
legacy_category: Spring ( Java )
source_url: https://beautiful-college-c84.notion.site/1c3eda9b0fe181d1803de9d68b415784
---
> 📌 Reference)<br><a href="https://brownbears.tistory.com/180">https&#58;//brownbears&#46;tistory&#46;com/180</a><br><a href="https://cbw1030.tistory.com/71">https&#58;//cbw1030&#46;tistory&#46;com/71</a>

> /icons/checkmark-line_pink.svg <strong>정리</strong><br><code>DDL</code>&#58; <strong>데이터베이스, 테이블</strong> <strong>생성 및 변경, 제거</strong><br><code>DML</code>&#58; 생성된 <strong>테이블 내 데이터(행, 열) </strong><strong>입력, 변경, 수정 </strong><br><code>DCL</code>&#58; <strong>데이터 베이스</strong>의 <strong>접속 권한</strong> 등 수정

> <strong><code>DDL</code></strong><strong>&#58; Data Definition Language, 데이터 정의어</strong>

<a id="1c3eda9b0fe1816283ddf25539eeae28"></a>

<strong><u>데이터베이스를 정의</u></strong><strong>하는 언어</strong>를 말하며 <strong><u>테이블 생성, 수정, 삭제, 초기화 </u></strong>등 데이터의 전체 골격(테이블)을 결정하는 역할 언어이다&#46;

| 명령어  | 설명 |
| --- | --- |
| <code>CREATE</code> | DB, Table 등을 생성 |
| <code>ALTER</code> | 테이블 수정 |
| <code>DROP</code> | DB, 테이블 삭제  |
| <code>TRUNCATE</code> | 테이블 초기화  (구조만 남기고 데이터 전부 삭제) |

> <strong><code>DML</code></strong><strong> &#58; Data Manipulation Language, 데이터 조작어</strong>

<a id="1c3eda9b0fe1818da1bed35e3058fe5d"></a>

정의된 데이터베이스, <strong>테이블 내 입력된 레코드</strong>를 <strong>조회, 수정, 삭제</strong> 등의 역할을 하는 언어

<a id="1c3eda9b0fe181d1b1a3efb4a8a875d3"></a>

쉽게 말해, <strong>테이블의 행, 열을 조작</strong>하는 언어이다&#46;

| 명령어  | 설명 |
| --- | --- |
| <code>SELECT</code> | 데이터 조회 |
| <code>INSERT</code> | 데이터 삽입 |
| <code>UPDATE</code> | 데이터 수행 |
| <code>DELETE</code> | 데이터 삭제 |

> <strong><code>DCL</code></strong><strong>&#58; Data Control Language, 데이터 제어어</strong>

<a id="1c3eda9b0fe181a6a170daeb5b735706"></a>

<strong>데이터베이스에 접근</strong>하거나 <strong>객체에 권한</strong>을 주는 등의 역할을 하는 언어

<a id="1c3eda9b0fe181aa80cbc9056c360ba3"></a>

데이터의 <strong>보안, 무결성, 데이터 회복, 병행 수행 제어 </strong>등을 정의하는데 사용한다&#46;

| 명령어  | 설명 |
| --- | --- |
| <code>GRANT</code> | <strong>권한 부여</strong>, 특정 데이터베이스 사용자에게 특정 작업에 대한 수행권한 부여 |
| <code>REVOKE</code> | <strong>권환 회수</strong><strong>, </strong>특정 데이터베이스 사용자에게 특정 작업에 대한 권한을 박탈, 회수한다&#46; |
| <code>COMMIT</code> | <strong>응답&#58; 성공</strong><strong>, </strong>트랜젝션의 작업이 정상적으로 완료되었음을 관리자에게 알려준다&#46;  |
| <code>ROLLBACK</code> | <strong>응답&#58; 실패, 복구</strong><strong>, </strong>트랜젝션 작업이 비정상적으로 종료 되었을때, 원래의 상태로 복구한다&#46; |
