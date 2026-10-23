---
order: 0
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 39feda9b-0fe1-80af-b2fb-e0517980dbb9
title: MSA 환경에서 REST API, gRPC, GraphQL로 마스터하는 백엔드 API 개발
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-817c-b119-d6a1706fbaf8
    title: 대규모 시스템 설계
  - id: 39feda9b-0fe1-80af-b2fb-e0517980dbb9
    title: MSA 환경에서 REST API, gRPC, GraphQL로 마스터하는 백엔드 API 개발
excerpt: "[패스트캠퍼스] MSA 환경에서 REST API, gRPC, GraphQL로 마스터하는 백엔드 API 개발 - 기간: 26.7.16(목) ~ 26.0.0() - 강의: ‣ reference - ‣ - ‣ Template ✏️ 📖 목차 - 1. REST API - 2. gRPC - 3. GraphQL - 4. API Ga"
cover: 2a203adfbbcee869.webp
icon: null
notionProperties: {}
schema_version: 1
parent_id: 1c3eda9b-0fe1-817c-b119-d6a1706fbaf8
created: 2026-07-16T03:13:36.162Z
updated: 2026-08-07T12:27:06.125Z
legacy_path: Main/대규모 시스템 설계-d6a1706fbaf8/MSA 환경에서 REST API, gRPC, GraphQL로 마스터하는 백엔드 A-e0517980dbb9/index.md
legacy_category: 대규모 시스템 설계
source_url: https://beautiful-college-c84.notion.site/39feda9b0fe180afb2fbe0517980dbb9
---
> 
> 
> <a id="a5eeda9b0fe182dfb4c8812ad359b599"></a>
> 
> <strong>&#91;패스트캠퍼스&#93;</strong> <strong>MSA 환경에서 REST API, gRPC, GraphQL로 마스터하는 백엔드 API 개발</strong>
> 
> - 기간&#58; 26&#46;7&#46;16(목) &#126; 26&#46;0&#46;0()
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
> </details>

<details>
<summary>Template</summary>

> 

> ✏️ 

> 📖 

> 
> 
> <a id="880eda9b0fe1820dbf0081b57a851d87"></a>
> 
> <strong>목차</strong>
> 
> - [ 1. REST API](#3b5eda9b0fe180e4a816e25aaa45a6ac)
> - [ 2. gRPC](#7b3eda9b0fe182a9802a01367f7816a0)
> - [ 3. GraphQL](#3b5eda9b0fe1805090d2dd4765e009fa)
> - [ 4. API Gateway](#3b5eda9b0fe180de93a7dcd5fa111736)
> - [ 5. Next Campus 프로젝트](#3b5eda9b0fe1803fb5bfee87f00dce17)
> - [ 6. [부록] 고성능 / 유연한 백엔드 서버를 위한 API 전략](#3b5eda9b0fe18007bdb4efd85ce85ec2)

<details>
<summary>&#91; 코드 &#93;</summary>

<a id="6eeeda9b0fe18209bc6381cdbfe0bd25"></a>

```typescript

```

</details>

[제목 없음](#/post/b4eeda9b-0fe1-8353-914e-0199ba8986ae)

[[ 실습 ]](#/post/77deda9b-0fe1-8379-838e-018886f5e3e3)

[[ 의문점 ]](#/post/a4ceda9b-0fe1-82bd-9fbf-81c37974bcca)

</details>

<a id="3b5eda9b0fe180e4a816e25aaa45a6ac"></a>

###  1&#46; REST API

[REST API 개요](#/post/3b5eda9b-0fe1-80c4-8be8-e348a1389393)

[HTTP 기본 개념](#/post/3b5eda9b-0fe1-807b-b99d-e04f22599cf2)

[REST API 디자인](#/post/3b5eda9b-0fe1-80be-961a-dac87b4f82c6)

[HTTP 메서드 활용](#/post/3b5eda9b-0fe1-8035-91e1-e32564f2db72)

[REST API 보완](#/post/3b5eda9b-0fe1-806e-aa00-c20008e944b7)

[REST API 문서화](#/post/3b5eda9b-0fe1-801c-b819-d752f8876d3c)

[REST API 고급 주제](#/post/3b5eda9b-0fe1-80f8-9f66-f487f5db4511)

[실습](#/post/3b5eda9b-0fe1-801c-9fa1-f336586e1af0)

<a id="7b3eda9b0fe182a9802a01367f7816a0"></a>

###  2&#46; gRPC

[gRPC 기본 개념](#/post/f4ceda9b-0fe1-82b9-ae18-812db14d32f9)

[Protocol Buffers(ProtoBuf)](#/post/3a1eda9b-0fe1-80ce-b184-cf2086179a2c)

[gRPC 개요](#/post/3a1eda9b-0fe1-80f5-8adb-f8bfda7b606f)

[[추가] RPC, Stub, 마샬링](#/post/3ddeda9b-0fe1-80fc-a5ce-e4fe1d852d54)

[gRPC 웹 및 REST 브리지](#/post/3b5eda9b-0fe1-80b5-90e8-d944cac3e70a)

[[추가] Armeria 사용 예제](#/post/3e1eda9b-0fe1-8038-9980-d12435b46db5)

[gRPC 스트리밍](#/post/3b5eda9b-0fe1-80db-a72c-ccfecd6cdfba)

[gRPC 에러 처리와 상태 코드](#/post/3b5eda9b-0fe1-8044-9f7c-df514a4505ed)

[gRPC 보안과 인증](#/post/3b5eda9b-0fe1-8034-93c1-d05a30f55177)

[[실습] gRPC 서버, 클라이언트 구현](#/post/3b5eda9b-0fe1-8076-9d58-cedc2ccb211e)

<a id="3b5eda9b0fe1805090d2dd4765e009fa"></a>

###  3&#46; GraphQL

[GraphQL 개요](#/post/3b5eda9b-0fe1-80c1-a1e5-e0384382b256)

[GraphQL 스키마, 타입](#/post/3b5eda9b-0fe1-80f0-8741-cb9e9dceb591)

[GraphQL 쿼리 언어](#/post/3b5eda9b-0fe1-8049-bb4a-ff111af5c122)

[GraphQL 쿼리, 뮤테이션](#/post/3b5eda9b-0fe1-8006-a960-c304a5179e09)

[GraphQL 보안, 인증](#/post/3b5eda9b-0fe1-807b-81c4-cfe9287de0ad)

[GraphQL 서버 개발 실습](#/post/3b5eda9b-0fe1-8067-be77-ee5b3a42a19a)

<a id="3b5eda9b0fe180de93a7dcd5fa111736"></a>

###  4&#46; API Gateway

[API Gateway](#/post/3b5eda9b-0fe1-80d0-bfe5-c99d1ae291f3)

[API 게이트웨이 프록시, 라우팅](#/post/3b5eda9b-0fe1-8073-a0a4-e057cf9a477f)

[인증(Authentication) 및 인가(Authorization)](#/post/3b5eda9b-0fe1-809d-ac2e-c8b6f0faeff0)

[트래픽 제어](#/post/3b5eda9b-0fe1-80d6-8c5d-d635ac382809)

[로깅 및 모니터링](#/post/3b5eda9b-0fe1-80b1-94d3-e2743a7ebfd0)

[BFF 패턴](#/post/3b5eda9b-0fe1-80ea-b0a5-d28e01faae39)

[마이크로서비스 아키텍처와의 연계](#/post/3b5eda9b-0fe1-8009-9cde-e3799f95b87b)

[실습 - API 게이트웨어 서버 개발](#/post/3b5eda9b-0fe1-8020-a6c1-d10cece18787)

<a id="3b5eda9b0fe1803fb5bfee87f00dce17"></a>

###  5&#46; Next Campus 프로젝트

[프로젝트 요구사항 분석 및 설계](#/post/3b5eda9b-0fe1-80c2-81a7-e9aedcfabf76)

[REST API 기반 마이크로서비스 구축](#/post/3b5eda9b-0fe1-8089-ba64-d3ce23f4db4c)

[gRPC 기반 마이크로서비스 구축](#/post/3b5eda9b-0fe1-80ba-95cf-ee255f84f664)

[GraphQL 스키마 설계 및 서비스 구축](#/post/3b5eda9b-0fe1-8039-9c5a-dee10485da80)

[API Gateway 설계 및 서비스 구축](#/post/3b5eda9b-0fe1-80e6-ac23-fcad43bbcd6d)

[로깅 및 모니터링 기능 추가](#/post/3b5eda9b-0fe1-800a-919c-fd45004bb498)

[Docker 이미지 빌드 및 Docker Compose로 베포](#/post/3b5eda9b-0fe1-80c6-8367-fb9eabd1af57)

[K8S Chart 로 어플리케이션 베포](#/post/3b5eda9b-0fe1-8079-8742-f807b8c43c60)

[API 문서화](#/post/3b5eda9b-0fe1-809c-b85d-fb6731832848)

[웹 클라이언트 구축](#/post/3b5eda9b-0fe1-80db-a971-fa9509aa1f1d)

[프로젝트 완성 및 리뷰](#/post/3b5eda9b-0fe1-8027-aa7b-f59ddc920b6d)

<a id="3b5eda9b0fe18007bdb4efd85ce85ec2"></a>

###  6&#46; &#91;부록&#93; 고성능 / 유연한 백엔드 서버를 위한 API 전략

[API 바로 알기](#/post/3b5eda9b-0fe1-802d-b895-e71813a309c9)

[API를 만드는 기술들](#/post/3b5eda9b-0fe1-8022-b922-d2b4971462d0)

[MSA 기반의 API 설계 개론](#/post/3b5eda9b-0fe1-8078-a5a4-fff5fe21500d)
