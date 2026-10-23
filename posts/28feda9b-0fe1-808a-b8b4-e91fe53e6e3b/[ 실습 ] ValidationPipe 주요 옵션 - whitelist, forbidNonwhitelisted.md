---
order: 6
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 28feda9b-0fe1-808a-b8b4-e91fe53e6e3b
title: "[ 실습 ] ValidationPipe 주요 옵션 - whitelist, forbidNonwhitelisted"
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 226eda9b-0fe1-802b-a035-c3a886768c4d
    title: Nest.js
  - id: 260eda9b-0fe1-801b-836b-c2e229a88ff9
    title: 한 번에 끝내는 NestJS 패키지 - Part 1. 기초
  - id: 27deda9b-0fe1-8071-8d19-d2363d6d91d0
    title: 유효성 검사 및 변환 ( Class Validator, Class Transformer )
  - id: 28feda9b-0fe1-808a-b8b4-e91fe53e6e3b
    title: "[ 실습 ] ValidationPipe 주요 옵션 - whitelist, forbidNonwhitelisted"
excerpt: 목차 - 주요 옵션-whitelist, forbidNonwhitelisted 주요 옵션-whitelist, forbidNonwhitelisted --- 📖 자바스크립트는 존재하지 않는 속성 접근을 오류로 간주하지 않고, 단순히 undefined로 평가한다. - 자바스크립트의 객체는 클래스 기반 언어의 “정적 타입 구조체
cover: null
icon: null
notionProperties: {}
schema_version: 1
parent_id: 27deda9b-0fe1-8071-8d19-d2363d6d91d0
created: 2025-10-17T08:04:42.944Z
updated: 2025-10-17T08:22:01.737Z
legacy_path: Main/Nest.js-c3a886768c4d/한 번에 끝내는 NestJS 패키지 - Part 1. 기초-c2e229a88ff9/유효성 검사 및 변환 ( Class Validator, Class Transfor-d2363d6d91d0/[ 실습 ] ValidationPipe 주요 옵션 - whitelist, forb-e91fe53e6e3b/index.md
legacy_category: Nest.js
source_url: https://beautiful-college-c84.notion.site/28feda9b0fe1808ab8b4e91fe53e6e3b
---
> 
> 
> <a id="28feda9b0fe180c3ae8cda68b75e9bac"></a>
> 
> <strong>목차</strong>
> 
> - [주요 옵션-whitelist, forbidNonwhitelisted](#28feda9b0fe180dbab13d182dc38993a)

<a id="28feda9b0fe180dbab13d182dc38993a"></a>

## 주요 옵션&#45;<code>whitelist</code>, <code>forbidNonwhitelisted</code>

---

> 📖 
> 
> <a id="28feda9b0fe1807ba5a8ffe98817f206"></a>
> 
> 자바스크립트는 존재하지 않는 속성 접근을 오류로 간주하지 않고, 단순히 <code>undefined</code>로 평가한다&#46; 
> 
> - 자바스크립트의 객체는 클래스 기반 언어의 “정적 타입 구조체(struct)”와 달리, <strong>런타임에 자유롭게 속성을 추가하거나 제거</strong>할 수 있는 <strong><u>해시맵 형태의 동적 자료구조</u></strong>이다
> 
> <a id="28feda9b0fe180999e1feae79da5dfc2"></a>
> 
> 즉, DTO 클래스에 정의되지 않은 속성(필드)가 요청에 담겨 전달될 경우 오류를 발생시키지 않고 해당 필드를 초기화하여 DB에 저장한다&#46; 
> 
> <a id="28feda9b0fe1807c9850c86ef81ffbde"></a>
> 
> 이러한 굉장히 심각한 오류를 ValidationPipe의 <code>whitelist</code>, <code>forbidNonwhitelisted</code> 옵션들을 통해 방지할 수 있다&#46;

![](9a415bb43a529f87.webp)

- <code>whitelist</code>
    > 정의하지 않는 필드 무시   ( 기본값&#58; <code>false</code> )

    <a id="28feda9b0fe1807bbb9cc54a33c242f9"></a>

    자바스크립트에서는 강제 값 삽입이 가능하다&#46;

    <a id="28feda9b0fe180fb978ec8c99be92c9f"></a>

    따라서 실제 DTO에 정의하지 않은 필드를 넣어 요청을 보내면 해당하는 필드가 추가되어 인스턴스가 생성된다&#46; 

    <a id="28feda9b0fe1808da6d3d443899bf59d"></a>

    이를 필터링을 통해 무시하도록 한다&#46;

- <code>forbidNonwhitelisted</code>
    > 정의하지 않은 필드가 요청에 담겨 오는 경우, <code>400 BadRequest</code> 오류를  발생시키다&#46;    ( 기본값&#58; <code>false</code> )

    ![](6cefd8734aca60f3.webp)
