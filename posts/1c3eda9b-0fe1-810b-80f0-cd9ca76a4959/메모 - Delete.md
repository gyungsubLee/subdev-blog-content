---
order: 39
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1c3eda9b-0fe1-810b-80f0-cd9ca76a4959
title: 메모 - Delete
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-819c-beab-c6a3a1072bb9
    title: 리액트
  - id: 1c3eda9b-0fe1-81e6-a83a-de71fca84d73
    title: 실무 중심! FE 입문자를 위한 React
  - id: 1c3eda9b-0fe1-810b-80f0-cd9ca76a4959
    title: 메모 - Delete
excerpt: "코드 - Memo 삭제 및 undefind 오류 처리 [project 1: memo - Delete, undefind 오류 처리 · gyungsubLee/inflearn_react_prac@aa9a8b7]() 학습 내용 메모 삭제 javascript const deleteMemo = (index) = { const new"
cover: null
icon: null
notionProperties:
  중요도: Yes
  상태: 의문점 정리 필요
schema_version: 1
parent_id: 1c3eda9b-0fe1-81e6-a83a-de71fca84d73
created: 2025-03-27T07:47:43.044Z
updated: 2025-03-27T07:47:43.044Z
legacy_path: Main/리액트-c6a3a1072bb9/실무 중심! FE 입문자를 위한 React-de71fca84d73/메모 - Delete-cd9ca76a4959/index.md
legacy_category: 리액트
source_url: https://beautiful-college-c84.notion.site/1c3eda9b0fe1810b80f0cd9ca76a4959
---
<a id="1c3eda9b0fe181898052da7260e6cbd9"></a>

### 코드  &#45; Memo  삭제 및 undefind 오류 처리

[project 1&#58; memo &#45; Delete, undefind 오류 처리 · gyungsubLee/inflearn&#95;react&#95;prac&#64;aa9a8b7]()

<a id="1c3eda9b0fe181b39023f6e820ae8af8"></a>

### 학습 내용

<details>
<summary>메모 삭제 </summary>

<a id="1c3eda9b0fe181e1b32ddcd0782f27d6"></a>

```javascript
  const deleteMemo = (index) => {
    const newMemos = [...memos];
    
    newMemos.splice(index, 1);
    
    setMemos(newMemos);
    
    console.log(index, memoContainerIndex);
    
    if (index === memoContainerIndex) {
      setMemoContainerIndex(0);
    }
  };
```

</details>

<details>
<summary>🤬 오류 &#45; 클릭된 메모가 삭제되면, undefind Error가 발생된다&#46; , 이벤트… (이해안됨 다시보기 )</summary>

<details>
<summary>🧐 event&#46;preventDefault</summary>



</details>

<details>
<summary>🧐 event&#46;stopPropagation</summary>



</details>

<a id="1c3eda9b0fe181b99160d258abfab1a0"></a>

```javascript
onClickDelete={(e) => {
	  deleteMemo(index);
	  e.preventDefault();
	  e.stopPropagation();
}}
```

</details>

<details>
<summary>🤬 오류 &#45; 전체 메모 삭제 시, <code>memo = undefind</code>오류 발생 </summary>

- MemoCotainer로 넘어가는 memo에 <code>undefind</code>가 넘어가는 경우, <br>조건문으로 다른 view를 보이게끔 수정 

<details>
<summary>&#91; 코드 &#93; MemoContainer&#46;jsx</summary>

<a id="1c3eda9b0fe1818996beddf19d6411b5"></a>

```javascript
const MemoContainer = ({ memo, setMemo }) => {

  if (memo === undefined) {
    return (
      <div>
        <h1>메모가 없습니다.</h1>
        <h2>메모를 추가해 주세요</h2>
      </div>
    );
  }

  return (
    <div className="MainContainer">
      <div>
        <input
          type="text"
          className="MainContainer__title"
          value={memo.title}
          onChange={(e) => {
            setMemo({
              ...memo,
              title: e.target.value,
              updatedAt: new Date().getTime(),
            });
          }}
        />
      </div>
      <div>
        <textarea
          className="MainContainer__content"
          value={memo.content}
          onChange={(e) => {
            setMemo({
              ...memo,
              content: e.target.value,
              updatedAt: new Date().getTime(),
            });
          }}
        />
      </div>
    </div>
  );
};

export default MemoContainer;

```

</details>

</details>

<a id="1c3eda9b0fe1814fa936fa554a26db43"></a>

### 스타일 구조, 및 파일 다듬기
