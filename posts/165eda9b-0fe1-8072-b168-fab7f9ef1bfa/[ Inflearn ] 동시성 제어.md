---
order: 0
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 165eda9b-0fe1-8072-b168-fab7f9ef1bfa
title: "[ Inflearn ] 동시성 제어"
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 108eda9b-0fe1-80a6-8a2b-c21df3ab9492
    title: 내일 배움 캠프 ( 백엔드 코스 7기)
  - id: 165eda9b-0fe1-8072-b168-fab7f9ef1bfa
    title: "[ Inflearn ] 동시성 제어"
excerpt: 📌 - 강의 - 재고시스템으로 알아보는 동시성 이슈 해결 방법 - 기간 - 24.12.23(월), 25.1.5 - 소스코드 - ‣ reference ‣ - redisson ‣ ‣ - 소스 코드 stockSystem Chapter 재고 감소 로직 문제점 - 멀티쓰레드 환경에서의 레이스 컨디션 Synchronized., 문
cover: null
icon: ✅
notionProperties: {}
schema_version: 1
parent_id: 108eda9b-0fe1-80a6-8a2b-c21df3ab9492
created: 2024-12-23T10:48:55.077Z
updated: 2026-04-10T05:13:25.097Z
legacy_path: Main/내일 배움 캠프 ( 백엔드 코스 7기)-c21df3ab9492/[ Inflearn ] 동시성 제어-fab7f9ef1bfa/index.md
legacy_category: 내일 배움 캠프 ( 백엔드 코스 7기)
source_url: https://beautiful-college-c84.notion.site/165eda9b0fe18072b168fab7f9ef1bfa
---
> 📌 
> 
> - <code>강의</code> &#45;  <a href="https://www.inflearn.com/course/%EB%8F%99%EC%8B%9C%EC%84%B1%EC%9D%B4%EC%8A%88-%EC%9E%AC%EA%B3%A0%EC%8B%9C%EC%8A%A4%ED%85%9C/dashboard">재고시스템으로 알아보는 동시성 이슈 해결 방법</a>
> 
> - <code>기간</code> &#45;  <code>24&#46;12&#46;23(월)</code>,  <code>25&#46;1&#46;5</code>
> 
> - <code>소스코드</code> &#45; ‣
> 
> <details>
> <summary>reference</summary>
> 
> <a id="173eda9b0fe180b1bda1f102500cffd6"></a>
> 
> ‣
> 
> - redisson
>     <a id="173eda9b0fe180228afce4e1571554c7"></a>
> 
>     ‣
> 
>     <a id="173eda9b0fe180b995e6d1b449958d74"></a>
> 
>     ‣
> 
> </details>

- 소스 코드 

[stockSystem](https://github.com/gyungsubLee/stockSystem)

<a id="165eda9b0fe180b58265f4e58868cb91"></a>

## Chapter

[재고 감소 로직](#/post/bd3eda9b-0fe1-83df-9d30-81ab20e73a36)

[문제점 - 멀티쓰레드 환경에서의  레이스 컨디션](#/post/268eda9b-0fe1-8301-9f46-01741a409ec9)

[Synchronized., 문제점 (분산 환경에서의 레이스 컨디션 )](#/post/c83eda9b-0fe1-8314-87ec-8141a6e7d7f0)

[비관적 락 ( Pessimistic Lock )](#/post/6b7eda9b-0fe1-8227-a295-01160dba23be)

[낙관적 락 ( Optimistic Lock )](#/post/fb7eda9b-0fe1-83f7-8ded-019d3d0c039a)

[명명된 락 ( Named Lock )](#/post/023eda9b-0fe1-8260-b061-016091f6ee28)

[Lettuce, Redisson 개념 설명 및 기본 설정](#/post/8c5eda9b-0fe1-8210-9688-810fd390d68f)

[Lettuce를 사용한 재고감소 로직 작성](#/post/edceda9b-0fe1-834a-b9f7-01b5681d1869)

[Redisson을 활용한 재고 로직 작성](#/post/f18eda9b-0fe1-828b-bc80-01b8b7ab0598)

[Lettuce, Redisson 장단점](#/post/b6deda9b-0fe1-8381-a489-81913e88d299)

[Mysql, Redis 장단점](#/post/f27eda9b-0fe1-8399-953f-81e483af2b4b)
