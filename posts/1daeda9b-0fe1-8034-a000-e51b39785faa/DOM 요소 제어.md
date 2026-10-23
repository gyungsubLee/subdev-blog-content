---
order: 28
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1daeda9b-0fe1-8034-a000-e51b39785faa
title: DOM 요소 제어
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-819c-beab-c6a3a1072bb9
    title: 리액트
  - id: 1d4eda9b-0fe1-80a2-95f7-e975482b1dcd
    title: React + GSAP
  - id: 1daeda9b-0fe1-8034-a000-e51b39785faa
    title: DOM 요소 제어
excerpt: DOM요소 제어 --- - Document.querySelector( selectors ) - ( ) 안의 선택자와 일치하는 첫번째 요소를 반환 - 만약 일치하는 요소가 없으면 null을 반환 - Document.querySelectorAll(selectors) - 선택자와 일치하는 요소의 모든 목록을 선택할 때 사용 -
cover: null
icon: null
notionProperties:
  Tags: JS
  상태: 완료
schema_version: 1
parent_id: 1d4eda9b-0fe1-80a2-95f7-e975482b1dcd
created: 2025-04-19T04:34:19.019Z
updated: 2025-04-19T04:50:16.790Z
legacy_path: Main/리액트-c6a3a1072bb9/React + GSAP-e975482b1dcd/DOM 요소 제어-e51b39785faa/index.md
legacy_category: 리액트
source_url: https://beautiful-college-c84.notion.site/1daeda9b0fe18034a000e51b39785faa
---
<a id="1daeda9b0fe1806f8d66f240746b81dc"></a>

# DOM요소 제어

---

- <code>Document&#46;querySelector( selectors )</code> 
    - <code>( )</code> 안의 선택자와 일치하는  첫번째 요소를 반환

    - 만약 일치하는 요소가 없으면 null을 반환 

- <code>Document&#46;querySelectorAll(selectors)</code>
    - 선택자와 일치하는 요소의 모든 목록을 선택할 때 사용

- <code>addEventListener(”event”)</code> 
    -  document의 특정요소(id class 변수&#46;&#46;)에  이벤트를 등록할 때 사용하는 메서드

    - 가장 권장되는 방식

    - 해당 메서드를 사용하면 여러 개의 이벤트 핸들러를 등록할 수 있다&#46;

- <code>Element&#46;classList</code> 
    - 엘리먼트의 클래스 목록에 접근하는 읽기전용 프로퍼티입이다&#46;
