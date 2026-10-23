---
order: 66
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1d4eda9b-0fe1-8155-9a14-cc9d0636bb88
title: tailwind css
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-819c-beab-c6a3a1072bb9
    title: 리액트
  - id: 1d4eda9b-0fe1-80a2-95f7-e975482b1dcd
    title: React + GSAP
  - id: 1d4eda9b-0fe1-8155-9a14-cc9d0636bb88
    title: tailwind css
excerpt: "✏️ - 최신 버전보다는 안정화된 버전 설치하는 것이 중요 - 25.04.13 기준 vite: 5.2.10 bash npm install -D vite@5.2.10 tailwindcss: 3.4.1 bash 이전 설치 내역 삭제 ( 캐시까지 ) npm uninstall tailwindcss rm -rf nodemodule"
cover: null
icon: null
notionProperties:
  Tags: 🧐 질문,복습,tailwind css
  상태: 완료
schema_version: 1
parent_id: 1d4eda9b-0fe1-80a2-95f7-e975482b1dcd
created: 2025-04-13T04:29:44.927Z
updated: 2025-04-13T05:35:48.986Z
legacy_path: Main/리액트-c6a3a1072bb9/React + GSAP-e975482b1dcd/tailwind css-cc9d0636bb88/index.md
legacy_category: 리액트
source_url: https://beautiful-college-c84.notion.site/1d4eda9b0fe181559a14cc9d0636bb88
---
> ✏️ 
> 
> - 최신 버전보다는 안정화된 버전 설치하는 것이 중요
> 
> - 25&#46;04&#46;13 기준
>     <details>
>     <summary><code>vite</code>&#58; 5&#46;2&#46;10</summary>
> 
>     <a id="1d4eda9b0fe180848377f4bfa51d4903"></a>
> 
>     ```bash
>     npm install -D vite@5.2.10
>     ```
> 
>     </details>
> 
>     <details>
>     <summary><code>tailwindcss</code>&#58; 3&#46;4&#46;1</summary>
> 
>     <a id="1d4eda9b0fe180b1ae78dff019bb79d0"></a>
> 
>     ```bash
>     # 이전 설치 내역 삭제 ( 캐시까지 )
>     npm uninstall tailwindcss
>     rm -rf node_modules
>     rm package-lock.json
>     npm cache clean --force
> 
>     # 재설치 (안정 버전 명시)
>     npm install -D tailwindcss@3.4.1 postcss autoprefixer
> 
>     # 설치 확인: tailwindcss 폴더가 있으면 정상 설치
>     ls node_modules/.bin
>     ```
> 
>     </details>
> 
> | <strong>파일명</strong> | <strong>역할</strong> |
> | --- | --- |
> | <code>vite&#46;config&#46;js</code> | React 플러그인 등록만 (Tailwind는 여기에 안 넣음) |
> | <code>tailwind&#46;config&#46;js</code> | Tailwind content 경로, 확장 설정 |
> | <code>postcss&#46;config&#46;js</code> | Tailwind &#43; Autoprefixer 적용 |
> | <code>index&#46;css</code> | &#64;tailwind base; 등 지시어 넣는 곳 |

<a id="1d4eda9b0fe180a9bd47d332c4d7b344"></a>

### <strong>✅ 1&#46; Tailwind CSS 설치 방법 (Vite &#43; React 기준)</strong>

---

<details>
<summary><strong>1&#46; 패키지 설치</strong></summary>

<a id="1d4eda9b0fe180c6a08adec1a4a81a5b"></a>

```bash
# Tailwind 관련 패키지 설치
npm install -D tailwindcss postcss autoprefixer

# 설정 파일 생성: tailwind.config.js, postcss.config.js
npx tailwindcss init -p
```

- tailwindcss&#58; 유틸리티 클래스 제공

- postcss, autoprefixer&#58; 브라우저 호환성 자동 처리

- tailwindcss init &#45;p&#58; 설정 파일 두 개 생성
    - tailwind&#46;config&#46;js

    - postcss&#46;config&#46;js

</details>

<details>
<summary><strong>2&#46; tailwind&#46;config&#46;js 설정</strong></summary>

> ✏️ 
> 
> <a id="1d4eda9b0fe180b791a7e34b35d75a84"></a>
> 
> content 경로 설정 추성

<a id="1d4eda9b0fe18085bec9e11887392ff9"></a>

```javascript
// tailwind.config.js
export default {
  content: [
    "./index.html",
    "./src/**/*.{js,ts,jsx,tsx}",
  ],
  theme: {
    extend: {},
  },
  plugins: [],
};
```

</details>

<details>
<summary><strong>3&#46; CSS 파일에 Tailwind 지시어 추가</strong></summary>

> src/index&#46;css 또는 src/main&#46;css에 아래 내용 작성

<a id="1d4eda9b0fe1804c927ee7c106bfe8e5"></a>

```css
@tailwind base;
@tailwind components;
@tailwind utilities;
```

</details>

<details>
<summary><strong>4&#46; 엔트리 포인트(main&#46;jsx 등)에서 CSS 불러오기</strong></summary>

<a id="1d4eda9b0fe1803c91e0dbded6432a37"></a>

```javascript
import './index.css'; // 또는 main.css
```

</details>

<a id="1d4eda9b0fe1801b92c1e3e38f9d08dd"></a>

### <strong>✅ 2&#46; Tailwind 자주 쓰는 유틸리티 정리</strong>

---

| <strong>목적</strong> | <strong>유틸리티 클래스</strong> |
| --- | --- |
| 배경색 | bg&#45;red&#45;500, bg&#45;gray&#45;800 |
| 글자색 | text&#45;white, text&#45;gray&#45;700 |
| 패딩 | p&#45;4, px&#45;2, py&#45;3, pt&#45;2, pl&#45;1 |
| 마진 | m&#45;4, mt&#45;2, ml&#45;3, mx&#45;2 |
| 폰트 크기 | text&#45;sm, text&#45;lg, text&#45;xl, text&#45;2xl |
| 폰트 굵기 | font&#45;bold, font&#45;semibold |
| 박스 그림자 | shadow, shadow&#45;md, shadow&#45;lg |
| 둥근 테두리 | rounded, rounded&#45;md, rounded&#45;full |
| 플렉스박스 | flex, items&#45;center, justify&#45;between |
| 그리드 | grid, grid&#45;cols&#45;3, gap&#45;4 |
| 버튼 효과 | hover&#58;bg&#45;blue&#45;600, transition, duration&#45;300 |

<a id="1d4eda9b0fe18044aba0e44086097462"></a>

### <strong>✅ 3&#46; 반응형 스타일링 (sm&#58;, md&#58;, lg&#58; 등)</strong>

---

> ✏️ 
> 
> <a id="1d4eda9b0fe1803e9493f813b2ab7ad2"></a>
> 
> Tailwind는 <strong>모바일 우선 방식</strong>(Mobile First)을 따른다&#46; 
> 
> <a id="1d4eda9b0fe180fe9310c12a9799219b"></a>
> 
> 즉, 작은 화면 먼저 스타일을 주고, 큰 화면에서 덮어씌운다&#46;

| <strong>브레이크포인트</strong> | <strong>설명</strong> | <strong>가로 해상도</strong> |
| --- | --- | --- |
| <code>sm&#58;</code> | Small | 640px 이상 |
| <code>md&#58;</code> | Medium | 768px 이상 |
| <code>lg&#58;</code> | Large | 1024px 이상 |
| <code>xl&#58;</code> | Extra Large | 1280px 이상 |
| <code>2xl&#58;</code> | 2x Extra Large | 1536px |

<details>
<summary>ex) 반응형 box</summary>

<a id="1d4eda9b0fe18058a0a6dc68931b270f"></a>

```javascript
<div className="text-sm md:text-lg lg:text-xl">
  반응형 텍스트
</div>
```

- 기본&#58; text&#45;sm (모바일)

- 768px 이상&#58; text&#45;lg

- 1024px 이상&#58; text&#45;xl

</details>

<details>
<summary>ex) 반응형 button</summary>

<a id="1d4eda9b0fe180968173d4aebca3927a"></a>

```javascript
<button className="bg-blue-500 hover:bg-blue-700 text-white px-4 py-2 rounded 
                   text-sm sm:text-base md:text-lg">
  버튼
</button>
```

</details>

<a id="1d4eda9b0fe180a4ad42d6e0c0c83d17"></a>

### <strong>✅ 이미 Vite 환경에 Tailwind 설치할 때 체크리스트</strong>

---

<details>
<summary><strong> 1&#46; 중복 postcss&#46;config&#46;js 또는 tailwind&#46;config&#46;js 확인</strong></summary>

> ✏️ 
> 
> <a id="1d4eda9b0fe1805da82de75ee29f5afb"></a>
> 
> vite 프로젝트에는 postcss&#46;config&#46;js, tailwind&#46;config&#46;js 파일이 하나만 존재해야 한다&#46; 
> 
> - 예전 설정이 있다면 <strong>병합하거나 삭제</strong> 후 다시 설정 필요

<a id="1d4eda9b0fe180b4a9cdfbbfbaa0292f"></a>

```javascript
# 혹시 예전 설정이 있다면
rm -f tailwind.config.js postcss.config.js
npx tailwindcss init -p
```

</details>

<details>
<summary><strong> 2&#46; Vite 플러그인 설정은 그대로</strong></summary>

> ✏️ 
> 
> <a id="1d4eda9b0fe180a7a289f4dbebe5f0fc"></a>
> 
> Tailwind는 Vite에서 별도 플러그인을 설치하지 않아도 동작한다&#46;
> 
> <a id="1d4eda9b0fe1802f9572c2d05fe27fc3"></a>
> 
> 즉, <code>vite&#46;config&#46;js</code>에 아래처럼 <strong>별도 설정이 없어도 된다&#46;</strong>
> 
> - Tailwind 관련 설정은 vite&#46;config&#46;js가 아니라 <strong><code>tailwind&#46;config&#46;js</code></strong><strong>와 </strong><strong><code>postcss&#46;config&#46;js</code></strong> 안에만 들어가면 된다&#46;

<a id="1d4eda9b0fe180e38ff1dba03ab52104"></a>

```javascript
// vite.config.js
import { defineConfig } from 'vite'
import react from '@vitejs/plugin-react'

export default defineConfig({
  plugins: [react()],
})
```

</details>

<details>
<summary><strong>3&#46; tailwindcss, postcss, autoprefixer 설치 확인</strong></summary>

<a id="1d4eda9b0fe180ff91bbc006e7a2a5c5"></a>

```bash
npm list -D tailwindcss postcss autoprefixer

# 결과 예시 
├── tailwindcss@3.4.1
├── postcss@8.4.31
└── autoprefixer@10.4.16
```

</details>
