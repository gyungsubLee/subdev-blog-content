---
order: 0
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1c3eda9b-0fe1-81c7-ae23-cfbc9fd6e83a
title: 비전공자도 이해할 수 있는 Redis - 캐싱 [ 리펙토링 필요 ]
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-81b8-a968-f6b1b2a79b94
    title: Redis
  - id: 1c3eda9b-0fe1-81c7-ae23-cfbc9fd6e83a
    title: 비전공자도 이해할 수 있는 Redis - 캐싱 [ 리펙토링 필요 ]
excerpt: 📌 [ Inflearn ] Redis 정리본 reference ‣ 페이지 ‣ Redis 개념, 장점, 사례 RedisTemplate, Jedis, Lettuce 비교 로컬 - Redis 설치 Redis 기본 명령어 Redis - Key 네이밍 컨벤션 캐시 ( Cache ), 캐싱 ( Cachig ) 데이터 캐싱 전략 (
cover: null
icon: 01de34a4c7d2d333.webp
notionProperties: {}
schema_version: 1
parent_id: 1c3eda9b-0fe1-81b8-a968-f6b1b2a79b94
created: 2025-03-27T07:47:12.303Z
updated: 2025-07-05T05:01:07.604Z
legacy_path: Main/Redis-f6b1b2a79b94/비전공자도 이해할 수 있는 Redis - 캐싱 [ 리펙토링 필요 ]-cfbc9fd6e83a/index.md
legacy_category: Redis
source_url: https://beautiful-college-c84.notion.site/1c3eda9b0fe181c7ae23cfbc9fd6e83a
---
> 📌 
> 
> <a id="1c3eda9b0fe181abae01f1fd6ca47d0b"></a>
> 
> <strong>&#91; Inflearn &#93; Redis  정리본</strong> 
> 
> <details>
> <summary>reference</summary>
> 
> <a id="1c3eda9b0fe181f3adbad74c58380931"></a>
> 
> ‣
> 
> <a id="1c3eda9b0fe181e6a678f2c96441b921"></a>
> 
> <a href="https://beautiful-college-c84.notion.site/37614062983943e69e6b06d1f3abe447">페이지</a> 
> 
> <a id="1c3eda9b0fe1817a8e97ebda3333f2bb"></a>
> 
> ‣
> 
> </details>

[Redis 개념, 장점, 사례](#/post/1c3eda9b-0fe1-81c7-a804-da38fe09f8b6)

[RedisTemplate, Jedis, Lettuce 비교](#/post/1c3eda9b-0fe1-813f-842e-d3c86d43d555)

[로컬 - Redis 설치](#/post/1c3eda9b-0fe1-81aa-80fe-cb6ae2b3678c)

[Redis 기본 명령어](#/post/1c3eda9b-0fe1-81c0-b73c-d3ac23405d3b)

[Redis - Key 네이밍 컨벤션](#/post/1c3eda9b-0fe1-81de-965a-f1a444bed954)

[캐시 ( Cache ), 캐싱 ( Cachig )](#/post/1c3eda9b-0fe1-8167-a9c7-f03c520be861)

[데이터 캐싱 전략 ( Cache Aside, Write Around )](#/post/1c3eda9b-0fe1-81dc-bd0c-ceeb86a8a464)

[캐싱을 통한 조회 성능 개선 전, 먼저 해야하는 것 - SQL 튜닝](#/post/1c3eda9b-0fe1-8118-adae-e182665bf45e)

[[ 실습 1 ] Spring Boot, MySQL, Redis 기본 세팅](#/post/1c3eda9b-0fe1-8114-93a4-f765392b7ed5)

[[ 실습 1 ] Redis 셋팅 추가](#/post/1c3eda9b-0fe1-819b-8572-fb1595d6c6ad)

[[ 실습 1 ] Redis 적용 전후, 성능 비교 ( postman )](#/post/1c3eda9b-0fe1-81ec-9c29-c627d7933597)

[[ 실습 2 ] Nest.js + Redis](#/post/1c3eda9b-0fe1-8160-9a72-d19689ccf55e)

[AWS 비용](#/post/1c3eda9b-0fe1-815c-8952-f56392663644)

[[ 실습 3 ] AWS EC2 - Spring Boot, Redis, MySQL](#/post/1c3eda9b-0fe1-8134-a52d-eb1b5ff964c1)

[[ 실습 3 ] Redis 부하테스트](#/post/1c3eda9b-0fe1-815a-983c-eb61ae942d38)

[[ 실습 4 ] Docker Compose로 Spring Boot + Redis 실행](#/post/1c3eda9b-0fe1-81a1-83fe-c13f2e23db04)

[AWS  - ElasticCache](#/post/1c3eda9b-0fe1-8113-b73d-f5ca2498015d)

[[ 실습 5 ] Spring Boot에 ElasticCache 연결](#/post/1c3eda9b-0fe1-8194-a3af-fd7d7dbf4f59)

[[ 오류 ] IAM 계정 - EC2 AccessDenied](#/post/1c3eda9b-0fe1-8124-8c5f-ea70a98981bf)
