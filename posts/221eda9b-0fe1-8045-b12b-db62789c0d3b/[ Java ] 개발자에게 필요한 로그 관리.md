---
order: 2
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 221eda9b-0fe1-8045-b12b-db62789c0d3b
title: "[ Java ] 개발자에게 필요한 로그 관리"
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 21eeda9b-0fe1-80b0-b8c7-dae82cab7873
    title: 모니터링
  - id: 221eda9b-0fe1-8045-b12b-db62789c0d3b
    title: "[ Java ] 개발자에게 필요한 로그 관리"
excerpt: "/icons/push-pingreen.svg [인프런] 개발자에게 필요한 로그 관리 - 기간: 25.01.28(화) - 강의: ‣ - reference: - ‣ - ‣ 📌 - Section 1: 로그의 기초 이해 - Section 2: Logback 설정 - Section 3: 로그 수집 - Section 4: 로그 시"
cover: null
icon: null
notionProperties: {}
schema_version: 1
parent_id: 21eeda9b-0fe1-80b0-b8c7-dae82cab7873
created: 2025-06-29T01:18:10.035Z
updated: 2025-06-29T04:32:33.111Z
legacy_path: Main/모니터링-dae82cab7873/[ Java ] 개발자에게 필요한 로그 관리-db62789c0d3b/index.md
legacy_category: 모니터링
source_url: https://beautiful-college-c84.notion.site/221eda9b0fe18045b12bdb62789c0d3b
---
> /icons/push-pin_green.svg 
> 
> <a id="221eda9b0fe1812fb375c80b54085882"></a>
> 
> &#91;인프런&#93; <strong>개발자에게 필요한 로그 관리</strong>
> 
> - 기간&#58; 25&#46;01&#46;28(화)
> 
> - 강의&#58; ‣
> 
> - reference&#58;
>     -  ‣
> 
>     - ‣

> 📌 
> 
> - [Section 1: 로그의 기초 이해](#221eda9b0fe181d18acbeb41e631e8e2)
> - [Section 2: Logback 설정](#221eda9b0fe180d49eb2cacdad914059)
> - [Section 3: 로그 수집](#221eda9b0fe1808aa090e7cc4cf95a6c)
> - [Section 4: 로그 시각화, 활용](#221eda9b0fe1801cac66cb369f3074b6)
> - [Section 5: 부록](#221eda9b0fe180d9a51efedfaf8563f1)

<a id="221eda9b0fe181d18acbeb41e631e8e2"></a>

## Section 1&#58; 로그의 기초 이해

[왜 로그가 필요한가?](#/post/221eda9b-0fe1-8024-af36-d8624bc7f064)

[어떤 것을 로그로 남겨야 할까?](#/post/221eda9b-0fe1-814c-984d-c44594384b4d)

[예외, 로그](#/post/221eda9b-0fe1-802e-b5c6-c7c9ba2a0e0f)

[로그 레벨](#/post/221eda9b-0fe1-8034-98f2-ef52daa57d85)

[로그 고도화](#/post/221eda9b-0fe1-804b-957b-d857cb2ac2cd)

<a id="221eda9b0fe180d49eb2cacdad914059"></a>

## Section 2&#58; Logback 설정

[Logback 설정 파일 작성](#/post/221eda9b-0fe1-8112-bd15-c7beb93c3bb4)

[Logback Appender 활용](#/post/221eda9b-0fe1-8084-99c6-c0eb28e4562d)

[개발 환경별로 다른 Logback 설정하기](#/post/221eda9b-0fe1-8076-b803-f1cb0d976ab8)

<a id="221eda9b0fe1808aa090e7cc4cf95a6c"></a>

## Section 3&#58; 로그 수집

[로그 수집이 필요한 이유](#/post/221eda9b-0fe1-81ba-baf5-d2974cc1ae34)

[Elasticsearch, Logtash 준비하기](#/post/221eda9b-0fe1-80bd-89d4-e1ddc2191785)

[Elasticsearch 에 수집된 로그 확인](#/post/221eda9b-0fe1-8076-a0db-f770e8963bce)

<a id="221eda9b0fe1801cac66cb369f3074b6"></a>

## Section 4&#58; 로그 시각화, 활용

[Kibana로 로그 확인해보기](#/post/221eda9b-0fe1-81d2-a9ed-c93ae8d87970)

[대시보드로 로그 데이터 시각화하기](#/post/221eda9b-0fe1-80dd-9029-eb87dfcede5e)

[로그 레벨을 기준으로 알람 설정하기](#/post/221eda9b-0fe1-8065-a2cd-d0f22a9284e6)

<a id="221eda9b0fe180d9a51efedfaf8563f1"></a>

## Section 5&#58; 부록

[도커 애플리케이션 동작 오류](#/post/221eda9b-0fe1-813b-87a9-fc84f76b7a47)

[표준출력(println)과 로깅 프레임워크 성능 차이](#/post/221eda9b-0fe1-8045-8155-d885ac2ddc95)
