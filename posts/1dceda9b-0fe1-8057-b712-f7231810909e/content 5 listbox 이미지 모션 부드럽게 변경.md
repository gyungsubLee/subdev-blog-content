---
order: 4
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1dceda9b-0fe1-8057-b712-f7231810909e
title: content 5 listbox 이미지 모션 부드럽게 변경
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-819c-beab-c6a3a1072bb9
    title: 리액트
  - id: 1d4eda9b-0fe1-80a2-95f7-e975482b1dcd
    title: React + GSAP
  - id: 1dceda9b-0fe1-8057-b712-f7231810909e
    title: content 5 listbox 이미지 모션 부드럽게 변경
excerpt: 리펙토링 전 javascript listBox[i].addEventListener('mousemove', (e) = { mouseX = e.pageX + 20; mouseY = e.pageY - 230; imgBox.style.left = imgBoxX + 'px'; imgBox.style.top = imgBoxY + '
cover: null
icon: null
notionProperties:
  Tags: 리펙토링
  상태: 완료
schema_version: 1
parent_id: 1d4eda9b-0fe1-80a2-95f7-e975482b1dcd
created: 2025-04-21T04:55:34.327Z
updated: 2025-04-21T06:23:07.644Z
legacy_path: Main/리액트-c6a3a1072bb9/React + GSAP-e975482b1dcd/content 5 listbox 이미지 모션 부드럽게 변경-f7231810909e/index.md
legacy_category: 리액트
source_url: https://beautiful-college-c84.notion.site/1dceda9b0fe18057b712f7231810909e
---
<a id="1dceda9b0fe18048a7ade7156d54138b"></a>

### 리펙토링 전 

<a id="1dceda9b0fe18029aac9dbae7a3e4546"></a>

```javascript
listBox[i].addEventListener('mousemove', (e) => {
		mouseX = e.pageX + 20;
		mouseY = e.pageY - 230;
		imgBox.style.left = imgBoxX + 'px';
		imgBox.style.top = imgBoxY + 'px';
}
```

<a id="1dceda9b0fe180bfa69fc77f01c51642"></a>

### 리펙토링 후 

<a id="1dceda9b0fe180e9987ad61220434af1"></a>

```javascript
let mouseX = 0;
let mouseY = 0;
let currentX = 0;
let currentY = 0;

listBox.forEach((item) => {
		item.addEventListener('mousemove', (e) => {
        mouseX = e.pageX + 20;
        mouseY = e.pageY - 230;
		});
});

// 딜레이 모션
gsap.ticker.add(() => {
    currentX += (mouseX - currentX) * 0.2;  // 0.2는 따라오는 정도 (0.1 ~ 0.3 추천)
    currentY += (mouseY - currentY) * 0.2;
    
    gsap.set(imgBox, {
        left: currentX,
        top: currentY
    });
});
```

- <code>gsap&#46;ticker()</code>
    <a id="1dceda9b0fe180979d4ecf05cd05982c"></a>

    마우스 모션에 따라 이미지를 살짝 늦춰서 부드럽게 따라올 수 있도록 함

    - ease를 <code>power3&#46;out</code>, <code>power4&#46;out</code>, <code>expo&#46;out</code> 로 주면 더 부드러운 애니메이션 동작이 가능하다&#46;

    - duration은 보통 <code>0&#46;2</code> &#126; <code>0&#46;3</code>  초 정도가 적합하다&#46;<br><br>
