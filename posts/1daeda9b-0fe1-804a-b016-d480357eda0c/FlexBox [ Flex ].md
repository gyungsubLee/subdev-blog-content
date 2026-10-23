---
order: 27
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1daeda9b-0fe1-804a-b016-d480357eda0c
title: FlexBox [ Flex ]
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-819c-beab-c6a3a1072bb9
    title: 리액트
  - id: 1d4eda9b-0fe1-80a2-95f7-e975482b1dcd
    title: React + GSAP
  - id: 1daeda9b-0fe1-804a-b016-d480357eda0c
    title: FlexBox [ Flex ]
excerpt: Flex는 Grid와 함께 레이아웃 적용에 가장 많이 사용되며, 부모요소는 Flex Container라 하며, 자식요소는 Flex Item이라고 합니다. 1. Flex Container ⇒ 부모요소에 정의 Container는 Flex의 영향을 받는 전체 공간으로 설정된 속성에 따라 각각 아이템들이 배치됩니다. Flex I
cover: null
icon: null
notionProperties:
  Tags: FlexBox
  최상단(구분용): Yes
schema_version: 1
parent_id: 1d4eda9b-0fe1-80a2-95f7-e975482b1dcd
created: 2025-04-19T04:51:44.599Z
updated: 2025-04-19T04:53:04.911Z
legacy_path: Main/리액트-c6a3a1072bb9/React + GSAP-e975482b1dcd/FlexBox [ Flex ]-d480357eda0c/index.md
legacy_category: 리액트
source_url: https://beautiful-college-c84.notion.site/1daeda9b0fe1804ab016d480357eda0c
---
<a id="1daeda9b0fe1802fa821ea6e00e9c939"></a>

Flex는 Grid와 함께 레이아웃 적용에 가장 많이 사용되며, 부모요소는 Flex Container라 하며, 자식요소는 Flex Item이라고 합니다&#46;

<a id="1daeda9b0fe180fea298e442181bbed1"></a>

## 1&#46; Flex Container ⇒ 부모요소에 정의

<a id="1daeda9b0fe180d290f8fb0b743571f1"></a>

Container는 Flex의 영향을 받는 전체 공간으로 설정된 속성에 따라 각각 아이템들이 배치됩니다&#46;

<a id="1daeda9b0fe1808c80a1c7d53f12f518"></a>

Flex Item을 가로방향으로 배치하고 , 자신의 내용크기만큼 width를 차지하고 height는 컨테이너의 높이만큼 늘어납니다&#46;

<a id="1daeda9b0fe180b2a94aef0be20cbf05"></a>

### (1) display&#58;flex와  display&#58;inline&#45;flex로 적용하는 것으로 시작

- display &#58; flex ⇒ 컨테이너의  block요소처럼 너비를 100%유지하고 그 안에 아이템을 위치시킴

- display&#58;inline&#45;flex ⇒ inline&#45;block처럼 아이템의 너비만큼 콘테이너의 너비를 결정함&#46;

<a id="1daeda9b0fe180a2a919e0030fb5a194"></a>

### (2) flex&#45;direction ⇒ 배치방향설정

- 아이템들이 배치되는 축의 방향을 결정하는 속성=&#62; 메인축을 가로냐 세로냐를 결정

- flex&#45;direction&#58; row &#45;&#62;기본값으로 아이템이 행(가로)방향으로 배치

- flex&#45;direction &#58; row&#45;reverse; 아이템들이 역순으로 가로 배치

- flex&#45;direction &#58; column; &#45;&#62;아이템들이 열(세로)방향으로 배치되는것으로 block요소처럼 보임

- flex&#45;direcion&#58; column&#45;reverse;

<a id="1daeda9b0fe1807fbd1ec950cc6e2fbc"></a>

### (3) flex&#45;wrap ⇒ 아이템의 줄바꿈을 결정

- flex&#45;wrap &#58; nowrap; &#45;&#62; 기본값으로 줄바꿈을 하지않아 아이템넘치면 컨테이너를 빠져나감

- flex&#45;wrap &#58; wrap; &#45;&#62;줄바꿈이 일어남

- flex&#45;wrap &#58; wrap&#45;reverse; &#45;&#62;줄바꿈이 일어나는데 역순으로 배치됨&#46;

<a id="1daeda9b0fe180639ce9ec63a7739e9c"></a>

### (4) flex&#45;flow ⇒ flex direction과 flex&#45;wrap순으로 한꺼번에 지정할 수 있는 단축속성

<a id="1daeda9b0fe180cc8106fb8e45ac9ad6"></a>

   ex)flex&#45;flow &#58;row wrap;

<a id="1daeda9b0fe180c396f9f1966930c7fb"></a>

### (5) <strong>justify&#45;content =&#62;메인축 방향 정렬</strong>

- justify&#45;content &#58; flex&#45;end ;  &#45;&#62; 아이템들을 끝점으로 정렬

- justify&#45;content &#58; flex&#45;start ;  &#45;&#62; 아이템들을 시작점으로 정렬

- justify&#45;content &#58; center; &#45;&#62; 아이템들을 가운데 정렬

- justify&#45;content &#58; space&#45;between ;&#45;&#62; 컨테이너 양쪽끝을 배치시키고 그 사이에 아이템 간격을 균일하게

- justify&#45;content &#58; space&#45;around ;&#45;&#62; 아이템의 둘레에 균일한 간격을 만들어 줌

- justify&#45;content &#58; space&#45;evenly ;&#45;&#62; 컨테이너 전체에서 아이템들의 간격균등

<a id="1daeda9b0fe1806ba569c4b3972eff88"></a>

### (6) <strong>align&#45;item =&#62;수직축 방향 정렬</strong>

- align&#45;items &#58; stretch; 기본값으로 아이템들이 수직축방향으로 끝까지 쭈욱 늘어남

- align&#45;items &#58; start; 아이템이 시작점으로 정렬

- align&#45;items &#58; flex&#45;end; 아이템이 끝으로 정렬

- align&#45;items &#58; center; 아이템이 가운데 정렬

- align&#45;items &#58; baseline; 아이템이 텍스트 베이스라인기준으로 정렬

- justify&#45;content&#58;center, align&#45;items&#58;center를 주면 가로세로 중앙에 아이템이 정렬됨

<a id="1daeda9b0fe180198b2ef9888b006140"></a>

### (7)align&#45;content ⇒ 여러행 정렬

<a id="1daeda9b0fe180228636cffb2a0cb421"></a>

flex&#45;wrap이 설정된 상태에서 아이템 행이 2줄 이상일때 수직축 방향 정렬

- align&#45;content &#58; flex&#45;start;

- align&#45;content &#58; flex&#45;end;

- align&#45;content &#58; center;

- align&#45;content &#58; space&#45;between;

- align&#45;content &#58; space&#45;around

- align&#45;contet &#58; space&#45;evenly;<br>(justify&#45;content는 가로축을 기준으로 작성되었다면 align&#45;content 수직축방향정렬)

<a id="1daeda9b0fe18005bc72fba1b2c7e3b5"></a>

## 2&#46;Flex Item ⇒ 자식요소에 정의

- flex&#45;basis ⇒ Flex Item의 기본크기를 설정하는데 flex&#45;direction &#58;  row;일땐 너비, 

<a id="1daeda9b0fe180b88428eb68cf1dfdbd"></a>

                          column일때는 높이를 설정&#46;

- flex&#45;grow =&#62; flex&#45;grow는 0보다 큰 값을 세팅하면, Flexible 박스로 변하면서<br>남은 여백을 메우는 속성 (flex&#45;grow는 기본값이 ‘0’이며, 따로 적용하지 않으면 아이템이 늘어나지 않음)

- flex&#45;grow에 들어가는 숫자는 flex&#45;basis에 적용된 값을 제외한 여백부분을<br>flex&#45;grow에 지정된숫자의 비율로 나누어가짐(내용물을 제외한 여백으로 확인)

- flex&#45;grow는 아이템이 flex&#45;basis의 값보다 커질 수 있는지를 결정하는 속성이고,<br>flex&#45;shrink는 flex&#45;grow와 쌍을 이루는 속성을 아이템이 flex&#45;basis의 값보다 작아질 수 있는지를 결정
