---
order: 2
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 356eda9b-0fe1-8010-9561-c7098d310a4f
title: "The RED: 대용량 서비스를 위한 아키텍처 with Redis (by 강대명)"
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-817c-b119-d6a1706fbaf8
    title: 대규모 시스템 설계
  - id: 356eda9b-0fe1-8010-9561-c7098d310a4f
    title: "The RED: 대용량 서비스를 위한 아키텍처 with Redis (by 강대명)"
excerpt: "[패스트캠퍼스] The RED : 백엔드 에센셜 : 대용량 서비스를 위한 아키텍처 with Redis by 강대명 - 기간: 26.06.04(금) ~ 26.07.06(일) - 강의: ‣ reference - ‣ - ‣ - ‣ - ‣ CH1. 대규모 서비스 및 장애포인트를 찾기 위한 모니터링 대규모 서비스 특성 인프라 구성"
cover: e4e949d92d686b56.webp
icon: ea6af72f3b48eb03.webp
notionProperties: {}
schema_version: 1
parent_id: 1c3eda9b-0fe1-817c-b119-d6a1706fbaf8
created: 2026-05-04T11:44:34.067Z
updated: 2026-07-01T11:45:15.753Z
legacy_path: Main/대규모 시스템 설계-d6a1706fbaf8/The RED- 대용량 서비스를 위한 아키텍처 with Redis (by 강대명)-c7098d310a4f/index.md
legacy_category: 대규모 시스템 설계
source_url: https://beautiful-college-c84.notion.site/356eda9b0fe180109561c7098d310a4f
---
> 
> 
> <a id="356eda9b0fe1805bb8b2db9344b34884"></a>
> 
> <strong>&#91;패스트캠퍼스&#93; The RED &#58; 백엔드 에센셜 &#58; 대용량 서비스를 위한 아키텍처 with Redis by 강대명</strong>
> 
> - 기간&#58; 26&#46;06&#46;04(금) &#126; 26&#46;07&#46;06(일)
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
> </details>

<a id="35ceda9b0fe180c089d6eb6a6ebdd8b1"></a>

###  CH1&#46; 대규모 서비스 및 장애포인트를 찾기 위한 모니터링

[대규모 서비스 특성](#/post/362eda9b-0fe1-8042-8efe-c9ab42315a0f)

[인프라 구성 - IoC(Infra as Code)](#/post/362eda9b-0fe1-80a6-abdd-cd00afaf72d8)

[실습 예제](#/post/362eda9b-0fe1-801e-a1f8-c5840b079d64)

[지표 수집, 모니터링](#/post/362eda9b-0fe1-819c-8e8e-d5acf18d494a)

[성능 테스트](#/post/362eda9b-0fe1-80fe-a3d1-e55c1e48752b)

<a id="356eda9b0fe1805da89aff355b8d2974"></a>

###  CH2&#46; 대규모 서비스 설계를 위한 백엔드 에센셜

[로드밸런싱](#/post/356eda9b-0fe1-8100-ac12-cbb149eb553f)

[서비스 디스커버리](#/post/362eda9b-0fe1-80e9-8cef-f9424018b9d7)

[Circuit Breaker](#/post/35ceda9b-0fe1-8024-8e32-dc9c7b3becc5)

[Failover](#/post/362eda9b-0fe1-806d-a9f3-ef4aa63ecb51)

[Replication (데이터 복제)](#/post/367eda9b-0fe1-8014-b834-f04a86647e59)

[샤딩 (Sharding)](#/post/362eda9b-0fe1-8012-8645-f1e3ff04f9fc)

[Consistent Hashing](#/post/362eda9b-0fe1-80d7-9f89-eba4cf8d684a)

[GUID (Global Unique ID)](#/post/362eda9b-0fe1-8066-8af4-e4e8defd9edd)

[비동기 큐](#/post/362eda9b-0fe1-8008-9931-d735f37e121c)

[배포](#/post/362eda9b-0fe1-803e-b47b-dc19027b38f2)

<a id="35ceda9b0fe180339712cb2012a28474"></a>

###  CH3&#46; 대규모 트래픽 처리를 위한 Redis

[Redis 기본 자료구조](#/post/35ceda9b-0fe1-814d-8536-cba7b23d442f)

[Redis 사용 예: Cache](#/post/362eda9b-0fe1-805c-a5f6-e4a66439a2a6)

[Redis 모니터링 매트릭](#/post/362eda9b-0fe1-80cd-94b8-f6239a8280d4)

[Redis 장애 처리](#/post/362eda9b-0fe1-8066-a847-c9c293b2bfe5)

[대규모 트래픽 처리 시, 발생될 수 있는 이슈들](#/post/362eda9b-0fe1-8093-8638-db187f1a98f8)

[[실습] 간단한 서비스 추상화](#/post/362eda9b-0fe1-80a7-b7cc-dc4bac97ba2e)
