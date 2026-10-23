---
order: 24
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1c3eda9b-0fe1-8168-9293-cd45faaddc76
title: styled-components
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-819c-beab-c6a3a1072bb9
    title: 리액트
  - id: 1c3eda9b-0fe1-81e6-a83a-de71fca84d73
    title: 실무 중심! FE 입문자를 위한 React
  - id: 1c3eda9b-0fe1-8168-9293-cd45faaddc76
    title: styled-components
excerpt: "styled-components --- 📖 리액트에서 css (스타일)을 컴포넌트 형태로 작성할 수 있도록 하는 라이브러리이다. - css 컴포너트 단위로 관리할 수 있다. - 내부에서 js를 조작할 수 있다. - ${ js 코드 } ( 보통 삼항연산자 와 많이 사용함 ) Docs [styled-components: B"
cover: null
icon: null
notionProperties:
  Tags: 스타일링
  상태: 완료
schema_version: 1
parent_id: 1c3eda9b-0fe1-81e6-a83a-de71fca84d73
created: 2025-03-27T07:47:43.045Z
updated: 2025-03-27T07:47:43.045Z
legacy_path: Main/리액트-c6a3a1072bb9/실무 중심! FE 입문자를 위한 React-de71fca84d73/styled-components-cd45faaddc76/index.md
legacy_category: 리액트
source_url: https://beautiful-college-c84.notion.site/1c3eda9b0fe181689293cd45faaddc76
---
<a id="1c3eda9b0fe181af8098edd425edc65e"></a>

## styled&#45;components

---

> 📖 
> 
> <a id="1c3eda9b0fe18155b792cff3e2457706"></a>
> 
> 리액트에서 css (스타일)을 컴포넌트 형태로 작성할 수 있도록 하는 라이브러리이다&#46; 
> 
> - css 컴포너트 단위로 관리할 수 있다&#46; 
> 
> - 내부에서 js를 조작할 수 있다&#46; &#45; <code>&#36;{ js 코드 }</code> ( 보통 <strong><u>삼항연산자</u></strong> 와 많이 사용함 )

<details>
<summary>Docs</summary>

[styled&#45;components&#58; Basics]()

</details>

<details>
<summary>styled components 설치</summary>

<a id="1c3eda9b0fe181dc8e15d5d48d47fafa"></a>

```javascript
npm install --save styled-components
```

</details>

<details>
<summary>사용 예시</summary>

<a id="1c3eda9b0fe1811283baef84a9808bbd"></a>

```javascript
// Create a Title component that'll render an <h1> tag with some styles
const Title = styled.h1`
  font-size: 1.5em;
  text-align: center;
  color: #BF4F74;
`;

// Create a Wrapper component that'll render a <section> tag with some styles
const Wrapper = styled.section`
  padding: 4em;
  background: papayawhip;
`;

// Use Title and Wrapper like any other React component – except they're styled!
render(
  <Wrapper>
    <Title>
      Hello World!
    </Title>
  </Wrapper>
);
```

</details>

<a id="1c3eda9b0fe181f48d32c21f4fc98160"></a>

### styled&#45;components의 장점

<details>
<summary>1&#46;   css안에<strong><u>  </u></strong><strong><u>js 조작 가능</u></strong>하다&#46;</summary>

<a id="1c3eda9b0fe181faac6cf76a6d0f630d"></a>

```
import styled from "styled-components";

const a = 123;

const CompletionPage = () => {
  return <CompletionPageWrapper>CompletionPage</CompletionPageWrapper>;
};

const CompletionPageWrapper = styled.div`
  background: aqua;
  padding: ${a === 123 ? "4em" : "1em"};
`;

export default CompletionPage;
```

</details>

1. 컴포넌트 처럼 태그 형태로 사용하기 때문에,  태그만을 보고 어떤 역활을 하는지 파악 가능하다&#46;
