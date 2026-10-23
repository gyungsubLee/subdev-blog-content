---
order: 49
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1d8eda9b-0fe1-802c-8191-ff1a66f62f42
title: place-items
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-819c-beab-c6a3a1072bb9
    title: 리액트
  - id: 1d4eda9b-0fe1-80a2-95f7-e975482b1dcd
    title: React + GSAP
  - id: 1d8eda9b-0fe1-802c-8191-ff1a66f62f42
    title: place-items
excerpt: "place-items --- 📖 place-items --- css place-items: ; / 만약 하나만 쓰면, 양쪽 모두 같은 값이 적용 / - 세로 방향 정렬(align-items)과 가로 방향 정렬(justify-items)을 한 줄에 같이 설정할 수 있게 만든 속성 - align-items + justify"
cover: null
icon: null
notionProperties:
  Tags: GridBox
  중요도: Yes
  상태: 완료
schema_version: 1
parent_id: 1d4eda9b-0fe1-80a2-95f7-e975482b1dcd
created: 2025-04-17T07:13:41.706Z
updated: 2025-04-18T05:19:24.401Z
legacy_path: Main/리액트-c6a3a1072bb9/React + GSAP-e975482b1dcd/place-items-ff1a66f62f42/index.md
legacy_category: 리액트
source_url: https://beautiful-college-c84.notion.site/1d8eda9b0fe1802c8191ff1a66f62f42
---
<a id="1d8eda9b0fe1807498a6f8b3feba76d4"></a>

## <strong><code>place&#45;items</code></strong>

---

> 📖 
> 
> <a id="1d8eda9b0fe180d9b890d40cb97eb14b"></a>
> 
> <strong><code>place&#45;items</code></strong>
> 
> ---
> 
> <a id="1d8eda9b0fe1808da575c7665f6849ea"></a>
> 
> ```css
> place-items: <세로 정렬 값> <가로 정렬 값>;
> /*	만약 하나만 쓰면, 양쪽 모두 같은 값이 적용 */
> ```
> 
> - <code>세로 방향 정렬(align&#45;items)</code>과 <code>가로 방향 정렬(justify&#45;items)</code>을 <strong>한 줄에 같이</strong> 설정할 수 있게 만든 속성
>     - <strong><code>align&#45;items</code></strong><strong> &#43; </strong><strong><code>justify&#45;items</code></strong><strong>를 합친 단축 속성</strong>
> 
> - <strong><code>place&#45;items</code></strong>는 <strong><u>Grid 레이아웃</u></strong><strong> </strong> 사용
>     - <strong>flexBox</strong> <strong>사용 불가</strong>

<details>
<summary>예시</summary>

<details>
<summary><strong>1&#46; place&#45;items에 하나만 쓸 때</strong></summary>

<a id="1d8eda9b0fe1803bbcacda3e09c47738"></a>

```css
.container {
  display: grid;
  place-items: center;
}
```

- <code>align&#45;items&#58; center</code> &#43; <code>justify&#45;items&#58; center</code> 둘 다 적용됨

</details>

<details>
<summary><strong>2&#46; place&#45;items에 둘 다 따로 지정할 때</strong></summary>

<a id="1d8eda9b0fe1805ca3b9f2832003a3c7"></a>

```css
.container {
  display: grid;
  place-items: start end;
}
```

- 세로(y축, align&#45;items)&#58; start (위쪽 정렬)

- 가로(x축, justify&#45;items)&#58; end (오른쪽 정렬)

</details>

</details>

<details>
<summary>tailwind css</summary>

![](5f53a83873b81c7b.webp)

<a id="1d8eda9b0fe180a6bcb0fa3af8671beb"></a>

```html
<div class="grid place-items-center h-screen">
  <div>가운데 정렬된 박스</div>
</div>
```

</details>

<details>
<summary>요약</summary>

![](64aec5e67cafaeda.webp)

</details>
