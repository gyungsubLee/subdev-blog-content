---
order: 37
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1d9eda9b-0fe1-800d-b615-df7ed4803957
title: 흰색 배경일 경우, 동적으로 header color 변경하기
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-819c-beab-c6a3a1072bb9
    title: 리액트
  - id: 1d4eda9b-0fe1-80a2-95f7-e975482b1dcd
    title: React + GSAP
  - id: 1d9eda9b-0fe1-800d-b615-df7ed4803957
    title: 흰색 배경일 경우, 동적으로 header color 변경하기
excerpt: 흰색 배경에 id 값을 주고, scroll 이벤트로 해당 섹션에 진입하는 순간 변경 예시 tailwind CSS javascript 나는 헤더야 javascript const header = document.getElementById('header'); const whiteSection = document.getEleme
cover: null
icon: null
notionProperties:
  Tags: 추가
schema_version: 1
parent_id: 1d4eda9b-0fe1-80a2-95f7-e975482b1dcd
created: 2025-04-18T05:51:05.658Z
updated: 2025-04-19T03:07:31.334Z
legacy_path: Main/리액트-c6a3a1072bb9/React + GSAP-e975482b1dcd/흰색 배경일 경우, 동적으로 header color 변경하기-df7ed4803957/index.md
legacy_category: 리액트
source_url: https://beautiful-college-c84.notion.site/1d9eda9b0fe1800db615df7ed4803957
---
<a id="1d9eda9b0fe1808f93fac5f086d1ecf9"></a>

흰색 배경에 id 값을 주고, scroll 이벤트로 해당 섹션에 진입하는 순간 변경

<a id="1d9eda9b0fe180b2b4ccf5f6b894c205"></a>

예시

<a id="1d9eda9b0fe1805f8dfce84dc65e8cf8"></a>

<strong>tailwind CSS</strong>

<a id="1d9eda9b0fe18082a10df45b6a2eb511"></a>

```javascript
<header id="header" class="fixed w-full p-4 text-white transition-colors duration-300">
  나는 헤더야
</header>

<main>
  <section class="h-[100vh] bg-black"></section>
  <section id="white-section" class="h-[100vh] bg-white"></section>
  <section class="h-[100vh] bg-gray-500"></section>
</main>
```

<a id="1d9eda9b0fe18031ac62e16b48c048c8"></a>

```javascript
const header = document.getElementById('header');
const whiteSection = document.getElementById('white-section');

window.addEventListener('scroll', () => {
  const sectionTop = whiteSection.offsetTop;
  const sectionHeight = whiteSection.offsetHeight;
  const scrollY = window.scrollY;

  if (scrollY >= sectionTop && scrollY < sectionTop + sectionHeight) {
    // 스크롤 위치가 흰색 섹션 안이면
    header.classList.add('text-black');
    header.classList.remove('text-white');
  } else {
    // 흰색 섹션 밖이면
    header.classList.add('text-white');
    header.classList.remove('text-black');
  }
});
```
