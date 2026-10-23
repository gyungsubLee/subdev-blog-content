---
order: 0
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 346eda9b-0fe1-805b-bb2f-c81770700aff
title: "[인프런] 실전에서 바로 써먹는 Elasticsearch 입문 (검색 최적화편)"
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 346eda9b-0fe1-8009-8dce-dab63413d77f
    title: ElasticSearch
  - id: 346eda9b-0fe1-805b-bb2f-c81770700aff
    title: "[인프런] 실전에서 바로 써먹는 Elasticsearch 입문 (검색 최적화편)"
excerpt: "[인프런] 실전에서 바로 써먹는 Elasticsearch 입문 (검색 최적화편) - 기간: 26.04.18(토) ~ 26.04.26(일) - 강의: ‣ reference - ‣ - ‣ - 페이지 1. Elasticsearch 기본 개념 Elastic search 개념 및 활용 Elasticsearch 세팅 (docker)"
cover: f869c4d6f5c3dc59.webp
icon: 217f99d0d0700423.webp
notionProperties: {}
schema_version: 1
parent_id: 346eda9b-0fe1-8009-8dce-dab63413d77f
created: 2026-04-18T02:05:28.262Z
updated: 2026-05-03T07:13:57.012Z
legacy_path: Main/ElasticSearch-dab63413d77f/[인프런] 실전에서 바로 써먹는 Elasticsearch 입문 (검색 최적화편)-c81770700aff/index.md
legacy_category: ElasticSearch
source_url: https://beautiful-college-c84.notion.site/346eda9b0fe1805bbb2fc81770700aff
---
> 
> 
> <a id="346eda9b0fe1808c9899e7b22852055d"></a>
> 
> <strong>&#91;인프런&#93; 실전에서 바로 써먹는 Elasticsearch 입문 (검색 최적화편)</strong>
> 
> - 기간&#58; 26&#46;04&#46;18(토) &#126; 26&#46;04&#46;26(일)
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
> - <a href="https://beautiful-college-c84.notion.site/1ce11062ff07802ea28af468a6575af6">페이지</a> 
> 
> </details>

<a id="346eda9b0fe1808c9fd5f98d16bd90d1"></a>

### <strong> 1&#46; Elasticsearch 기본 개념</strong>

[Elastic search 개념 및 활용](#/post/346eda9b-0fe1-80bf-a1fd-eee30f99426f)

[Elasticsearch 세팅 (docker)](#/post/346eda9b-0fe1-80fc-8463-d148619e989e)

[Kibana - GUI 툴로 Elasticsearch 조작](#/post/348eda9b-0fe1-80d0-9d28-cd29acc66a9b)

[Elasticsearch의 기본 용어 - 인덱스, 도큐먼트, 매핑, 필드](#/post/348eda9b-0fe1-8079-9877-d81ea7d5293e)

[[기초 실습] 인덱스, 매핑, 도큐먼트](#/post/348eda9b-0fe1-80fd-b2a5-e21db9da5ac0)

<a id="346eda9b0fe180319df2defa8f387f49"></a>

###  2&#46; <strong>Spring Boot, Elasitcsearch를 활용한 CRUD 구현</strong>

[[Spring Data Elasticsearch] Spring Boot에 Elasitcsearch 연결](#/post/348eda9b-0fe1-809a-be4a-fdf99a870f28)

[[Spring Data Elasticsearch] CRUD API](#/post/348eda9b-0fe1-80c8-bd18-ffee53faee5b)

<a id="346eda9b0fe18091baa5d53643a5abff"></a>

###  3&#46; <strong>기본 검색 기능 및 작동 원리</strong>

[Elasticsearch 검색 기능 (feat. 쿠팡)](#/post/348eda9b-0fe1-807b-a504-cf07564fc7f6)

[[실습] Elasticsearch 검색 기능 테스트](#/post/348eda9b-0fe1-8037-9e09-fb33ab6ba8fd)

[역인덱스(Inverted Index)](#/post/348eda9b-0fe1-8005-9187-c9953c9e30e4)

[애널라이저 (Analyzer)](#/post/348eda9b-0fe1-80ef-a206-f13019ab8175)

[기본 애널라이저 (Standard Analyzer)](#/post/348eda9b-0fe1-8085-ad6e-eb586c89df9b)

[Standard Analyzer의 토큰 분할 과정 확인](#/post/348eda9b-0fe1-8040-ad20-f00f781d316f)

---

[소문자 변환(전처리) 애널라이저: [lowercase]](#/post/348eda9b-0fe1-80ff-849e-dd1ce05648e7)

[HTML 태그 제거(전처리) 애널라이저: [html_strip]](#/post/348eda9b-0fe1-8041-b5c0-f7ed0b84083b)

[불용어(a, an, or) 제거(전처리) 애널라이저: [stop]](#/post/348eda9b-0fe1-8034-a64b-cb0a08759bed)

[단어의 형태(-ed, -ing, -s 등) 제거(전처리) 애널라이저: [stemmer]](#/post/348eda9b-0fe1-80bd-9ddb-e30fa043f36d)

[동의어로 검색(전처리) 애널라이저: [synonym]](#/post/348eda9b-0fe1-8020-8ae1-ded6fa33d58d)

<a id="346eda9b0fe180f786b3e017377f4ef5"></a>

###  4&#46; <strong>한글에 최적화된 검색 기능</strong>

[[문제] 한글(korean) 전처리 시,  기존  애널라이저 오류](#/post/348eda9b-0fe1-80b3-8db2-dfd8c2065b41)

[Nori Analyzer를 활용한 한글 전처리 및 검색 실습](#/post/348eda9b-0fe1-80db-8fe1-de321f68e376)

[[한글 + 영어] 검색 기능](#/post/348eda9b-0fe1-8083-9f5d-f64735910c3d)

<a id="346eda9b0fe1806b8ecaee3e07ade688"></a>

###  5&#46; <strong>데이터의 저장 타입을 결정하는 매핑(Mapping)</strong>

[매핑(mapping), 데이터 타입(data type), 매핑 특징](#/post/348eda9b-0fe1-8018-9d59-d7b52793c63b)

[[실습] 인덱스 매핑 및 도큐먼트 생성](#/post/349eda9b-0fe1-800d-9f59-ca2f8acdd056)

<a id="346eda9b0fe180fda8b2fe527c7a94e9"></a>

###  6&#46; <strong>자주 사용하는 검색 기능</strong>

[검색 키워드가 포함된 데이터 조회: [match]](#/post/348eda9b-0fe1-80c2-b120-d3eff4e29738)

[특정 값(들)과 정확하게 일치하는 데이터 조회: [term, terms]](#/post/349eda9b-0fe1-8084-937d-d85a12b8dca1)

[2가지 이상의 조건을 만족하는 데이터 조회: [bool : filter, must]](#/post/349eda9b-0fe1-80de-9002-e92febb5250c)

[특정 조건을 만족하지 않는 데이터 조회: [bool : must_not]](#/post/349eda9b-0fe1-809c-a290-f8f0565b372e)

[숫자/날짜의 값에 대한 범위 조건으로 데이터 조회: [range]](#/post/349eda9b-0fe1-8080-b6e4-dd7f3128311d)

[특정 조건을 만족하는 데이터 위주로 상위 노출하려는 경우: [bool: should]](#/post/349eda9b-0fe1-80a2-a723-db9623f1d731)

[오타가 있더라도 유사한 단어를 포함한 데이터 조회: [fuzziness]](#/post/34aeda9b-0fe1-80e4-a464-f4ca14cd83a9)

[여러 필드(ex. 제목, 내용)에서 검색 키워드가 포함된 데이터 조회: [multi_match]](#/post/34aeda9b-0fe1-8070-9d67-c730eb9f5a51)

[검색한 키워드를 하이라이팅 처리: [highlight]](#/post/34aeda9b-0fe1-80f1-ba0e-f640ada9745d)

[페이지네이션 (Pagination), 정렬(Sorting)](#/post/34aeda9b-0fe1-8000-9c83-cc80724b9874)

[하나의 필드에 text와 keyword 타입을 동시에 사용: [Multi Field]](#/post/34aeda9b-0fe1-80b2-b492-c7de5628351d)

[검색 키워드를 일부 입력했을 때 검색어 추천: [자동 완성 기능]](#/post/34aeda9b-0fe1-806d-b532-f748064d1c19)

<a id="346eda9b0fe180adbde7f3905e6c8de1"></a>

###  7&#46; <strong>&#91;프로젝트&#93; Elasticsearch로 쿠팡의 상품 검색 기능 구현하기</strong>

[요구사항(상품 검색, 자동 완성), 프로젝트 기본 셋업](#/post/348eda9b-0fe1-804e-89b7-dfe822d585c2)

[[주의사항] 데이터 동기화 문제 및 아키텍처 설계](#/post/34deda9b-0fe1-80cb-bda7-e50bce5f6e44)

[[실습] 자동완성 및 검색 기능 구현](#/post/34deda9b-0fe1-80e3-9375-e8435c0204a8)

<a id="346eda9b0fe180ecb52cc31c3920babf"></a>

### <strong> 9&#46; Elastic Cloud를 활용한 Elasticsearch 구축</strong>

[Elastic Cloud를 활용한 구축](#/post/348eda9b-0fe1-8044-aaed-d734ae733cb6)
