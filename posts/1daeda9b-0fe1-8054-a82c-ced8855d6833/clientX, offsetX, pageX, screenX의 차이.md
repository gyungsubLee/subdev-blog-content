---
order: 32
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1daeda9b-0fe1-8054-a82c-ced8855d6833
title: clientX, offsetX, pageX, screenX의 차이
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-819c-beab-c6a3a1072bb9
    title: 리액트
  - id: 1d4eda9b-0fe1-80a2-95f7-e975482b1dcd
    title: React + GSAP
  - id: 1daeda9b-0fe1-8054-a82c-ced8855d6833
    title: clientX, offsetX, pageX, screenX의 차이
excerpt: "[clientX, offsetX, pageX, screenX 차이]() 4.clientX, offsetX, pageX, screenX의 차이 --- (1) clientX, clientY clientX, clientY 메서드는 클라이언트 영역 내의 가로, 세로 좌표를 제공합니다. 여기서 클라이언트 영역은 현재 보이는 브라우"
cover: null
icon: null
notionProperties:
  Tags: JS
  상태: 진행 중
schema_version: 1
parent_id: 1d4eda9b-0fe1-80a2-95f7-e975482b1dcd
created: 2025-04-19T04:31:32.363Z
updated: 2025-04-19T04:34:09.161Z
legacy_path: Main/리액트-c6a3a1072bb9/React + GSAP-e975482b1dcd/clientX, offsetX, pageX, screenX의 차이-ced8855d6833/index.md
legacy_category: 리액트
source_url: https://beautiful-college-c84.notion.site/1daeda9b0fe18054a82cced8855d6833
---
[clientX, offsetX, pageX, screenX  차이]()

<a id="1daeda9b0fe1801cbe19f072919f8c2e"></a>

## 4&#46;clientX, offsetX, pageX, screenX의 차이

---

<a id="1daeda9b0fe1804d8ebefdcfef0177c7"></a>

### (1) clientX, clientY

<a id="1daeda9b0fe180f8b369f0552d39adea"></a>

 clientX, clientY 메서드는 클라이언트 영역 내의 가로, 세로 좌표를 제공합니다&#46; 여기서 클라이언트 영역은 현재 보이는 브라우저 화면이 기준이 됩니다&#46;

- <strong>clientX</strong> &#58; 브라우저 페이지에서의 X좌표 위치를 반환하나 스크롤은 무시하고 해당 페이지의 상단을 0으로 측정합니다&#46;

- <strong>clientY</strong> &#58; 브라우저 페이지에서의 Y좌표 위치를 반환하나 스크롤은 무시하고 해당 페이지의 상단을 0으로 측정합니다&#46;

<a id="1daeda9b0fe1807391eaf03ce47f4cf1"></a>

### (2) offsetX, offsetY

<a id="1daeda9b0fe18022b368cca8f8ea0889"></a>

offsetX, offsetY 메서드는 이벤트 대상이 기준이 됩니다&#46; ( 화면 중간에 있는 박스 내부에서 클릭한 위치를 찾을 때 해당 박스의 왼쪽 모서리 좌표가 0이됩니다&#46; 화면의 기준이 아닙니다)

<a id="1daeda9b0fe180d39e74dd06232a6b6c"></a>

전체 문서를 기준으로 합니다(스크롤 화면 포함)

- <strong>offsetX</strong> &#58; 이벤트 대상 객체에서의 상대적 마우스 x좌표 위치를 반환합니다&#46;

- <strong>offsetY</strong> &#58; 이벤트 대상 객체에서의 상대적 마우스 y좌표 위치를 반환합니다&#46;

<a id="1daeda9b0fe180248949dc07d15a9da6"></a>

### (3) pageX, pageY

<a id="1daeda9b0fe1807b941ce12e2b0538ff"></a>

 pageX, pageY메서드는 전체 문서를 기준으로 x, y 좌표를 반환 합니다&#46; 스크롤 화면을 포함해서 측정합니다&#46;

- <strong>pageX</strong> &#58; 브라우저 페이지에서의 x좌표 위치를 반환합니다&#46;

- <strong>pageY</strong> &#58; 브라우저 페이지에서의 Y좌표 위치를 반환합니다&#46;

<a id="1daeda9b0fe18025a22ada1adc06c709"></a>

### (4) screenX, screenY

<a id="1daeda9b0fe18031ae0cc2ab87f606c3"></a>

 screenX, screenY 메서드는 모니터 화면을 기준으로 좌표를 제공합니다&#46; 여기서 중요한 점은 브라우저 화면이 아니라 자신의 모니터 화면 전체를 기준으로 좌표를 측정한다는 점입니다&#46;

- <strong>screenX</strong> &#58; 전체 모니터 스크린에서의 x좌표 위치를 반환합니다&#46;

- <strong>screenY</strong> &#58; 전체 모니터 스크린에서의 y좌표 위치를 반환합니다&#46;
