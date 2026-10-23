---
order: 2
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 210eda9b-0fe1-8058-abd9-eceec7820379
title: Spring WebFlux + LLM 실전 구현
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-81ae-909e-cd1f71740107
    title: Spring ( Java )
  - id: 210eda9b-0fe1-8058-abd9-eceec7820379
    title: Spring WebFlux + LLM 실전 구현
excerpt: "/icons/push-pingreen.svg [인프런] RabbitMQ를 이용한 비동기 아키텍처 한방에 해결하기 - 정리본 - 기간: 보류 - 강의: ‣ - reference - ‣ - ‣ 목차 - Chapter 1: WebFlux 개념 - Chapter 2: WebFlux 구현 - Chapter 3: WebFlux + "
cover: 2701e0372b259a00.webp
icon: null
notionProperties: {}
schema_version: 1
parent_id: 1c3eda9b-0fe1-81ae-909e-cd1f71740107
created: 2025-06-12T00:36:11.782Z
updated: 2026-04-04T15:50:44.996Z
legacy_path: Main/Spring ( Java )-cd1f71740107/Spring WebFlux + LLM 실전 구현-eceec7820379/index.md
legacy_category: Spring ( Java )
source_url: https://beautiful-college-c84.notion.site/210eda9b0fe18058abd9eceec7820379
---
> /icons/push-pin_green.svg 
> 
> <a id="210eda9b0fe1819f858defd5bee94c91"></a>
> 
> &#91;인프런&#93; <strong>RabbitMQ를 이용한 비동기 아키텍처 한방에 해결하기 &#45; 정리본</strong>
> 
> - 기간&#58; 보류
> 
> - 강의&#58; ‣
> 
> - reference
>     - ‣
> 
>     - ‣

> 
> 
> <a id="28beda9b0fe180cabf03c913547ed6b1"></a>
> 
> 목차
> 
> - [Chapter 1: WebFlux 개념](#210eda9b0fe181d6b6d8f21996602860)
> - [Chapter 2: WebFlux 구현](#212eda9b0fe1808cbe6ad48b7ef81946)
> - [Chapter 3: WebFlux + LLM ( GPT )](#212eda9b0fe180eb9f8df7fa41359fdc)

> 💬 
> 
> <a id="211eda9b0fe1805e8c14c656b4ea4f6b"></a>
> 
> 각 개념들 간의 연결고리를 찾고 각 개념들이 Spring WebFlux에서 어떤 역할을 하는지를 학습한다면 WebFlux를 구현할 때 어떻게 해야하는지 자연스럽게 이해 가능하다&#46; 
> 
> ![](00a36d7f6f14a357.webp)

<a id="210eda9b0fe181d6b6d8f21996602860"></a>

## Chapter 1&#58; WebFlux 개념

[1. WebFLux](#/post/210eda9b-0fe1-8006-a929-face3a590697)

[1.2 SSE ( Server-Sent Events )](#/post/212eda9b-0fe1-800e-910d-cc2100e77faa)

[2. 리액티브 프로그래밍](#/post/210eda9b-0fe1-80cf-9985-f1cd37cb8664)

[3. 스레드 - Netty, Tomcat 비교](#/post/212eda9b-0fe1-80fa-8a40-cf46a578dfc3)

[4. 블로킹, 논블로킹 - 비동기 프로그래밍](#/post/212eda9b-0fe1-8096-8b74-e506e4c363c8)

[5. Reactive Streams, 함수형 프로그래밍](#/post/212eda9b-0fe1-80a1-8caa-ef0a361980c2)

[6. WebFlux - Pub/Sub 패턴](#/post/217eda9b-0fe1-80d7-9f80-dbe392a6e47d)

[7. Netty 와 이벤트 루프 패턴](#/post/212eda9b-0fe1-80a5-b220-c8664b98fe0e)

[[ 추가 ]  Netty 와 이벤트 루프 동작 원리](#/post/21ceda9b-0fe1-80fc-81eb-fec44dbfee1d)

[8. WebFlux, Netty 통합  ( 부제: 이벤트 루프 패턴들 )](#/post/212eda9b-0fe1-80a2-9875-f2a498c5f5db)

[9. WebFlux 블로킹 처리](#/post/212eda9b-0fe1-8050-8056-df0834044f08)

<a id="212eda9b0fe1808cbe6ad48b7ef81946"></a>

## Chapter 2&#58; WebFlux 구현

[1. WebFlux 기본 사용법 -  Flux, Mono](#/post/212eda9b-0fe1-816d-af62-ded0b8b7d476)

[2. Operator 1 - Mono](#/post/212eda9b-0fe1-8100-8547-ee3a3815f26e)

[3. Operator 2 - Flux](#/post/212eda9b-0fe1-802c-97eb-c53413752f6f)

[4. Operator 3 - FluxMap](#/post/212eda9b-0fe1-80da-8151-fd262d340adb)

[5. 시그널, 예외처리](#/post/212eda9b-0fe1-8089-aecc-e21a57363777)

[6. Scheduler](#/post/212eda9b-0fe1-80de-ad28-dfa642e57d21)

<a id="212eda9b0fe180eb9f8df7fa41359fdc"></a>

## Chapter 3&#58; WebFlux &#43; LLM ( GPT )

[1. LLM 서비스 설계, WebClient 1](#/post/212eda9b-0fe1-816f-917c-d2adb3fe81d9)

[1.2 LLM 서비스 설계, WebClient 2](#/post/212eda9b-0fe1-80c3-bdfb-ea7a9fc31539)

[2. 웹 뷰를 위한 간단한 React 프로젝트 설정](#/post/212eda9b-0fe1-813e-afb5-c5df6c8e1700)

[3. Facade API 구현, CORS 설정](#/post/212eda9b-0fe1-8093-a167-e6627008bd47)

[4. Http stream 통신](#/post/212eda9b-0fe1-80dc-ab94-fe7e974e9dd7)

[5. 실전 예외처리](#/post/212eda9b-0fe1-80f5-a8e9-c6ba5e72bdc8)

[6. Chain of Thought 1](#/post/212eda9b-0fe1-80c1-8ae1-c19615095659)

[7. Chain of Thought 2](#/post/212eda9b-0fe1-8011-bd01-e5dee53a8767)

[제목 없음](#/post/236eda9b-0fe1-8007-a2dd-d618f53e8c97)

[제목 없음](#/post/236eda9b-0fe1-80be-9fd8-c3a35234a47c)
