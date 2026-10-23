---
order: 7
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 226eda9b-0fe1-8033-8da8-d95646ad1c16
title: Next.js  - 개념 2. Metadata, Server Action
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 226eda9b-0fe1-802b-a035-c3a886768c4d
    title: Nest.js
  - id: 226eda9b-0fe1-80c9-b906-d1c0ad48e506
    title: "[ 풀스택 ] 인프런 클론 코딩 Next.js ,  Nest.js ( Part1 )"
  - id: 226eda9b-0fe1-8033-8da8-d95646ad1c16
    title: Next.js  - 개념 2. Metadata, Server Action
excerpt: 목차 - 1. Server Actions - [[ 실습 ] Using Forms in Next.js](226eda9b0fe1803282eaf0b22457839c) - 2. Metadata - 1. Static Metadata 방식 - 2. Dynamic Metadata 방식 1. Server Actions --- Docs
cover: fb3b1ee7da4a15e0.webp
icon: 9bed2eae1e079b4b.avif
notionProperties: {}
schema_version: 1
parent_id: 226eda9b-0fe1-80c9-b906-d1c0ad48e506
created: 2025-07-04T04:08:24.316Z
updated: 2025-07-04T07:53:02.761Z
legacy_path: Main/Nest.js-c3a886768c4d/[ 풀스택 ] 인프런 클론 코딩 Next.js ,  Nest.js ( Part1 -d1c0ad48e506/Next.js  - 개념 2. Metadata, Server Action-d95646ad1c16/index.md
legacy_category: Nest.js
source_url: https://beautiful-college-c84.notion.site/226eda9b0fe180338da8d95646ad1c16
---
> 
> 
> <a id="226eda9b0fe180e5af34e00b91e61699"></a>
> 
> <strong>목차</strong>
> 
> - [1. Server Actions](#226eda9b0fe180b28a3be29a6d439d88)
> - [[ 실습 ] Using Forms in Next.js](#226eda9b0fe1803282eaf0b22457839c)
> - [2. Metadata](#226eda9b0fe180caace5f43725c61dfc)
> - [1. Static Metadata 방식](#226eda9b0fe1803dbc90f7d561d76eb0)
> - [2. Dynamic Metadata 방식](#226eda9b0fe1804ca900d258802b52af)

<a id="226eda9b0fe180b28a3be29a6d439d88"></a>

## 1&#46; <code>Server Actions</code>

---

<details>
<summary>Docs</summary>

[Getting Started&#58; Updating Data]()

</details>

> 📖 
> 
> <a id="226eda9b0fe180c2a8e3f9a206414cd8"></a>
> 
> Next&#46;js의 <code>Server Actions</code>는 <strong><u>서버에서 실행되는 함수를 클라이언트 컴포넌트에서 직접 호출</u></strong>할 수 있게 해주는 기능이다&#46;
> 
> <a id="226eda9b0fe180aca2c5c7887e2bcaff"></a>
> 
> 이는 Next&#46;js 14에서 안정화(stable) 되었으며, React의 서버 컴포넌트(Server Components) 및 Next&#46;js의 새로운 앱 라우터(App Router)와 함께 사용하는 새로운 형태의 <strong>mutating</strong> API이다&#46; 
> 
> - 서<strong>버에서 실행되는 함수를 직접 import 없이 클라이언트에서 호출 가능</strong>

<details>
<summary>ex)</summary>

- 기존 데이터를 수정하거나 저장하려 아래와 같은 흐름이 필요했다&#46; 
    <a id="226eda9b0fe180f49152e8a52f38202d"></a>

    ```typescript
    // client
    await fetch('/api/save', { method: 'POST', body: JSON.stringify(data) })

    // server - /api/save.ts
    export async function POST(req: Request) {
      // parse and save to DB
    }
    ```

    <a id="226eda9b0fe180758e92eee892076f0f"></a>

    이러한 흐름은 API 라우트를 수동으로 생성하고, fetch 호출을 통해 처리했기 때문에, <strong><u>중복 코드 및 불편한 타입 추론</u></strong><strong> </strong>문제점이 존재했다&#46;

- 이를 Server Actions을 통해 단순화하여 해결한다&#46; 
    <a id="226eda9b0fe1805aa8d5fd36c12638b4"></a>

    ```typescript
    // actions.ts (서버)
    'use server'

    export async function saveData(data: FormData) {
      // 서버에서 직접 DB 저장
    }
    ```

    <a id="226eda9b0fe18043bebcce8814ce4d19"></a>

    ```typescript
    // page.tsx (클라이언트)
    <form action={saveData}>
      <input name="title" />
      <button type="submit">Save</button>
    </form>
    ```

    <a id="226eda9b0fe18016927bfdac5805954a"></a>

    <code>saveData</code>는 서버에서 실행되며, 클라이언트에서 import하지 않고 <code>form actions={}</code>로 바로 연결한다&#46;

</details>

<a id="226eda9b0fe1803282eaf0b22457839c"></a>

### &#91; 실습 &#93; <strong>Using Forms in Next&#46;js</strong>

> 
> 
> <a id="226eda9b0fe180849bf0f18cfa48828e"></a>
> 
> 유저를 DB에서 검색
> 
> - <strong><code>fetch</code></strong><strong> &#43; </strong><strong><code>REST API</code></strong>
> 
> - <strong><code>Server Action</code></strong>

[video](https://www.youtube.com/watch?v=dDpZfOQBMaU&embeds_referring_euri=https%3A%2F%2Fwww.notion.so%2F&source_ve_path=MjM4NTE)

<a id="226eda9b0fe180caace5f43725c61dfc"></a>

## <strong>2&#46; Metadata</strong>

---

> ✏️ 
> 
> <a id="226eda9b0fe180a8bda0e9d75fadb7d2"></a>
> 
> <code>Next&#46;js</code>는 <strong><u>SEO와 웹 공유성을 향상</u></strong>시키기 위해 애플리케이션의 메타데이터(ex&#46; HTML head 요소 내 메타 및 링크 태크 )를 정의하는데 사용할 수 있는 <strong><u>메타데이터 API를 가지고 있</u></strong>다&#46; 

<a id="226eda9b0fe180a386c8cbbf19ffd876"></a>

메타데이터를 애플리케이션에 추가하는 2가지 방법

<a id="226eda9b0fe1803dbc90f7d561d76eb0"></a>

### 1&#46; Static Metadata 방식

<a id="226eda9b0fe180ee93aedb425c82bece"></a>

```typescript
import type { Metadata } from 'next'
 
export const metadata: Metadata = {
  title: '...',
  description: '...',
}
 
export default function Page() {}
```

<a id="226eda9b0fe1804ca900d258802b52af"></a>

### 2&#46; Dynamic Metadata 방식

<a id="226eda9b0fe1808cb43ee698e16a68bd"></a>

```typescript
import type { Metadata, ResolvingMetadata } from 'next'
 
type Props = {
  params: { id: string }
  searchParams: { [key: string]: string | string[] | undefined }
}
 
export async function generateMetadata(
  { params, searchParams }: Props,
  parent: ResolvingMetadata
): Promise<Metadata> {
  // read route params
  const id = params.id
 
  // fetch data
  const product = await fetch(`https://.../${id}`).then((res) => res.json())
 
  // optionally access and extend (rather than replace) parent metadata
  const previousImages = (await parent).openGraph?.images || []
 
  return {
    title: product.title,
    openGraph: {
      images: ['/some-specific-page-image.jpg', ...previousImages],
    },
  }
}
 
export default function Page({ params, searchParams }: Props) {}
```
