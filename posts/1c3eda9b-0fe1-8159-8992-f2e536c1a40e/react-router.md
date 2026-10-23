---
order: 42
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1c3eda9b-0fe1-8159-8992-f2e536c1a40e
title: react-router
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-819c-beab-c6a3a1072bb9
    title: 리액트
  - id: 1c3eda9b-0fe1-81e6-a83a-de71fca84d73
    title: 실무 중심! FE 입문자를 위한 React
  - id: 1c3eda9b-0fe1-8159-8992-f2e536c1a40e
    title: react-router
excerpt: Routing --- 프론트에서 라우팅이란, 주소에 맞게 적절한 페이지를 로드하는 것이다 예를 들어, 특정 사이트의 리스트라는 경로에 있다가 화면에 있는 링크를 클릭해서 다른 페이지로 이동하는 경우, 라우팅 이라 한다. 전통적인 방식의 웹 서비스에서의 라우팅은 서버에 요청하는 주소에 따라 서로 다른 페이지의 HTML을 보
cover: null
icon: null
notionProperties:
  Tags: react-router
  중요도: Yes
  상태: 완료
schema_version: 1
parent_id: 1c3eda9b-0fe1-81e6-a83a-de71fca84d73
created: 2025-03-27T07:47:43.044Z
updated: 2025-03-27T07:47:43.044Z
legacy_path: Main/리액트-c6a3a1072bb9/실무 중심! FE 입문자를 위한 React-de71fca84d73/react-router-f2e536c1a40e/index.md
legacy_category: 리액트
source_url: https://beautiful-college-c84.notion.site/1c3eda9b0fe181598992f2e536c1a40e
---
<a id="1c3eda9b0fe1811097add91b7da8398a"></a>

## Routing

---

![](f2f709cd7006a24a.webp)

<a id="1c3eda9b0fe1816686b1ee7dd6f2ecf1"></a>

프론트에서 라우팅이란, 주소에 맞게 적절한 페이지를 로드하는 것이다 

<a id="1c3eda9b0fe181d0be57e00da23f3deb"></a>

예를 들어, 특정 사이트의 리스트라는 경로에 있다가 화면에 있는 <u>링크를 클릭</u>해서 <strong>다른 페이지로 이동</strong>하는 경우, <code>라우팅</code> 이라 한다&#46;

<a id="1c3eda9b0fe181648f85c1482001277f"></a>

전통적인 방식의 웹 서비스에서의 <code>라우팅</code>은 <strong><u>서버에 요청하는 주소에 따라 서로 다른 페이지의 HTML을 보여주는 방식</u></strong>이었다&#46; 

<a id="1c3eda9b0fe18178b39ac256979ea769"></a>

SPA 방식에서는 페이지가 여러 개가 아닌 말 그대로 싱글 페이지 애플리케이션이기 때문에, <br>SPA에서의 <code>라우팅</code>은 <strong><u>브라우저의 히스토리를 조작</u></strong>하는 방식으로 동작한다&#46; 

<a id="1c3eda9b0fe181c491cbe87128265566"></a>

## 브라우저 history

---

![](2225aeeb45c6ea4c.webp)

<a id="1c3eda9b0fe181e89bb9d16e60debc3b"></a>

브라우저는 <strong><u>페이지 이동에 대한 내용을 기록</u></strong>하기 위해 <code>히스토리 객체</code>를 가지고 있다&#46;

- 페이지를<strong><u> 앞으로 가기</u></strong>, <strong><u>뒤로 가기</u></strong> 하여 변경할 수 있는 것도 이 히스토리 객체 덕분이다 &#46;

<a id="1c3eda9b0fe181c09923dbbd044ca0d5"></a>

히스토리 객체에서 제공하는 기능들을 활용해 실제 다른 링크로 페이지를 이동하지 않지만<br>즉, 해당하는 주소로 HTTP 요청을 보내지 않지만 히스토리를 직접 쌓음으로써 페이지가 이동하는 것과 같은 효과를 줄 수 있다&#46; 

<a id="1c3eda9b0fe18190b229cab2b2719835"></a>

## React&#45;router

---

![](85d2225dc62b4023.webp)

<a id="1c3eda9b0fe181dfb554ca47297ad05a"></a>

<code>SPA</code>에서는 이 <strong><u>히스토리 객체를 사용</u></strong>하여 페이지가 변경(라우팅)되는 효과를 활용하며, <br>리액트에서는 <code>리액트 라우터</code>라는 라이브러리를 통해 구현할 수 있다&#46; 

<a id="1c3eda9b0fe181fdbb3dc0aa5f7f1e44"></a>

즉, 리액트 라우터는 <strong><u>리액트에서 라우팅 기능을 구현</u></strong>한 라이브러리이다&#46;

<a id="1c3eda9b0fe181aa8e68ea4998bd6644"></a>

따라서 내부적으로 히스토리 객체를 통해 주소를 변경하고, 변경된 주소에 대한 적절한 화면을 보여줄 수 있도록 도와준다&#46;
