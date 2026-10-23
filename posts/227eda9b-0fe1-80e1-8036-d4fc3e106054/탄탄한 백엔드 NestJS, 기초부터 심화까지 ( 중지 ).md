---
order: 0
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 227eda9b-0fe1-80e1-8036-d4fc3e106054
title: 탄탄한 백엔드 NestJS, 기초부터 심화까지 ( 중지 )
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 226eda9b-0fe1-802b-a035-c3a886768c4d
    title: Nest.js
  - id: 227eda9b-0fe1-80e1-8036-d4fc3e106054
    title: 탄탄한 백엔드 NestJS, 기초부터 심화까지 ( 중지 )
excerpt: "자료가 오래된 버전이며 설명이 명확하지 않아 다른 레퍼런스로 변경 ( 아래 자료 참조 ) - 페이지 /icons/tagred.svg [인프런] 비전공자도 이해할 수 있는 MySQL 성능 최적화 입문/실전 (SQL 튜닝편) - 기간: 25.07.07(일) ~ 25.07. - 강의: ‣ reference - ‣ - ‣ - ‣"
cover: 17cc569a69ac585c.webp
icon: e6e75ed58fae3588.svg
notionProperties: {}
schema_version: 1
parent_id: 226eda9b-0fe1-802b-a035-c3a886768c4d
created: 2025-07-05T15:33:34.111Z
updated: 2026-01-31T03:38:56.055Z
legacy_path: Main/Nest.js-c3a886768c4d/탄탄한 백엔드 NestJS, 기초부터 심화까지 ( 중지 )-d4fc3e106054/index.md
legacy_category: Nest.js
source_url: https://beautiful-college-c84.notion.site/227eda9b0fe180e18036d4fc3e106054
---
> 
> 
> <a id="271eda9b0fe180128175e41d75d44797"></a>
> 
> 자료가 오래된 버전이며 설명이 명확하지 않아 다른 레퍼런스로 변경 ( 아래 자료 참조 )
> 
> - <a href="#/post/260eda9b-0fe1-801b-836b-c2e229a88ff9">페이지</a> 

> /icons/tag_red.svg 
> 
> <a id="227eda9b0fe181f1a20af04d3ce291b1"></a>
> 
> &#91;인프런&#93; <strong>비전공자도 이해할 수 있는 MySQL 성능 최적화 입문/실전 (SQL 튜닝편)</strong>
> 
> - 기간&#58; 25&#46;07&#46;07(일) &#126; 25&#46;07&#46;
> 
> - 강의&#58; ‣
> 
> <details>
> <summary>reference</summary>
> 
> - ‣
> 
> - ‣
> 
> - ‣
> 
> - ‣
> 
> - ‣
> 
> </details>

> 
> 
> <a id="227eda9b0fe1801bb3ccef37df0d393d"></a>
> 
> <strong>목차</strong>
> 
> - [ 🧐 의문점](#22ceda9b0fe180bd8dbfecdd774efb67)
> - [1.  기본 설정 및 개념](#227eda9b0fe1810da34ccf920494c4c6)
> - [2.  Nest.JS를 위한 express 핵심 원리](#227eda9b0fe1809d8220ed82cd1f99ab)
> - [3.  MySQL, MongoDB 설계와 구축](#227eda9b0fe18073b70eccb0366467a5)
> - [4.  NestJS 개요 및 객체지향 디자인 패턴](#227eda9b0fe180379529ceb1e32fc758)
> - [5.  프로젝트1 : 고양이 정보 커뮤니티](#227eda9b0fe18018a11cdea7e4d3845d)
> - [6.  베포, 서버 운영](#227eda9b0fe1800a8447f98a90825854)
> - [7.  프로젝트2 : 랜덤 채팅 웹 앱 ( 풀스택,  소캣 프로그래밍 )](#227eda9b0fe1806fb64dd01039ce9113)
> - [9.  SQL, TypeORM in the Nest](#227eda9b0fe1805984e5c811b854a742)
> - [10.  MQTT](#227eda9b0fe18065b1c3cf748194e8d5)

<details>
<summary>Template</summary>

> 

> ✏️ 

> 📖 

> 
> 
> <a id="227eda9b0fe181f082dcceb63a9a12a8"></a>
> 
> <strong>목차</strong>
> 
> - [ 🧐 의문점](#22ceda9b0fe180bd8dbfecdd774efb67)
> - [1.  기본 설정 및 개념](#227eda9b0fe1810da34ccf920494c4c6)
> - [2.  Nest.JS를 위한 express 핵심 원리](#227eda9b0fe1809d8220ed82cd1f99ab)
> - [3.  MySQL, MongoDB 설계와 구축](#227eda9b0fe18073b70eccb0366467a5)
> - [4.  NestJS 개요 및 객체지향 디자인 패턴](#227eda9b0fe180379529ceb1e32fc758)
> - [5.  프로젝트1 : 고양이 정보 커뮤니티](#227eda9b0fe18018a11cdea7e4d3845d)
> - [6.  베포, 서버 운영](#227eda9b0fe1800a8447f98a90825854)
> - [7.  프로젝트2 : 랜덤 채팅 웹 앱 ( 풀스택,  소캣 프로그래밍 )](#227eda9b0fe1806fb64dd01039ce9113)
> - [9.  SQL, TypeORM in the Nest](#227eda9b0fe1805984e5c811b854a742)
> - [10.  MQTT](#227eda9b0fe18065b1c3cf748194e8d5)

<details>
<summary>&#91; 코드 &#93;</summary>

<a id="229eda9b0fe18030822aea6edce97e58"></a>

```typescript

```

</details>

[기본 설정](#/post/22deda9b-0fe1-80f5-83df-f7f0b041ea37)

[제목 없음](#/post/227eda9b-0fe1-8149-a640-f2001020dd68)

[[ 실습 ]](#/post/227eda9b-0fe1-81fe-9c8c-f0ab611cb81c)

[[ 의문점 ]](#/post/229eda9b-0fe1-8028-b1ad-d81cf3984ff6)

</details>

<a id="22ceda9b0fe180bd8dbfecdd774efb67"></a>

###  🧐 의문점

[[ 의문점 ] 자바스크립트 코드 실행 과정](#/post/228eda9b-0fe1-80b1-aa01-cd6659e84a8b)

[[ 의문점 ] undefined 타입 할당](#/post/229eda9b-0fe1-803a-90fb-e2e6696953a8)

[[ 의문점 ] pnpm 사용 이유](#/post/22aeda9b-0fe1-8035-b9ba-ed483053a3f6)

[[ 의문점 ] State sharing ( 동기화 문제 ) [ 보류 ]](#/post/22aeda9b-0fe1-806b-88b0-ce68b3e415bb)

[[ 의문점 ] Node.js, Netty(Spring WebFlux) 비교](#/post/22aeda9b-0fe1-80ef-8f53-faed71ec3bf9)

[[ 의문점 ] 왜 NestJS에서는 Token 사용하는가? [ 재정리 필요 ]](#/post/22beda9b-0fe1-802c-bbd0-f40fbd73d1dc)

[[ 의문점 ] 예외처리 - NestJS, Spring 비교](#/post/22ceda9b-0fe1-806e-8abf-c6e30fd8b0dc)

[[ 의문점 ] middleware,  Interceptor  비교](#/post/22deda9b-0fe1-802e-a807-cc51abda8319)

[[ 추가 ] RxJS  [ 정리 필요 ]](#/post/22deda9b-0fe1-8082-9166-d675799da110)

[[ 추가 ] Fastify  [ 정리 필요 ]](#/post/22feda9b-0fe1-801d-a1cb-c6485d2e9e35)

[[ 추가 ] AWS DynamoDB 설정 [ 정리 필요 ]](#/post/22feda9b-0fe1-8084-859f-f68b43b6ac11)

[[ 의문점 ] NestJS에서 process.env 대신 ConfigService.get()을 사용하는 이유](#/post/231eda9b-0fe1-8054-9d17-c339768a2cde)

<a id="227eda9b0fe1810da34ccf920494c4c6"></a>

### 1&#46;  기본 설정 및 개념

[웹 앱 아키턱처, HTTP 프로토콜](#/post/228eda9b-0fe1-80ac-988f-e4e348d8175e)

[RESTfull API](#/post/228eda9b-0fe1-80e4-8298-c138d62ee2a6)

<a id="227eda9b0fe1809d8220ed82cd1f99ab"></a>

### 2&#46;  Nest&#46;JS를 위한 express 핵심 원리

[express, TS 개발 환경 셋업, “hello world” 출력](#/post/228eda9b-0fe1-8034-be04-e2825b26e5fb)

[[ 실습 ] 데이터 모킹 테스트](#/post/228eda9b-0fe1-80bd-b152-de936956e696)

[express 미들웨어](#/post/228eda9b-0fe1-8029-98bc-df5bfea00ce9)

[[ 실습 ] 모듈 분리 및 CRUD API 구현](#/post/229eda9b-0fe1-8051-9a01-d23fc4175582)

[express 싱글톤 패턴, 서비스 패턴](#/post/229eda9b-0fe1-80d2-a652-da7405f6e62b)

<a id="227eda9b0fe18073b70eccb0366467a5"></a>

### 3&#46;  MySQL, MongoDB 설계와 구축

[Database 개요](#/post/229eda9b-0fe1-80f5-a931-ef08ae7a14ce)

[MongoDB 로컬 구축 및 CRUD CLI 실습 ( CLI 정리 중 )](#/post/229eda9b-0fe1-804c-8f92-e6cf898e723f)

[MongoDB 클라우드 구축](#/post/229eda9b-0fe1-8055-9084-d4caa4cd4466)

<a id="227eda9b0fe180379529ceb1e32fc758"></a>

### 4&#46;  NestJS 개요 및 객체지향 디자인 패턴

[NestJS 프로젝트 세팅 및 기본 구조 및 데코레이터 파악](#/post/22aeda9b-0fe1-8068-87b8-d9c3327f1247)

[ESLint, Prettier [ 정리 필요 ]](#/post/22aeda9b-0fe1-8009-88cf-faa9489d2d9c)

[Controller 패턴](#/post/22aeda9b-0fe1-8042-bed3-ff2206fa9ec5)

[Providers & 의존성 주입 ( DI )](#/post/22beda9b-0fe1-80d8-9502-f066e276de51)

[Module & 캡슐화 ( Nest CLI )](#/post/22beda9b-0fe1-80d5-8cfe-ed866b0be3a8)

[Nest 미들웨어 ( Middleware )](#/post/22beda9b-0fe1-8037-870d-e77c1a34631a)

[NestJs의 예외 처리 - Exception Filter](#/post/22beda9b-0fe1-80a9-aeaa-eb1f12cff2e4)

[Pipes - 유효성 검사, 파싱 [ 정리 중 ]](#/post/22ceda9b-0fe1-808d-aca9-f0c4915b0314)

[AOP 패턴 & Interceptors](#/post/22beda9b-0fe1-8090-8ddd-d81c73a5ba0b)

<a id="227eda9b0fe18018a11cdea7e4d3845d"></a>

### 5&#46;  프로젝트1 &#58; 고양이 정보 커뮤니티

[기본 세팅: Nest 프로젝트 및  MongoDB 설정](#/post/22deda9b-0fe1-80bc-9069-ef853ac5fbf0)

[환경변수 (config) 설정](#/post/22deda9b-0fe1-8083-960b-faeeff88659d)

[Validation ( 유효성 검사 )](#/post/22deda9b-0fe1-8094-ba57-ea4fa43986cf)

[MongDB - Model 스키마 정의 및 사용](#/post/22deda9b-0fe1-8059-bdd2-faa2a1313f78)

[데이터 암호화 - bcrypt](#/post/22eeda9b-0fe1-80e5-bf33-d8b1901445f0)

[API 문서 - Swagger UI](#/post/22feda9b-0fe1-8003-a6f3-f3b3c636adb9)

[CORS ( Cross-Origin Resource Sharing )](#/post/22feda9b-0fe1-805e-93b9-cf037c8ce79f)

[Repository 패턴](#/post/22feda9b-0fe1-802d-8e55-ead766da19b2)

[JWT를 통한 인증/인가](#/post/22feda9b-0fe1-8028-8cb5-c9861355f44b)

[순환 참조 모듈](#/post/231eda9b-0fe1-8024-bbcf-cd1e4d2fcbc4)

[[ 실습 ] 회원가입 API](#/post/22eeda9b-0fe1-800d-b0a1-fc642917f996)

[[ 실습 ] 인증 ( 로그인 API, Guard )](#/post/230eda9b-0fe1-8081-9f0b-fd00744b10ff)

<a id="227eda9b0fe1800a8447f98a90825854"></a>

### 6&#46;  베포, 서버 운영

<a id="227eda9b0fe1806fb64dd01039ce9113"></a>

### 7&#46;  프로젝트2 &#58; 랜덤 채팅 웹 앱 ( 풀스택,  소캣 프로그래밍 )

[CSR, SSR](#/post/231eda9b-0fe1-8057-a61c-f8b98d0d54a8)

[MVC 패턴](#/post/231eda9b-0fe1-80cc-b14b-f41a15ab2e2e)

[HTTP, Socket](#/post/231eda9b-0fe1-801c-b3f1-e5975b532355)

[WebSocket with NestJS](#/post/231eda9b-0fe1-804e-ad05-ff5449463e91)

[DB 세팅](#/post/231eda9b-0fe1-80f3-88b9-ed2943ebdd97)

[Gateways](#/post/24beda9b-0fe1-8077-86e2-fc150d2dd630)

<a id="227eda9b0fe1805984e5c811b854a742"></a>

### 9&#46;  SQL, TypeORM in the Nest

<details>
<summary>reference</summary>

[GitHub &#45; amamov/teaching&#45;typeorm&#45;in&#45;the&#45;nest]()

[Documentation &#124; NestJS &#45; A progressive Node&#46;js framework]()

[Entities &#124; TypeORM]()

</details>

[TypeORM](#/post/231eda9b-0fe1-804c-9de8-d632d6f144d4)

[PostgreSQL 셋업 ( with docker ) & TypeORM](#/post/231eda9b-0fe1-8002-89f7-fc3a30b1253e)

[보일러플레이트 코드 리뷰 및 테스팅 소개](#/post/231eda9b-0fe1-80c5-8f3c-f5ed977c714d)

[TDD 소개 및 통합 테스팅](#/post/231eda9b-0fe1-8075-9098-fc0b84351667)

[요구사항 및 도메인 설계, ERD 모델링](#/post/231eda9b-0fe1-8087-ab62-e34f73b852f5)

[엔티티 관계](#/post/231eda9b-0fe1-8047-a41e-dbc42b4be935)

<a id="227eda9b0fe18065b1c3cf748194e8d5"></a>

### 10&#46;  MQTT

[MQTT](#/post/237eda9b-0fe1-80e9-ae11-df69639446d6)

[보일러플레이트](#/post/237eda9b-0fe1-80a4-8605-eb55abf9738d)
