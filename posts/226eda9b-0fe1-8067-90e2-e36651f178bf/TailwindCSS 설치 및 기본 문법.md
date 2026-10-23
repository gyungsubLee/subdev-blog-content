---
order: 6
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 226eda9b-0fe1-8067-90e2-e36651f178bf
title: TailwindCSS 설치 및 기본 문법
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 226eda9b-0fe1-802b-a035-c3a886768c4d
    title: Nest.js
  - id: 226eda9b-0fe1-80c9-b906-d1c0ad48e506
    title: "[ 풀스택 ] 인프런 클론 코딩 Next.js ,  Nest.js ( Part1 )"
  - id: 226eda9b-0fe1-8067-90e2-e36651f178bf
    title: TailwindCSS 설치 및 기본 문법
excerpt: 목차 - 1. 설치 - 2. 연습 - 3. 기본 문법 - Basic - Flex Box - Grid Box - Text - Border - Decoration? 1. 설치 [Installing with Vite - Installation]() 2. 연습 [Tailwind Play]() 3. 기본 문법 {…} 안은 실제 값
cover: fb3b1ee7da4a15e0.webp
icon: 9bed2eae1e079b4b.avif
notionProperties: {}
schema_version: 1
parent_id: 226eda9b-0fe1-80c9-b906-d1c0ad48e506
created: 2025-07-04T04:08:10.375Z
updated: 2025-07-04T08:25:00.003Z
legacy_path: Main/Nest.js-c3a886768c4d/[ 풀스택 ] 인프런 클론 코딩 Next.js ,  Nest.js ( Part1 -d1c0ad48e506/TailwindCSS 설치 및 기본 문법-e36651f178bf/index.md
legacy_category: Nest.js
source_url: https://beautiful-college-c84.notion.site/226eda9b0fe1806790e2e36651f178bf
---
> 
> 
> <a id="226eda9b0fe181b599aad4d55256eb9a"></a>
> 
> <strong>목차</strong>
> 
> - [1. 설치](#226eda9b0fe1800ba544dee2b2d312a2)
> - [2. 연습](#226eda9b0fe18078ade8d8696fb10f1f)
> - [3. 기본 문법](#226eda9b0fe180169430d4b94c8eca9c)
> - [Basic](#226eda9b0fe180ac8de8f3e110ca04e0)
> - [Flex Box](#226eda9b0fe18017a9f4d323b2ebbbdb)
> - [Grid Box](#226eda9b0fe1803684a1fb40ea690a90)
> - [Text](#226eda9b0fe180348caeda48c34d9df5)
> - [Border](#226eda9b0fe18004b4b2dabbd3b2b751)
> - [Decoration?](#226eda9b0fe180d19867cdb829af068b)

<a id="226eda9b0fe1800ba544dee2b2d312a2"></a>

### 1&#46; 설치

[Installing with Vite &#45; Installation]()

<a id="226eda9b0fe18078ade8d8696fb10f1f"></a>

### 2&#46; 연습

[Tailwind Play]()

<a id="226eda9b0fe180169430d4b94c8eca9c"></a>

## 3&#46; 기본 문법

> 
> 
> <a id="226eda9b0fe180ac8492d49bdbdd97ad"></a>
> 
> <code>{…}</code> 안은 실제 값을 설정해야 합니다&#46; 

<a id="226eda9b0fe180ac8de8f3e110ca04e0"></a>

### Basic

- <code>bg&#45;{color}</code>&#58;  요소의 배경색 설정

- <code>p&#45;{n}</code>&#58; 요소의 padding 설정

- <code>m&#45;{n}</code>&#58; 요소의 margin 설정

- <code>w&#45;{n}</code>&#58; 요소의 너비(width) 설정

- <code>h&#45;{n}</code>&#58; 요소의 높이(height) 설정

<a id="226eda9b0fe18017a9f4d323b2ebbbdb"></a>

### Flex Box

- <code>flex</code>&#58; Floxbox 레이아웃 설정

- <code>flex&#45;col</code>&#58; Flexbox 레이아웃에서 아이템들을 수직 방향(위&#45;아래)으로 배치

- <code>flex&#45;row</code>&#58; Flexbox 레이아웃에서 아이템들을 수평 방향(왼쪽&#45;오른쪽)으로 배치

- <code>justify&#45;{keyword}</code>&#58; Flexbox 아이템의 수평 정렬 설정
    - ex) <code>justify&#45;center</code>&#58; 아이템 <strong><u>수평 중앙</u></strong> 배치

- <code>items&#45;{keyword}</code>&#58; Flexbox 아이템의 수직 정렬 설정
    - ex) <code>items&#45;center</code>&#58; 아이템 <strong><u>수직 중앙</u></strong> 배치

- <code>flex&#45;{n}</code>&#58; Flexbox 아이템의 성장, 축소 및 크기 설정
    - ex) <code>flex&#45;1</code>&#58;  아이템을 사용 가능한 공간에 균등하게 차지

<a id="226eda9b0fe1803684a1fb40ea690a90"></a>

### Grid Box

- <code>grid</code>&#58; Grid 레이아웃 설정

- <code>grid&#45;cols&#45;{n}</code>&#58; Grid 레이아웃의 <strong><u>열의 수</u></strong> 설정
    - ex) <code>grid&#45;cols&#45;3</code>&#58;  Grid 레이아웃에 3개의 열 생성

- <code>col&#45;span&#45;{n}</code>&#58;  그리드 아이템이 차지하는 열의 수를 설정
    - ex) <code>col&#45;span&#45;2</code>&#58; 그리드 아이템이 두 열을 차지하도록 함

<a id="226eda9b0fe180348caeda48c34d9df5"></a>

### Text

- <code>text&#45;{size}</code>&#58; 글자 크기 설정
    - ex) <code>text&#45;lg</code>&#58; 큰 글자 적용 

- <code>text&#45;{color}</code>&#58; 글자 색상 설정
    - ex) <code>text&#45;red&#45;500</code>&#58; 글자 색상 &#45; 빨간색

- <code>font&#45;{keyword}</code>&#58; 글자 스타일 설정
    - ex) <code>font&#45;bold</code>&#58; 글자 굵게

<a id="226eda9b0fe18004b4b2dabbd3b2b751"></a>

### Border

- <code>border&#45;{color}</code>&#58; 테두리(border) 색상 설정

- <code>rounded&#45;{keyword}</code>&#58;  테두리(border) 둥굴기(round) 설정

<a id="226eda9b0fe180d19867cdb829af068b"></a>

### Decoration?

- <code>shadow&#45;{keyword}</code>&#58; 요소의 그림자 설정
    - ex) <code>shadow&#45;lg</code>&#58; 요소에 큰 그림자 적용

- <code>tracking&#45;{keyword}</code>&#58; 줄 간격 설정

- <code>z&#45;{n}</code>&#58; 요소의 z&#45;index 값 설정
