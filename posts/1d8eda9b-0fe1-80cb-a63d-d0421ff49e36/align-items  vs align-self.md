---
order: 54
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1d8eda9b-0fe1-80cb-a63d-d0421ff49e36
title: align-items  vs align-self
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-819c-beab-c6a3a1072bb9
    title: 리액트
  - id: 1d4eda9b-0fe1-80a2-95f7-e975482b1dcd
    title: React + GSAP
  - id: 1d8eda9b-0fe1-80cb-a63d-d0421ff49e36
    title: align-items  vs align-self
excerpt: "align-items vs align-self --- 📖 - align-items: 부모가 자식들 전체를 정렬 - -align-self: 자식 하나가 나만 정렬 다르게 할래요! 하는 것 예시 html css .container { display: flex; align-items: center; / 모든 자식이 세로 가운"
cover: null
icon: null
notionProperties:
  Tags: GridBox
  중요도: Yes
  상태: 완료
schema_version: 1
parent_id: 1d4eda9b-0fe1-80a2-95f7-e975482b1dcd
created: 2025-04-17T07:10:22.120Z
updated: 2025-04-18T05:17:24.495Z
legacy_path: Main/리액트-c6a3a1072bb9/React + GSAP-e975482b1dcd/align-items  vs align-self-d0421ff49e36/index.md
legacy_category: 리액트
source_url: https://beautiful-college-c84.notion.site/1d8eda9b0fe180cba63dd0421ff49e36
---
<a id="1d8eda9b0fe1804dadf1f6b5e3c777c3"></a>

## <code>align&#45;items</code> vs <code>align&#45;self</code>

---

> 📖 
> 
> ![](3696ac646b139905.webp)
> 
> - <code>align&#45;items</code>&#58; <strong>부모가 자식들 전체를 정렬</strong>
> 
> - &#45;<code>align&#45;self</code>&#58; <strong>자식 하나가 </strong><strong><u>나만 정렬 다르게 할래요</u></strong><strong>&#33; 하는 것</strong>

<details>
<summary><strong>예시</strong></summary>

<a id="1d8eda9b0fe18048877becf19f52507f"></a>

```html
<div class="container">
  <div class="box A"></div>
  <div class="box B"></div>
  <div class="box C"></div>
</div>
```

<a id="1d8eda9b0fe180c6a6e2c84e4b80daec"></a>

```css
.container {
  display: flex;
  align-items: center; /* 모든 자식이 세로 가운데 정렬됨 */
}

.box.B {
  align-self: flex-end; /* B 박스만 아래쪽 정렬됨 */
}
```

- <code>align&#45;items&#58; center</code>&#58; A, B, C 모두를 <strong>가운데 기준</strong>으로 정렬

- <code>align&#45;self&#58; flex&#45;end</code>&#58;B만 <strong>개별적으로 아래쪽 정렬</strong>

</details>

<details>
<summary><strong>Tailwind CSS</strong></summary>

![](c763afd3453bd3da.webp)

<a id="1d8eda9b0fe18062a323e4d1619b9dad"></a>

```html
<div class="flex items-center">
  <div class="self-start">👈 얘만 위로 정렬</div>
  <div>나머지는 가운데 정렬</div>
</div>
```

</details>
