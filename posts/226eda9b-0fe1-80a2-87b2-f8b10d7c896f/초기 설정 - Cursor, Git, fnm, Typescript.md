---
order: 8
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 226eda9b-0fe1-80a2-87b2-f8b10d7c896f
title: 초기 설정 - Cursor, Git, fnm, Typescript
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 226eda9b-0fe1-802b-a035-c3a886768c4d
    title: Nest.js
  - id: 226eda9b-0fe1-80c9-b906-d1c0ad48e506
    title: "[ 풀스택 ] 인프런 클론 코딩 Next.js ,  Nest.js ( Part1 )"
  - id: 226eda9b-0fe1-80a2-87b2-f8b10d7c896f
    title: 초기 설정 - Cursor, Git, fnm, Typescript
excerpt: 목차 - 1. Cusor - 2. fnm 설치 ( or Node 22버전 설치) - ✅ fnm 사용이 적절한 상황 - ❌ fnm 사용이 불필요한/부적절한 상황 - fnm(Fast Node Manager)을 사용한 설치 - Node 22 버전 직접설치 - 3. Pnpm 설치 - 4. Typescript 설치 1. Cusor
cover: 093076d5aa28ba27.webp
icon: ⚙
notionProperties: {}
schema_version: 1
parent_id: 226eda9b-0fe1-80c9-b906-d1c0ad48e506
created: 2025-07-04T02:46:02.648Z
updated: 2025-07-04T06:30:00.082Z
legacy_path: Main/Nest.js-c3a886768c4d/[ 풀스택 ] 인프런 클론 코딩 Next.js ,  Nest.js ( Part1 -d1c0ad48e506/초기 설정 - Cursor, Git, fnm, Typescript-f8b10d7c896f/index.md
legacy_category: Nest.js
source_url: https://beautiful-college-c84.notion.site/226eda9b0fe180a287b2f8b10d7c896f
---
> 
> 
> <a id="226eda9b0fe1802aa6e7db0589dca05b"></a>
> 
> 목차
> 
> - [1. Cusor](#226eda9b0fe1801a99fede7fea7f2b72)
> - [2. fnm 설치 ( or Node 22버전 설치)](#226eda9b0fe180759132e3c3f8b6afa6)
> - [✅ fnm 사용이 적절한 상황](#226eda9b0fe1800c9827c5b8eea7a6c8)
> - [❌ fnm 사용이 불필요한/부적절한 상황](#226eda9b0fe1806a81c4f4d10fad6cf3)
> - [fnm(Fast Node Manager)을 사용한 설치](#226eda9b0fe180cebe3dd576416a6b8c)
> - [Node 22 버전 직접설치](#226eda9b0fe180559dffe64dea3bd93b)
> - [3. Pnpm 설치](#226eda9b0fe180c69180f8caabd9cc86)
> - [4. Typescript 설치](#226eda9b0fe18078b989d8a4c3dcfd86)

<a id="226eda9b0fe1801a99fede7fea7f2b72"></a>

## 1&#46; Cusor

[Cursor &#45; The AI Code Editor]()

> 
> 
> <a id="226eda9b0fe180c0b440db74ced4a515"></a>
> 
> 유료버전 결제 권장

- <code>Prettier 포맷터</code> 플러그인

- <code>TailwindCSS</code> 플러그인

<details>
<summary>rule 설정</summary>

<a id="226eda9b0fe18028a4fbc699337e6e3d"></a>

```typescript
[Rules prompt]
you are an expert AI programming assistant in VSCode that primarily focuses on producing clear, readable code.  
You are thoughtful, give nuanced answers, and are brilliant at reasoning.  
You carefully provide accurate, factual, and thoughtful answers, and you are a genius at reasoning.

1. Follow the user's requirements carefully and precisely.
2. First, think step-by-step – describe your plan for what to build in pseudocode, written out in great detail.
3. Confirm, then write the code!
4. Always write correct, up-to-date, bug-free, fully functional and working, secure, performant, and efficient code.
5. Focus on **readability** over performance.
6. Fully implement all requested functionality.
7. Leave **NO** to-dos, placeholders, or missing pieces.
8. Ensure the code is complete! Thoroughly verify the final version.
9. Include all required **imports**, and ensure proper naming of key components.
10. Be concise. Minimize any unnecessary explanations.
11. If you think there might not be a correct answer, say so. If you do not know the answer, admit it instead of guessing.
12. Always provide concise answers.
13. Please answer in Korean

```

</details>

<a id="226eda9b0fe18046bfefdd03f7445061"></a>

<br>

<a id="226eda9b0fe180759132e3c3f8b6afa6"></a>

## 2&#46; fnm 설치 ( or <code>Node 22</code>버전 설치)

<details>
<summary>🧐 왜 <code>fnm</code>을 사용하는가?</summary>

> ✏️ 
> 
> <a id="226eda9b0fe180818312e443fcf3346a"></a>
> 
> <code>fnm</code> 과 <code>npm</code>은 용도가 다르다&#46;
> 
> | <strong>항목</strong> | <code>fnm</code> | <code>npm</code> |
> | --- | --- | --- |
> | 의미 | Fast Node Manager | Node Package Manager |
> | 역할 | Node&#46;js 버전 관리 도구 | Node&#46;js 패키지 관리 도구 |
> | 사용 목적 | 여러 버전의 Node&#46;js를 쉽게 설치/전환 | 패키지 설치, 실행, 빌드 등 |
> | 명령어 예 | fnm install 18 /<br> fnm use 20 | npm install axios / npm run build<br> |
> 
> - <code>fnm</code>은 <strong>Node&#46;js </strong><strong><u>버전 관리 도구</u></strong>
> 
> - <code>npm</code>은 <strong>Node&#46;js 환경에서의 </strong><strong><u>패키지 관리 도구</u></strong>

> 
> 
> <a id="226eda9b0fe18038a553e0efaec2c084"></a>
> 
> <strong>npm의 장점</strong>
> 
> 1. <strong>속도</strong>
>     - fnm은 Rust로 작성되어 매우 빠름
> 
>     -  nvm보다 설치/전환 속도가 빠름
> 
> 1. <strong>편리한 설정</strong>
>     <a id="226eda9b0fe18062b13fefe42a9c1665"></a>
> 
>     <code>&#46;node&#45;version</code>, <code>&#46;nvmrc</code> 등을 자동 인식하여 프로젝트별 버전 적용 가능
> 
> 1. <strong>lightweight</strong>
>     <a id="226eda9b0fe180699f45e04fecbb73b0"></a>
> 
>     글로벌 설치가 아닌 사용자 홈 디렉토리 내에서 관리됨

<a id="226eda9b0fe1800c9827c5b8eea7a6c8"></a>

### ✅ <code>fnm</code> 사용이 적절한 상황

<a id="226eda9b0fe180a19de9e865f3400fe5"></a>

<code>fnm</code> (Fast Node Manager)은 <strong>“Node&#46;js 버전 관리 도구”이다&#46;</strong>

<a id="226eda9b0fe180b5ba06f1bdf3bab090"></a>

즉, <strong><u>Node&#46;js 자체를 여러 버전으로 전환</u></strong><strong>하거나 </strong><strong><u>프로젝트별로 다르게 쓸 때</u></strong><strong> </strong>사용하는 것이 적절하다&#46;

- <strong>프로젝트마다 다른 Node&#46;js 버전을 써야 할 때</strong>

- <strong>&#46;node&#45;version 또는 &#46;nvmrc 파일로 자동 전환하고 싶을 때</strong>
    - nvm보다 빠르고 경량이라 실무에서도 많이 선호된다&#46;

- <strong>CI/CD, 도커 환경 외 로컬 개발에서 유연하게 사용하고 싶을 때</strong>

- <strong>nvm보다 빠른 성능을 원할 때 (Rust 기반)</strong>

<a id="226eda9b0fe1806a81c4f4d10fad6cf3"></a>

### <strong>❌ </strong><strong><code>fnm</code></strong><strong> 사용이 불필요한/부적절한 상황</strong>

- Node 버전이 하나로 고정된 단일 프로젝트
    - 굳이 관리 도구를 쓸 필요 없dm

- 이미 다른 Node 버전 매니저(nvm, volta 등) 사용 중
    - 중복되므로 충돌 가능

- Docker 컨테이너에서 Node 버전 고정 사용
    - 컨테이너 이미지로 해결 가능하므로 굳이 필요 없음

- CI/CD 환경에서 버전 명시된 이미지 사용 중
    - &#46;nvmrc보다는 Dockerfile 내 버전 명시가 일반적

</details>

<a id="226eda9b0fe180cebe3dd576416a6b8c"></a>

### <code>fnm(Fast Node Manager)</code>을 사용한 설치

[fnm](https://github.com/Schniz/fnm)

[Node&#46;js — Download Node&#46;js®]()

<a id="226eda9b0fe18013887bd0c2b7e1986c"></a>

```bash
# 1. fnm 다운로드
curl -o- https://fnm.vercel.app/install | bash

# 2. node 22 버전 설치
fnm install 22

# 2.2 node 기본 버전 선택 ( 옵션 ) 
npm default 22

# 3. 노드 설치 버전 확인
node -v

# 4. npm 설치 버전 확인
npm -v
```

<details>
<summary>1&#46; fnm env 설정이 쉘에 반영 됐는지 확인</summary>

> 
> 
> <a id="226eda9b0fe1800a98b5f24f9e3d51ef"></a>
> 
> <code>fnm</code>은 환경 변수를 직접 쉘에 등록해줘야 node, npm, npx 등을 인식한다&#46;

<a id="226eda9b0fe1805fa5d2e610c69f3fda"></a>

```bash
# node 22 설치 
fnm install 22 

# node 확인 -> 결과 X
node -v

# fnm 설정 쉘에 반영
eval "$(fnm env)"
```

<details>
<summary>자동 적용 &#45; &#126;/zshrc에 위 설정 추가하기</summary>

<a id="226eda9b0fe180b690ccf1fe032a2bf4"></a>

```bash
eval "$(fnm env)"

source ~/.zshrc
```

</details>

</details>

<details>
<summary>2&#46; node가 fnm에서 관리되고 있는지 확인</summary>

<a id="226eda9b0fe18085ada7c17b99026088"></a>

```bash
fnm list
# * v22.17.0

# 위 출력값이 아닌 경우
fnm use 22
```

</details>

<a id="226eda9b0fe180559dffe64dea3bd93b"></a>

### <code>Node 22</code> 버전 직접설치

[Node&#46;js — Download Node&#46;js®]()

<a id="226eda9b0fe180c69180f8caabd9cc86"></a>

## 3&#46; Pnpm 설치

> ✏️ 
> 
> <a id="226eda9b0fe180a296f1cc1d5a83f076"></a>
> 
> <code>pnpm</code>은 <code>npm</code>과 <code>yarn</code>에 이은 <strong>차세대 Node&#46;js 패키지 매니저이다&#46;</strong>
> 
> - 단순히 “더 빠르다”는 주장만이 아니라, <strong><u>구조적으로 훨씬 효율적인 의존성 관리 방식</u></strong>을 가지고 있어 실무에서도 점점 채택되고 있다&#46;
> 
> <details>
> <summary><strong>🧐 왜 pnpm을 사용하는가?</strong></summary>
> 
> | <strong>항목</strong> | pnpm<strong>의 특징</strong> | <strong>실무적 이점</strong> |
> | --- | --- | --- |
> | <strong>하드링크 기반 저장소</strong> | 전역 캐시 → 하드링크로 연결 | 디스크 공간 최소화 |
> | <strong>매우 빠른 설치 속도</strong> | 설치 시 병렬 &#43; 캐시 재활용 | npm보다 최대 3배 빠름 |
> | <strong>엄격한 의존성 격리</strong> | node&#95;modules에 flat하게 안 깔림 | 숨겨진 의존성 문제 방지 |
> | <strong>작은 node&#95;modules 구조</strong> | symlink/hardlink 기반 | du &#45;sh node&#95;modules 작아짐 |
> | <strong>Monorepo 친화적</strong> | 기본적으로 workspaces 내장 | Lerna, Turbo 없이도 다중 패키지 관리 가능 |
> | <strong>npm 완전 호환</strong> | package&#46;json, lockfile 모두 호환 | 이관 시 부담 없음 |
> 
> </details>

<a id="226eda9b0fe18008a522eb01d1f1c897"></a>

```bash
# pnpm 설치
curl -fsSL https://get.pnpm.io/install.sh | sh -

# 변경된 환경변수 경로 적용 - pnpm 호출 가능
source /Users/igyeongseob/.zshrc

# 설치 확인
pnpm -v
```

[Installation &#124; pnpm]()

<a id="226eda9b0fe18078b989d8a4c3dcfd86"></a>

## 4&#46; Typescript 설치

<a id="226eda9b0fe18053bf8ded79289a4b05"></a>

```bash
npm i -g typescript
```
