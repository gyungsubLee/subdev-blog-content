---
order: 30
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1daeda9b-0fe1-8064-bec6-c0d7c7a05f96
title: classList
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-819c-beab-c6a3a1072bb9
    title: 리액트
  - id: 1d4eda9b-0fe1-80a2-95f7-e975482b1dcd
    title: React + GSAP
  - id: 1daeda9b-0fe1-8064-bec6-c0d7c7a05f96
    title: classList
excerpt: "[classList.replace()]() classList 속성 --- ✏️ Element.classList.속성() --- - Element.classList로 Element를 반환하는 읽기전용 속성 DomtokenList [add() , remove(), replace(), toggle() ]를 사용하여 DOM의 클"
cover: null
icon: null
notionProperties:
  Tags: JS
  상태: 완료
schema_version: 1
parent_id: 1d4eda9b-0fe1-80a2-95f7-e975482b1dcd
created: 2025-04-19T04:36:52.931Z
updated: 2025-04-19T04:43:35.568Z
legacy_path: Main/리액트-c6a3a1072bb9/React + GSAP-e975482b1dcd/classList-c0d7c7a05f96/index.md
legacy_category: 리액트
source_url: https://beautiful-college-c84.notion.site/1daeda9b0fe18064bec6c0d7c7a05f96
---
[classList&#46;replace()]()

<a id="1daeda9b0fe1805ab052ceca4d9254b5"></a>

## classList 속성

---

> ✏️ 
> 
> <a id="1daeda9b0fe180419799dec3018039c6"></a>
> 
> <code>Element&#46;classList&#46;</code><u><code>속성</code></u><code>()</code>
> 
> ---
> 
> -  Element&#46;classList로 Element를 반환하는 읽기전용 속성
> 
> > <strong><code>DomtokenList</code></strong> &#91;<code>add()</code> ,<code> remove()</code>, <code>replace(),</code> <code>toggle()</code> &#93;를 사용하여 DOM의 클래스(CSS) 수정
> 
> - <code>classList&#46;add(클래스명)</code>&#58; 해당 DOM 클래스(CSS) 추가
> 
> - <code>classList&#46;remove(클래스명)</code>&#58;  해당 DOM에 클래스(CSS) 제거
> 
> - <code>classList&#46;replace(클래스명)</code>&#58;  해당 DOM에 클래스(CSS) 변경
> 
> - <code>classList&#46;toggle(클래스명)</code>&#58;  해당 DOM에 클래스(CSS)가 없는 경우 추가, 있는 경우 다시 제거, 반복

<a id="1daeda9b0fe18096837beb0446b5051c"></a>

<strong>예제</strong>

<a id="1daeda9b0fe180c3b2c9f831a11b320f"></a>

```javascript
setTimeout(() => loading.classList.add("scene1"), 0), .loading에 0초 뒤 scene1 클래스 추가
setTimeout(() => loading.classList.add("scene2"), 1500), .loading 에 1.5초 뒤 scene2 클래스 추가
setTimeout(() => loading.classList.remove("scene1" , "scene2"), 2500), .loading에 2.5초 뒤 scene 1과 scene2 클래스 지워줌
setTimeout(() => rotate.forEach(rotate => { rotate.classList.add('on') }), 2500), 2.5초 뒤 rotate에 .on 붙임
setTimeout(() => opacity.forEach(opacity => { opacity.classList.add('on') }), 2500);  2.5초 뒤  opacity에 .on 붙임
```
