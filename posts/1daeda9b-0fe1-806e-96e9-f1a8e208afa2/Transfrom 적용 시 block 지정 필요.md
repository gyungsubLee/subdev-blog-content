---
order: 24
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1daeda9b-0fe1-806e-96e9-f1a8e208afa2
title: Transfrom 적용 시 block 지정 필요
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-819c-beab-c6a3a1072bb9
    title: 리액트
  - id: 1d4eda9b-0fe1-80a2-95f7-e975482b1dcd
    title: React + GSAP
  - id: 1daeda9b-0fe1-806e-96e9-f1a8e208afa2
    title: Transfrom 적용 시 block 지정 필요
excerpt: Transfrom 적용 시 block 지정 필요 --- 📖 CSS에서 inline, block, inline-block 요소는 transform이나 x, y 이동 (translateX, translateY) 같은 걸 적용할 때 영향을 크게 미친다. | | | | | --- | --- | --- | | display 종류
cover: null
icon: null
notionProperties:
  Tags: 오류
  상태: 완료
schema_version: 1
parent_id: 1d4eda9b-0fe1-80a2-95f7-e975482b1dcd
created: 2025-04-19T06:10:13.223Z
updated: 2025-04-19T07:03:01.441Z
legacy_path: Main/리액트-c6a3a1072bb9/React + GSAP-e975482b1dcd/Transfrom 적용 시 block 지정 필요-f1a8e208afa2/index.md
legacy_category: 리액트
source_url: https://beautiful-college-c84.notion.site/1daeda9b0fe1806e96e9f1a8e208afa2
---
<a id="1daeda9b0fe180d689f6e9c3081d1f21"></a>

## Transfrom 적용 시 block 지정 필요

---

> 📖 
> 
> <a id="1daeda9b0fe1802bb7efc25516bd8848"></a>
> 
> CSS에서 <code>inline</code>, <code>block</code>, <code>inline&#45;block</code> 요소는 <strong><code>transform</code></strong><strong>이나 </strong><strong><code>x, y 이동 </code></strong><strong>(</strong><strong><code>translateX, translateY</code></strong><strong>)</strong> 같은 걸 적용할 때 <strong>영향을 크게 미친다&#46;</strong>
> 
> |  |  |  |
> | --- | --- | --- |
> | <strong>display 종류</strong> | <strong>특징</strong> | <strong>transform 적용 시</strong> |
> | <code>inline</code> | 글자처럼 흐름 속 존재 | 이동 적용 불안정 (깨질 수 있음) |
> | <code>block</code> | 한 줄 전체 차지, 박스 | 이동 적용 매우 안정적 |
> | <code>inline&#45;block</code> | 글자처럼 흐르면서 박스 성질도 가짐 | 이동 가능하지만 block보단 주의 필요 |
> 
> | <strong>상황</strong> | <strong>추천 display</strong> |
> | --- | --- |
> | 글자 단위로 이동시키고 싶다 | <code>inline&#45;block</code> |
> | 전체 줄(한 문장)이나 블록 덩어리를 움직이고 싶다 | <code>block</code> |

- <strong>display&#58; </strong><strong><code>inline</code></strong> 요소
    - <strong><u>“글자 흐름” 안에서만 존재하는 작은 조각</u></strong>이라서

    - <code>transform</code> 같은 변형이 들어가면 <strong>예상치 못한 문제가 생길 수 있</strong>다&#46;

- <strong>display&#58; </strong><strong><code>block</code></strong> 요소
    - “박스(Box)“처럼 동작

    - <strong><u>위치 이동(y, x, rotate 등)을 명확하게 적용</u></strong>할 수 있다&#46;<br>무

<details>
<summary>ex) &#60;i&#62;  의 기본 display가 inline이다&#46; 따라서 transform 애니메이션 적용 시, 적용시 안되는 오류가 발생되었다&#46;</summary>

> <a href="#/post/1daeda9b-0fe1-80c4-8623-df2d84305d9f">페이지</a> 

<a id="1daeda9b0fe1802d8c68f2cbde0ad879"></a>

<strong>오류</strong>

<a id="1daeda9b0fe180028f23e54d5a41bfb6"></a>

```css
.con4 .mainTextBox .title i {
  /* display 설정 없음 → 기본 display: inline; */
}
```

- &#60;i&#62; 태그&#58;  기본 inline

- 따라서 Inline 요소는 <strong>width, height</strong>를 가지지 않고

- <strong>transform&#58; translateY()</strong> 같은 이동이 제대로 적용되지 않을 때가 있다&#46;

- 그래서 y축으로 150px 이동시키려 했는데, <strong>눈에 보이는 이동이 제대로 발생하지 않았다&#46;</strong><br>

<a id="1daeda9b0fe180eeaf15dbcca366923c"></a>

<strong><br>수정 후 스타일 (정상 작동)</strong>

<a id="1daeda9b0fe180328a92d383d6458611"></a>

```css
.con4 .mainTextBox .title i {
  display: block;
}
```

- block 요소가 되니까 명확한 박스(영역)&#42;&#42;를 가지게 되고<br><code>transform&#58; translateY(150px)</code>도 명확하게 적용된다&#46; 

- 그래서 스크롤에 따라 부드럽게 위로 올라오는 애니메이션이 정상 작동된다&#46;<br>

</details>

<a id="1daeda9b0fe180bf9eecc5b85c2228a3"></a>

### <strong>정리</strong>

|  |  |  |
| --- | --- | --- |
| <strong>display 종류</strong> | <strong>특징</strong> | <strong>transform 적용 시</strong> |
| <code>inline</code> | 글자처럼 흐름 속 존재 | 이동 적용 불안정 (깨질 수 있음) |
| <code>block</code> | 한 줄 전체 차지, 박스 | 이동 적용 매우 안정적 |
| <code>inline&#45;block</code> | 글자처럼 흐르면서 박스 성질도 가짐 | 이동 가능하지만 block보단 주의 필요 |

<a id="1daeda9b0fe18082aab8d654a04e8105"></a>

### 실무 

<a id="1daeda9b0fe1804b9779dfc03471b0fd"></a>

```css
.mainTextBox .title i {
  display: inline-block;
  overflow: hidden;
}
```

- inline&#45;block을 주면 글자처럼 흐르면서 transform도 안정적으로 적용 가능&#46;

- overflow&#58; hidden을 주면, 자식 요소가 넘어갈 때 깔끔하게 가려줄 수 있고<br><strong>그리고 애니메이션에서는 y축으로 부드럽게 이동시킬 수 있다&#46;</strong>
