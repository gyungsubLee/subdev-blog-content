---
order: 12
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1daeda9b-0fe1-80ec-8c6e-dfdd1ace87ec
title: gsap.utils.toArray()
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-819c-beab-c6a3a1072bb9
    title: 리액트
  - id: 1d4eda9b-0fe1-80a2-95f7-e975482b1dcd
    title: React + GSAP
  - id: 1daeda9b-0fe1-80ec-8c6e-dfdd1ace87ec
    title: gsap.utils.toArray()
excerpt: gsap.utils.toArray() --- ✏️ 동일한 유형의 애니메이션들을 한번에 설정 및 관리 할 수 있다. - 유사한 애니메이션 배열로 만들어서 한번에 적용 - con2 - .mainTextBox .title i - con4 - .mainTextBox .title i javascript gsap.utils.toAr
cover: null
icon: null
notionProperties:
  Tags: GSAP 개념
  상태: 완료
schema_version: 1
parent_id: 1d4eda9b-0fe1-80a2-95f7-e975482b1dcd
created: 2025-04-19T04:55:57.219Z
updated: 2025-04-20T01:56:31.166Z
legacy_path: Main/리액트-c6a3a1072bb9/React + GSAP-e975482b1dcd/gsap.utils.toArray()-dfdd1ace87ec/index.md
legacy_category: 리액트
source_url: https://beautiful-college-c84.notion.site/1daeda9b0fe180ec8c6edfdd1ace87ec
---
<a id="1daeda9b0fe1803daf9df2023e3638c7"></a>

## <code>gsap&#46;utils&#46;toArray()</code>

---

> ✏️ 
> 
> <a id="1daeda9b0fe180f0b3cee2bc4b0a3c71"></a>
> 
> 동일한 유형의 애니메이션들을 한번에 설정 및 관리 할 수 있다&#46;
> 
> - 유사한 애니메이션 배열로 만들어서 한번에 적용
>     - con2 &#45; <code>&#46;mainTextBox &#46;title i</code>
> 
>     - con4 &#45; <code>&#46;mainTextBox &#46;title i</code>

<a id="1daeda9b0fe180458edff4c86e8a2229"></a>

```javascript
gsap.utils.toArray(".subText p").forEach((selector) => {
		gsap.timeline({
				scrollTrigger: {
						trigger: selector,
						start: '100% 100%',
						end: '100% 100%',
						scrub: 1,
						// markers: true
				}
		})
		.fromTo(selector, {opacity: 0, y: 100}, {opactity: 1, y: 0, ease: 'non'.. duration: 5}. 0)
}	

```

-  <code>gsap&#46;utils&#46;toArray(’subText p&#39;)</code>
    - <code>&#46;subText p</code> 의 선택자를 가진 모든 DOM 요소를 선택하여 <code>toArray()</code>를 통해 배열로 변환한다

- <code>toArray()</code>
    - CSS 선택자, NodeList 배열 등을 배열로 변환한다&#46;

- <code>forEach((parm, i) ⇒ {…})</code>
    - 반환된 배열에 대해 forEach를 사용하여 배열의 요소마다 <code>{…}</code> 구문에 대해 반복 작업을 수행한다&#46; 

- <code>gsap&#46;timeline({…})</code>
    - 타임 라인은 트윈과 전체 애니메이션 컨테이너를 제어하고 타이밍을 관리한다&#46; 

- <code>scrollTrigger&#58; {…}</code>
    - 각 param에 대해 ScrollTrigger 인스턴스를 생성하낟&#46; 이를 통해 스크롤 위치에 따른 애니메이션 효과를 제어한다&#46; 

- <code>trigger&#58; panel</code>
    - 현재 패널을 트리거로 설정한다&#46; 

    - 스크롤 위치가 해당 트리거의 시작과 끝 위치 사이로 이동하면 애니메이션 효과가 적용된다&#46; 

- <code>start&#58; ‘top top’</code>
    - 애니메이션 시작 지점을 정의한다&#46; 

    - <code>&#39;top top’</code>은 트리거 요소의 상단이 뷰 포트 상단에 도달했을 때 시작하게 된다&#46; 

- <code>pin&#58; true</code>
    -  트리거 요소를 고정한다&#46;

    - 스크롤 위치가 지정된 시작과 끝 위치 사이일 떄, 트리거 요소가 뷰 포트 내에 고정된다&#46; 

- <code>pinSpacing</code>
    - 트리거 요소가 고정된 상태에서 다른 요소 사이의 공간을 제거한다&#46;

    - 이로써 다음 트리거가 이전 트리거 나타날 수 있게 한다&#46;

<a id="1daeda9b0fe180cda5a2ca86b573c77c"></a>

&#46;

<a id="1daeda9b0fe18016bfb6c59c8775c015"></a>

### 리액트 &#45; tailwind css

<details>
<summary>react</summary>

<a id="1daeda9b0fe180e795cfe6dafc066f3f"></a>

```javascript

```

</details>
