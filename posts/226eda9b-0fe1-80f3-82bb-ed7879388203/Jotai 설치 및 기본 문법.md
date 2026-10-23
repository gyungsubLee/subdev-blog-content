---
order: 5
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 226eda9b-0fe1-80f3-82bb-ed7879388203
title: Jotai 설치 및 기본 문법
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 226eda9b-0fe1-802b-a035-c3a886768c4d
    title: Nest.js
  - id: 226eda9b-0fe1-80c9-b906-d1c0ad48e506
    title: "[ 풀스택 ] 인프런 클론 코딩 Next.js ,  Nest.js ( Part1 )"
  - id: 226eda9b-0fe1-80f3-82bb-ed7879388203
    title: Jotai 설치 및 기본 문법
excerpt: Reference inflearn-jotai-tutorial [atom — Jotai, primitive and flexible state management for React]() [Resettable — Jotai, primitive and flexible state management for React]() [jot
cover: fb3b1ee7da4a15e0.webp
icon: 9bed2eae1e079b4b.avif
notionProperties: {}
schema_version: 1
parent_id: 226eda9b-0fe1-80c9-b906-d1c0ad48e506
created: 2025-07-04T07:53:43.994Z
updated: 2025-07-04T08:57:00.385Z
legacy_path: Main/Nest.js-c3a886768c4d/[ 풀스택 ] 인프런 클론 코딩 Next.js ,  Nest.js ( Part1 -d1c0ad48e506/Jotai 설치 및 기본 문법-ed7879388203/index.md
legacy_category: Nest.js
source_url: https://beautiful-college-c84.notion.site/226eda9b0fe180f382bbed7879388203
---
<details>
<summary><strong>Reference</strong></summary>

[inflearn-jotai-tutorial](https://github.com/lopun-lecture/inflearn-jotai-tutorial)

[atom — Jotai, primitive and flexible state management for React]()

[Resettable — Jotai, primitive and flexible state management for React]()

[jotai/examples at main · pmndrs/jotai]()

</details>

> 
> 
> <a id="226eda9b0fe181e4a7d4d576e029cbbc"></a>
> 
> <strong>목차</strong>
> 
> - [1. Jotai](#226eda9b0fe181afbfbac18b9f8d12d9)
> - [[ 실습 ] jotai 사용](#226eda9b0fe180519cdac28539843032)
> - [1. Jotai + Next.js  기본 설정](#226eda9b0fe180f3843dc91b52d8eb0c)
> - [2. 기본 사용법](#226eda9b0fe180d7bb65d9ad5480d9d1)

<a id="226eda9b0fe181afbfbac18b9f8d12d9"></a>

## 1&#46; Jotai

---

> 📖 
> 
> <a id="226eda9b0fe1801ba84df640855af7b8"></a>
> 
> <code>Jotai</code>는 React를 위한 primitive하고 유연한 상태 관리 라이브러리이다&#46;
> 
> <a id="226eda9b0fe180d48ab5c3d4555137ef"></a>
> 
> 최소한의 API로 상태 관리할 수 있으며, TypeScript로 작성되어 타입 안정성이 뛰어나다&#46;

<details>
<summary>pnpm을 통한 Jotai 설치</summary>

<a id="226eda9b0fe180aaaf15e937ff7ec7ad"></a>

```bash
# pnpm 이용한 설치
pnpm create next-app@15 inflearn-jotai-tutorial
cd inflearn-jotai-tutorial
pnpm add jotai
```

</details>

<a id="226eda9b0fe180519cdac28539843032"></a>

## &#91; 실습 &#93; <code>jotai</code> 사용

---

<a id="226eda9b0fe180f3843dc91b52d8eb0c"></a>

### 1&#46; Jotai &#43; Next&#46;js  기본 설정

> ✏️ 
> 
> <a id="226eda9b0fe1804a8a37ffdb64975ee0"></a>
> 
> <code>jotai</code>의 <strong><u>Provider 컴포넌트</u></strong><strong> </strong>정의 후, <strong><u>루트 layout 컴포넌트</u></strong>에 적용한다&#46;  

<details>
<summary><code>config/providers&#46;tsx</code></summary>

<a id="226eda9b0fe1803987a5f38bfe5cd1f7"></a>

```typescript
"use client"

import { Provider as JotaiProvider } from "jotai";

export default function Providers({ children }: React.PropsWithChildren) {
		return <JotaiProvider>{children}</JotaiProvider>
}
```

</details>

<details>
<summary><code>app/layout&#46;tsx</code></summary>

<a id="226eda9b0fe180d290caf9e8e07143c0"></a>

```typescript
import "./globals.css";
import Providers from "./config/providers";

export default async function RootLayout({ children }) {
	return (
		<html lang="en">
			<body>
				<Providers>
					{children}
				</Providers>
			</body>
		</html>	
	)
}
```

</details>

<a id="226eda9b0fe180d7bb65d9ad5480d9d1"></a>

### 2&#46; 기본 사용법

<details>
<summary>1&#46; atom 생성</summary>

<a id="226eda9b0fe180d7af46d4cf8e01b70f"></a>

```typescript
import { atom } from 'jotai'

export const countAtom = atom(0) // 원시값
export const userAtom = atom({ name: 'John', age: 20 }) // 객체
export const derivedAtom = atom((get) => get(countAtom) * 2) // 다른 atom 참조
```

</details>

<details>
<summary>2&#46; atom 사용</summary>

<a id="226eda9b0fe180e6ace3ea951a3e4e0f"></a>

```typescript
"use client"

import { useAtom } from 'jotai'

function Counter() {
	const [count, setCount] = useAtom(countAtom)
	return (
		<button onClick={() => setCount(c => c + 1)}>
			Count: {count}
		</button>
	)
}
```

</details>
