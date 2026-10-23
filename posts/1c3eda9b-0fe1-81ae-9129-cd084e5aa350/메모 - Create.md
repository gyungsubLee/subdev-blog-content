---
order: 38
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1c3eda9b-0fe1-81ae-9129-cd084e5aa350
title: 메모 - Create
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-819c-beab-c6a3a1072bb9
    title: 리액트
  - id: 1c3eda9b-0fe1-81e6-a83a-de71fca84d73
    title: 실무 중심! FE 입문자를 위한 React
  - id: 1c3eda9b-0fe1-81ae-9129-cd084e5aa350
    title: 메모 - Create
excerpt: "요구사항 - 새로운 메모 생성 시 - title: Untitled - content: ‘’ - createdAt: 생성시간 - updatedAt: 동일 - 새로 생성된 메모가 check 되어 바로 화면 변경이 일어나야 한다 . javascript setMemoContainerIndex(memos.length); 구현 - "
cover: null
icon: null
notionProperties:
  중요도: Yes
  상태: 완료
schema_version: 1
parent_id: 1c3eda9b-0fe1-81e6-a83a-de71fca84d73
created: 2025-03-27T07:47:43.044Z
updated: 2025-03-27T07:47:43.044Z
legacy_path: Main/리액트-c6a3a1072bb9/실무 중심! FE 입문자를 위한 React-de71fca84d73/메모 - Create-cd084e5aa350/index.md
legacy_category: 리액트
source_url: https://beautiful-college-c84.notion.site/1c3eda9b0fe181ae9129cd084e5aa350
---
<a id="1c3eda9b0fe1813a89cde879a2733b24"></a>

### 요구사항

- 새로운 메모 생성 시
    - title&#58; Untitled

    - content&#58; ‘’

    - createdAt&#58; 생성시간

    - updatedAt&#58; 동일

- 새로 생성된 메모가 check 되어 바로 화면 변경이 일어나야 한다 &#46;
    <a id="1c3eda9b0fe181bc9e18e8bdf98aa3b0"></a>

    ```javascript
    setMemoContainerIndex(memos.length);
    ```

<a id="1c3eda9b0fe18139ab2ae110ef40c47d"></a>

### 구현 &#45; Create

<details>
<summary>&#91; 코드 &#93; App&#46;js</summary>

<a id="1c3eda9b0fe1815a89a5dae2e1f84d00"></a>

```javascript
function App() {
  const [memos, setMemos] = useState(defaultMemosData);

  const [memoContainerIndex, setMemoContainerIndex] = useState(0);

  const setMemo = (newMemo) => {
    const newMemos = [...memos];
    newMemos[memoContainerIndex] = newMemo;

    setMemos(newMemos);
  };

  const addMemo = (addMemo) => {
    const now = new Date().getTime();  // 클린코드: 중복 코드인 경우, 변수 추출

    setMemos([   // 요구사항1: 새로운 메모 생성
      ...memos,
      {
        title: "Untitled",
        content: "",
        createdAt: now,
        updatedAt: now,
      },
    ]);
    
    setMemoContainerIndex(memos.length);  // 요구사항 2: 새로 생성된 메모 check
  };

  return (
    <div className="App">
      <SideBar
        memos={memos}
        setMemoContainerIndex={setMemoContainerIndex}
        memoContainerIndex={memoContainerIndex}
        addMemo={addMemo}
      />
      <MemoContainer memo={memos[memoContainerIndex]} setMemo={setMemo} />
    </div>
  );
}
```

</details>

<details>
<summary>&#91; 코드 &#93; SideBar&#46;js</summary>

<a id="1c3eda9b0fe181bfbaebd3277dbf32da"></a>

```javascript
const SideBar = ({
  memos,
  addMemo,
  setMemoContainerIndex,
  memoContainerIndex,
}) => {
  return (
    <div className="SideBar">
      <SideBarHeader />
      <MemoList
        memos={memos}
        setMemoContainerIndex={setMemoContainerIndex}
        memoContainerIndex={memoContainerIndex}
      />
      <SideBarFooter onClick={addMemo} />
    </div>
  );
};
```

</details>

<details>
<summary>&#91; 코드 &#93; SideBarFooter&#46;js</summary>

<a id="1c3eda9b0fe181488491e9d0edaebdf4"></a>

```javascript
const SideBarFooter = ({ onClick }) => {
  return (
    <div className="SideBarFooter">
      <Button onClick={onClick} />
    </div>
  );
};
```

</details>

<details>
<summary>&#91; 코드 &#93; Button&#46;js</summary>

<a id="1c3eda9b0fe1814688c7d3a021d5aaca"></a>

```javascript
const Button = ({ onClick }) => {
  return (
    <button className="custom-btn btn-3" onClick={onClick}>
      <span>메모 추가</span>
    </button>
  );
};
```

</details>
