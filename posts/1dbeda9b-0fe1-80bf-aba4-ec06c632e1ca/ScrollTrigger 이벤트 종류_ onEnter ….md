---
order: 8
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1dbeda9b-0fe1-80bf-aba4-ec06c632e1ca
title: "ScrollTrigger 이벤트 종류: onEnter …"
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-819c-beab-c6a3a1072bb9
    title: 리액트
  - id: 1d4eda9b-0fe1-80a2-95f7-e975482b1dcd
    title: React + GSAP
  - id: 1dbeda9b-0fe1-80bf-aba4-ec06c632e1ca
    title: "ScrollTrigger 이벤트 종류: onEnter …"
excerpt: "[ScrollTrigger | GSAP | Docs & Learning]() ScrollTrigger 이벤트 종류 📖 ScrollTrigger 이벤트 종류 간단 비교 --- | 이벤트 이름 | 설명 | 스크롤 방향 | | --- | --- | --- | | onEnter | 요소가 뷰포트에 들어올 때 | 아래로 스크롤할"
cover: null
icon: null
notionProperties:
  Tags: GSAP 개념
  중요도: Yes
  상태: 완료
schema_version: 1
parent_id: 1d4eda9b-0fe1-80a2-95f7-e975482b1dcd
created: 2025-04-20T02:03:50.185Z
updated: 2025-04-20T03:18:18.779Z
legacy_path: Main/리액트-c6a3a1072bb9/React + GSAP-e975482b1dcd/ScrollTrigger 이벤트 종류- onEnter …-ec06c632e1ca/index.md
legacy_category: 리액트
source_url: https://beautiful-college-c84.notion.site/1dbeda9b0fe180bfaba4ec06c632e1ca
---
[ScrollTrigger &#124; GSAP &#124; Docs &#38; Learning]()

<a id="1dbeda9b0fe1802093b0c6f360b61b0e"></a>

## <strong>ScrollTrigger 이벤트 종류</strong>

> 📖 
> 
> <a id="1dbeda9b0fe180458cf0ebbb655ac955"></a>
> 
> <strong>ScrollTrigger 이벤트 종류 간단 비교</strong>
> 
> ---
> 
> | <strong>이벤트 이름</strong> | <strong>설명</strong> | <strong>스크롤 방향</strong> |
> | --- | --- | --- |
> | <code>onEnter</code> | 요소가 <u>뷰포트에 들</u>어올 때 | <strong><u>아래로 스크롤</u></strong><strong>할 때만</strong> |
> | <code>onEnterBack</code> | 요소가 <u>다시 뷰포트에 들</u>어올 때 | <strong><u>위로 스크롤</u></strong><strong>할 때만</strong> |
> | <code>onLeave</code> | 요소가 <u>뷰포트에서 나갈</u> 때 | <strong><u>아래로 스크롤</u></strong><strong>할 때만</strong> |
> | <code>onLeaveBack</code> | 요소가 <u>뷰포트에서 다시 나갈</u> 때 | <strong><u>위로 스크롤</u></strong><strong>할 때만</strong> |

> ✏️ 
> 
> <a id="1dbeda9b0fe180209995e9891eaa530e"></a>
> 
> <strong>Point</strong>
> 
> ---
> 
> - <code>onEnter</code> → 스크롤 <strong>아래</strong> 방향 진입
> 
> - <code>onEnterBack</code> → 스크롤 <strong>위</strong> 방향 진입

<details>
<summary><strong><code>onEnter</code></strong><strong>&#58; 스크롤 아래로 내릴 때만</strong></summary>

---

> ✏️ 
> 
> <a id="1dbeda9b0fe180558f31dde2abe25458"></a>
> 
> <strong><code>onEnter&#58; () ⇒ {…}</code></strong>
> 
> ---
> 
> <a id="1dbeda9b0fe1800c9703e4da35db9cc5"></a>
> 
> <strong><code>onEnter</code></strong>는 요소가 <code>viewport</code>에 <strong>들어올 때(enter) 트리거</strong>되는 이벤트이다&#46;
> 
> <a id="1dbeda9b0fe18068b315dcda9aadfed3"></a>
> 
> 즉, <strong><u>아래 스크롤 </u></strong><strong><u>시 </u></strong><strong><u>viewport에 들</u></strong>어올 때 <strong><u>트리거가 발생</u></strong>된다&#46; 

<details>
<summary>ex) </summary>

<a id="1dbeda9b0fe180229050f9f6b509706a"></a>

```javascript
gsap.utils.toArray('.con3 .listBox li').forEach((selector, idx) => {
    ScrollTrigger.create({
        trigger: selector,
        start: '30% 50%',
        onEnter: () => {
            gsap.set(selector, {
                rotationX: '-65deg',
                z: '-500px',
                opacity: 0
            }),
            gsap.to(selector, {
                rotationX: 0,
                z: 0,
                opacity: 1,
                delay: idx % 3 * .05
            })
        },
        markers: true
    })
})
```

![](1a4fd2bcb67de2ca.webp)

- Scroll이 아래로 진행될 때만 이벤트 트리거가 발생되어 애니메이션이 진행된다&#46; 

</details>

</details>

<a id="1dbeda9b0fe1802787cdec61728d2135"></a>

## <strong><code>toggleActions</code></strong>

---

> ✏️ 
> 
> <a id="1dbeda9b0fe18054bb9bd65bb1f3870d"></a>
> 
> <strong>toggleActions</strong>
> 
> ---
> 
> <a id="1dbeda9b0fe1804f9d1ef2d55632559c"></a>
> 
> <strong><code>toggleActions</code></strong><strong>으로 </strong><u>위 4개의 이벤트 한번에 설정</u><strong> 가능하다&#46;</strong>
> 
> <a id="1dbeda9b0fe180fdac38d3f6a9d48bcc"></a>
> 
> ```javascript
> toggleActions: ‘{onEnter} {onLeave} {onEnterBack} {onLeaveBack}`
> 
> // ex. toggleActions: 'play none none reset'
> ```

<details>
<summary>ex)</summary>

<a id="1dbeda9b0fe18048b5caee2536f2f9a8"></a>

```javascript
ScrollTrigger.create({
  trigger: selector,
  start: '30% 50%',
  toggleActions: 'play none none reset', // 이거 한 줄이면 끝
  animation: gsap.fromTo(selector, 
    {
      rotationX: '-65deg',
      z: '-500px',
      opacity: 0
    }, 
    {
      rotationX: 0,
      z: 0,
      opacity: 1,
      delay: idx % 3 * 0.05
    }
  ),
  markers: true
})
```

</details>
