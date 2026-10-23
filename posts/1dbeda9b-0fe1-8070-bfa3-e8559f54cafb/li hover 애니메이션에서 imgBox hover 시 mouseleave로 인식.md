---
order: 7
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1dbeda9b-0fe1-8070-bfa3-e8559f54cafb
title: li hover 애니메이션에서 imgBox hover 시 mouseleave로 인식
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-819c-beab-c6a3a1072bb9
    title: 리액트
  - id: 1d4eda9b-0fe1-80a2-95f7-e975482b1dcd
    title: React + GSAP
  - id: 1dbeda9b-0fe1-8070-bfa3-e8559f54cafb
    title: li hover 애니메이션에서 imgBox hover 시 mouseleave로 인식
excerpt: 문제 --- js(gsap) 코드 javascript const listBox = document.querySelectorAll('.con5 .listBox li'); const imgBox = document.querySelector('.con5 .imgBox'); const img = document.querySele
cover: null
icon: null
notionProperties:
  Tags: 오류
  상태: 완료
schema_version: 1
parent_id: 1d4eda9b-0fe1-80a2-95f7-e975482b1dcd
created: 2025-04-20T05:00:03.804Z
updated: 2025-04-20T05:11:10.987Z
legacy_path: Main/리액트-c6a3a1072bb9/React + GSAP-e975482b1dcd/li hover 애니메이션에서 imgBox hover 시 mouseleave로 인-e8559f54cafb/index.md
legacy_category: 리액트
source_url: https://beautiful-college-c84.notion.site/1dbeda9b0fe18070bfa3e8559f54cafb
---
<a id="1dbeda9b0fe180e7afbce5799d5c6701"></a>

### 문제

---

![](7d85367e206f1af4.webp)

<details>
<summary>js(gsap) 코드</summary>

<a id="1dbeda9b0fe1807caaa8e59ab1bfddda"></a>

```javascript
const listBox = document.querySelectorAll('.con5 .listBox li');
const imgBox = document.querySelector('.con5 .imgBox');
const img = document.querySelector('.con5 .imgBox img');

for(let i = 0; i < listBox.length; i++) {
    listBox[i].addEventListener('mouseenter', () => {
        img.src =`images/img${i}.jpg`;

        gsap.fromTo(imgBox, 
            {scale: 0, opacity: 0},  
            {scale: 1, opacity: 1, duration: 0.3}
        );
    });

    listBox[i].addEventListener('mousemove', (e) => {
        let imgBoxX = e.pageX + 20;
        let imgBoxY = e.pageY - 20;
        imgBox.style.left = imgBoxX + 'px';
        imgBox.style.top = imgBoxY + 'px';
    })
    
    listBox[i].addEventListener('mouseleave', () => {
        gsap.to(imgBox, {scale:0, opacity:0, duration:.3})
    });
}
```

</details>

<a id="1dbeda9b0fe18080a3faf4d3870cddc1"></a>

li hover 시에 생기는 imgBox에 마우스가 hover 되면 

<a id="1dbeda9b0fe180d6a1a0cb3b53ee3a8d"></a>

<code>mouseleave </code>로 인식되어 img가 사라진다&#46; 

- <code>imgBox</code>의 크기가 ‘줄었다 커졌다’하는  애니메이션이 발생됨

<a id="1dbeda9b0fe180ed87bed8ca38913f74"></a>

### 해결&#58; <code>pointer&#45;events&#58; none</code>

---

![](3d3ac1d9d28144f1.webp)

<a id="1dbeda9b0fe180449bc1f3bc8c568844"></a>

```javascript
.con5 .imgBox { 
	position: absolute; 
	transform: scale(0); 
	opacity: 0; 
	z-index: 100; 
	transition: all .1s; 
	pointer-events: none;
}
```

<a id="1dbeda9b0fe1804190b4f5d73b297470"></a>

&#46;imgBox에 <code>pointer&#45;events&#58; none</code> 을 적용시키면 pointer 이벤트가 발생되지 않는다&#46; 

<a id="1dbeda9b0fe1802da689d44a8b0a2a21"></a>

즉, mouseenter 이벤트가 무시 처리된다&#46; 

<a id="1dbeda9b0fe1804ab73be0381fdd0253"></a>

<br>따라서 위 화면과 같이 크기가 줄었다가 커졌다 하는 애니메이션 효과를  제거 가능하다&#46;
