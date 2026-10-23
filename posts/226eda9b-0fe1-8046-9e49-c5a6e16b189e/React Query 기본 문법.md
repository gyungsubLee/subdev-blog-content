---
order: 3
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 226eda9b-0fe1-8046-9e49-c5a6e16b189e
title: React Query 기본 문법
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 226eda9b-0fe1-802b-a035-c3a886768c4d
    title: Nest.js
  - id: 226eda9b-0fe1-80c9-b906-d1c0ad48e506
    title: "[ 풀스택 ] 인프런 클론 코딩 Next.js ,  Nest.js ( Part1 )"
  - id: 226eda9b-0fe1-8046-9e49-c5a6e16b189e
    title: React Query 기본 문법
excerpt: "reference [Inside React Query]() 목차 - 1. Server Action - [2. [ 실습 ] 기본 사용법](226eda9b0fe180b4bfead93e3fced1df) ✏️ 📖 1. Server Action React Query 설치 bash npm install react-query 2. "
cover: fb3b1ee7da4a15e0.webp
icon: 9bed2eae1e079b4b.avif
notionProperties: {}
schema_version: 1
parent_id: 226eda9b-0fe1-80c9-b906-d1c0ad48e506
created: 2025-07-04T08:27:29.969Z
updated: 2025-07-04T09:32:00.043Z
legacy_path: Main/Nest.js-c3a886768c4d/[ 풀스택 ] 인프런 클론 코딩 Next.js ,  Nest.js ( Part1 -d1c0ad48e506/React Query 기본 문법-c5a6e16b189e/index.md
legacy_category: Nest.js
source_url: https://beautiful-college-c84.notion.site/226eda9b0fe180469e49c5a6e16b189e
---
<details>
<summary>reference</summary>

[Inside React Query]()

</details>

> 
> 
> <a id="226eda9b0fe18154b8a7ca4a41597906"></a>
> 
> <strong>목차</strong>
> 
> - [1. Server Action](#226eda9b0fe1811ea5b4ce5f585fda67)
> - [2. [ 실습 ]  기본 사용법](#226eda9b0fe180b4bfead93e3fced1df)

> 

> ✏️ 

> 📖 

<a id="226eda9b0fe1811ea5b4ce5f585fda67"></a>

## 1&#46; Server Action

<details>
<summary>React Query 설치</summary>

<a id="226eda9b0fe18041a077e03b2b5d1864"></a>

```bash
npm install react-query
```

</details>

<a id="226eda9b0fe180b4bfead93e3fced1df"></a>

## 2&#46; &#91; 실습 &#93;  기본 사용법

---

<details>
<summary><code>useQuery</code></summary>

> ✏️ 
> 
> <a id="226eda9b0fe180379f6bd5c6cda8d16a"></a>
> 
> <code>useQuery</code>는 데이터를 가져오는 작업에 사용된다&#46;

<a id="226eda9b0fe1801a9b30d794d34fe288"></a>

```typescript
import { useQuery } from 'react-query';

function TodosPage() {
	const todosQuery = useQuery({
		queryKey: ["todos"],
		queryFn: () => getTodos(),
	})
	
	// ... return ...
}
```

- 위 예제에서 useQuery는 2개의 인수를 받는다&#46;
    1. 쿼리 키

    1. 데이터를 조회하는 함수

</details>

<details>
<summary><code>useMutaion</code></summary>

> ✏️ 
> 
> <a id="226eda9b0fe1801ca32bda5205aebb76"></a>
> 
> <code>useMutation</code>은 데이터를 변경하는 작업(ex&#46; POST, PUT, DELETE)에 사용된다&#46; 

<a id="226eda9b0fe18014b32ed29b7f9f205a"></a>

```typescript
import { useMutation, useQueryClient } from 'react-query';

function TodosPage() {
	const createTodoMutation = useMutation({
		mutationFn: async () => {
			if (todoInput === "") throw new Error("TODO를 입력해주세요"):
			return createTodo(todoInput);			
		},
		onSuccess: (TODOS) => {
			todosQuery.refetch();
			// queryClient를 사용해 쿼리 캐시를 날릴 수 있다. 
			// queryClient.invalidateQueries(["todos"]);
		},
		onError: (error: any) => {
			alert(error.message);
		},
	});
	
	// ... return ...
}
```

</details>

<details>
<summary><code>config/ReactQueryProvider&#46;tsx</code></summary>

<a id="226eda9b0fe1803f9d80dae5dee14595"></a>

```typescript
import { QueryClient, QueryClientProvider } from "react-query";

const queryClinet = new QueryClient();

export default function ReactQueryProvider({children}) {
	return (
		<QueryClientProvider client={queryClient}>
			{children}
		</QueryClientProvider>
	)
}
```

</details>
