---
order: 0
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1d4eda9b-0fe1-80a2-95f7-e975482b1dcd
title: React + GSAP
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-819c-beab-c6a3a1072bb9
    title: 리액트
  - id: 1d4eda9b-0fe1-80a2-95f7-e975482b1dcd
    title: React + GSAP
excerpt: "/icons/tagblue.svg [유데미] 실전 GSAP의 scrollTrigger를 활용한 웹사이트제작 - 기간 - HTML, CSS, JS: 25.04.13(일) ~ 25.04.23(수) - React, tailwind CSS: reference - ‣ - ‣ - ‣ - ‣ - ‣ - 페이지 - 페이지 - ‣ - ‣"
cover: ee7da0b7cbb72014.webp
icon: ddc677e05c9e7c74.webp
notionProperties: {}
schema_version: 1
parent_id: 1c3eda9b-0fe1-819c-beab-c6a3a1072bb9
created: 2025-04-13T04:29:44.927Z
updated: 2025-04-23T05:44:05.070Z
legacy_path: Main/리액트-c6a3a1072bb9/React + GSAP-e975482b1dcd/index.md
legacy_category: 리액트
source_url: https://beautiful-college-c84.notion.site/1d4eda9b0fe180a295f7e975482b1dcd
---
> /icons/tag_blue.svg 
> 
> <a id="1d4eda9b0fe18126bf0af7661f545f95"></a>
> 
> &#91;유데미&#93; <strong>실전 GSAP의 scrollTrigger를 활용한 웹사이트제작</strong>
> 
> - 기간
>     - HTML, CSS, JS&#58; 25&#46;04&#46;13(일) &#126; 25&#46;04&#46;23(수)
> 
>     - React, tailwind CSS&#58; 
> 
> <details>
> <summary>reference</summary>
> 
> - ‣
> 
> - ‣
> 
> - ‣
> 
> - ‣
> 
> - ‣
> 
> - <a href="https://beautiful-college-c84.notion.site/b740f67be6034edcaf3b586e5bc289d6">페이지</a> 
> 
> - <a href="https://beautiful-college-c84.notion.site/2a0b234b0ae140eab448c74bf43b0480">페이지</a> 
> 
> - ‣
> 
> - ‣
> 
> </details>

<a id="1d4eda9b0fe18185b3cef2dc30915a8e"></a>

## Github

[gsap_prac-raw-](https://github.com/gyungsubLee/gsap_prac-raw-)

[gsap_prac](https://github.com/gyungsubLee/gsap_prac)

<a id="1daeda9b0fe180a8a079fa710b48b41a"></a>

todo

- overflow&#58; hidden

- 흐리게 보이는 효과 blur
    - backdrop&#45;filter&#58; blur(30px)

<a id="1daeda9b0fe1805d9a14cc5bce392315"></a>

padding을 주면, box&#45;size&#58; border&#45;box를 줘야한다&#46;

<details>
<summary>기본 CSS 설정</summary>

<a id="1d4eda9b0fe1804c9aaacfff04ce30c1"></a>

```css
@charset "utf-8";

/* 00. font - 구글폰트에서 Montserrat 300/400/600 가져옴 */
@import url('https://fonts.googleapis.com/css2?family=Montserrat:wght@300;500;600&family=Noto+Sans+KR&display=swap');
@import url('https://fonts.googleapis.com/css2?family=Raleway:wght@300;500;600&display=swap');

/* 00. Reset */
* {margin: 0;padding: 0;}
html, body, div, span, applet, object, iframe, h1, h2, h3, h4, h5, h6, p, blockquote, pre, a, abbr, acronym, address, big, cite, code, del, dfn, em, font, img, ins, kbd, q, s, samp, small, strike, strong, sub, sup, tt, var, b, u, i, center, dl, dt, dd, ol, ul, li, fieldset, form, label, legend, table, tbody, tfoot, thead, tr, th, td{margin:0;padding:0;}
a {color: inherit; text-decoration: inherit;}
li {list-style: none;}
address, em, i {font-style: normal;}
button {background: none; border: none;}
img {vertical-align: middle;}
```

</details>

<a id="1d4eda9b0fe1815787addf6873b36953"></a>

## CSS

[display](#/post/1d5eda9b-0fe1-8019-9bc3-c2e76a99637d)

[FlexBox [ Flex ]](#/post/1daeda9b-0fe1-804a-b016-d480357eda0c)

[flex-wrap: wrap](#/post/1d8eda9b-0fe1-8090-9692-c55e4d7a78a9)

[flex-grow](#/post/1d9eda9b-0fe1-8081-a5ea-ee74697a20e0)

[요소 정중앙 정렬](#/post/1d9eda9b-0fe1-80b8-a5b1-c8d9bcdb9b6f)

[Grid Box [ Grid ]](#/post/1d4eda9b-0fe1-8088-aeea-f33866227915)

[align-items  vs align-self](#/post/1d8eda9b-0fe1-80cb-a63d-d0421ff49e36)

[grid-colums](#/post/1d8eda9b-0fe1-8039-8951-ee1fbb838d7d)

[place-items](#/post/1d8eda9b-0fe1-802c-8191-ff1a66f62f42)

[아이템(sell) 가로, 세로 정렬: justify-self, align-self](#/post/1d8eda9b-0fe1-80d6-8f2b-de7a2230682f)

[position](#/post/1d5eda9b-0fe1-80f8-a2a1-d8f74dec1bee)

[position: fixed](#/post/1d4eda9b-0fe1-8046-a36f-f27dd518f1b3)

[position: sticky](#/post/1d5eda9b-0fe1-8077-9786-db7fc22a1fd6)

[position: absolute](#/post/1d9eda9b-0fe1-80bc-9cfe-eff1184902c2)

[요소 중앙 정렬](#/post/1d5eda9b-0fe1-805f-9f92-e3d4e66a5cab)

[overflow](#/post/1d5eda9b-0fe1-8018-90ce-f5d98ab97241)

[원근감: perspective](#/post/1d8eda9b-0fe1-80da-98e5-e4ee0a426af2)

[흐리게 보이는 효과: blur](#/post/1d5eda9b-0fe1-8010-b71e-e5149455d84d)

[filter:brightness()](#/post/1d8eda9b-0fe1-803d-9fd3-f075d41b4acd)

[text-transform: text 대문사, 소문자 변경](#/post/1d9eda9b-0fe1-807a-9113-e1ca46846ad9)

[cursor: pointer](#/post/1d9eda9b-0fe1-801a-9129-e54d7e9214d0)

[data-color](#/post/1d8eda9b-0fe1-80e4-966f-cf0065e3251f)

[rem ( root em )](#/post/1dbeda9b-0fe1-8024-ad2e-e49032bfda79)

[vw, vh, %](#/post/1dbeda9b-0fe1-808d-a449-e3bc5990fb11)

[box-size: border-box](#/post/1d5eda9b-0fe1-8086-b570-e908ae9303fd)

[tailwind css](#/post/1d4eda9b-0fe1-8155-9a14-cc9d0636bb88)

[CSS 적용 X: 세미콜론(;) 문법 오류](#/post/1d5eda9b-0fe1-80f4-90c6-f813dfa7252b)

[CSS 트랜지션을 무효화](#/post/1d5eda9b-0fe1-802c-b433-e021360a7a0c)

[grid에서는 align-self ❌](#/post/1d8eda9b-0fe1-8042-bda2-d36ea6ba6795)

[Transfrom 적용 시 block 지정 필요](#/post/1daeda9b-0fe1-806e-96e9-f1a8e208afa2)

[z-index 적용한됨](#/post/1dceda9b-0fe1-80d4-80ac-ee6d24a0638c)

<a id="1d5eda9b0fe18009a21ae40b53220277"></a>

## DOM

[Header](#/post/1d5eda9b-0fe1-816f-989c-e8b7e71afe38)

[Visual](#/post/1daeda9b-0fe1-8079-99ff-c29182ebb50f)

[Content 1](#/post/1d7eda9b-0fe1-808f-bd51-dba77048e5de)

[Content 2](#/post/1d8eda9b-0fe1-8022-9e12-d9545ebd4829)

[Content 3](#/post/1d8eda9b-0fe1-8069-b924-f47d9bc5d344)

[Conetent 4](#/post/1d8eda9b-0fe1-80e9-9a80-c5c5bbb7b72f)

[Content 5](#/post/1d9eda9b-0fe1-807e-9793-c4ff1b271f96)

[Content 6](#/post/1daeda9b-0fe1-8016-8672-f5be693c0e11)

[Footer](#/post/1daeda9b-0fe1-80e4-a19f-fd7ad0c17248)

[GSAP](#/post/1daeda9b-0fe1-8046-8ae7-c61b4502f959)

[흰색 배경일 경우, 동적으로 header color 변경하기](#/post/1d9eda9b-0fe1-800d-b615-df7ed4803957)

[제목 없음](#/post/1daeda9b-0fe1-80af-b21e-cb5145df9010)

<a id="1daeda9b0fe180dca6d8ccc862f87159"></a>

## GSAP &#45; interactive 애니메이션 효과

[clientX, offsetX, pageX, screenX의 차이](#/post/1daeda9b-0fe1-8054-a82c-ced8855d6833)

[setTimeout](#/post/1daeda9b-0fe1-803c-a498-dba169b09456)

[classList](#/post/1daeda9b-0fe1-8064-bec6-c0d7c7a05f96)

[DOM 요소 제어](#/post/1daeda9b-0fe1-8034-a000-e51b39785faa)

[ES6 텀플릿 리터널 방식 ( 문장을 ``베틱으로 감쌈 )](#/post/1daeda9b-0fe1-803c-a37b-e6ed5b3689ad)

[0. GSAP, ScrollTrigger 라이브러리 추가](#/post/1daeda9b-0fe1-8048-b4ea-c5d1ae48b2db)

[1. [ visual 영역 ] 로고 애니메이션](#/post/1daeda9b-0fe1-81dd-a7f4-d9dda75608b2)

[ScrollTrigger - markers: true](#/post/1daeda9b-0fe1-80f5-93f3-d8256752cf15)

[2. [ MainText 영역 ] 애니메이션](#/post/1daeda9b-0fe1-80c4-8623-df2d84305d9f)

[3.  [ SubText 영역 ] 애니메이션](#/post/1daeda9b-0fe1-80bf-b787-de25b3a6ee81)

[4. [ TextAni ] 텍스트 변경 애니메이션](#/post/1daeda9b-0fe1-800b-96c3-fc454d80abff)

[5. [ cardBox ] z축(원근감) 애니메이션](#/post/1daeda9b-0fe1-80cb-8966-e7fde551b29a)

[6. [ con3 listBox ] box 애니메이션](#/post/1daeda9b-0fe1-8098-976d-cfc0ab28523c)

[7. [ con5 listbox ] li hover 시 이미지 보이게하는 애니메이션](#/post/1dbeda9b-0fe1-805c-b38b-d73a8a5c85f1)

[8. [ footer ] 로고, 텍스트 애니메이션](#/post/1deeda9b-0fe1-8032-8a9c-c5f850c0974d)

[9. [ Loading ] 로딩 애니메이션](#/post/1deeda9b-0fe1-80e2-b9b0-c5f3b1a11630)

[10. [ 상단 메뉴바 ] 흰 배경에서 색상 변경](#/post/1deeda9b-0fe1-80f6-9191-ecabe3144bf1)

[gsap.utils.toArray()](#/post/1daeda9b-0fe1-80ec-8c6e-dfdd1ace87ec)

[ScrollTrigger.create()](#/post/1dbeda9b-0fe1-8009-9755-f6379767a452)

[gsap.set(selector, {…})](#/post/1dbeda9b-0fe1-80d7-af68-f15d86c4962c)

[ScrollTrigger 이벤트 종류: onEnter …](#/post/1dbeda9b-0fe1-80bf-aba4-ec06c632e1ca)

[gsap.timeline(),  ScrollTiger.create() 비교](#/post/1dbeda9b-0fe1-8068-bf8c-ced5b7c2a060)

[li hover 애니메이션에서 imgBox hover 시 mouseleave로 인식](#/post/1dbeda9b-0fe1-8070-bfa3-e8559f54cafb)

[content 5 listbox 이미지 모션 부드럽게 변경](#/post/1dceda9b-0fe1-8057-b712-f7231810909e)
