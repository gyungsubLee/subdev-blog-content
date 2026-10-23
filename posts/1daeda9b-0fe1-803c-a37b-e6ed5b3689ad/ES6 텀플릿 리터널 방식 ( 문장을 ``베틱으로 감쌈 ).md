---
order: 29
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1daeda9b-0fe1-803c-a37b-e6ed5b3689ad
title: ES6 텀플릿 리터널 방식 ( 문장을 ``베틱으로 감쌈 )
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-819c-beab-c6a3a1072bb9
    title: 리액트
  - id: 1d4eda9b-0fe1-80a2-95f7-e975482b1dcd
    title: React + GSAP
  - id: 1daeda9b-0fe1-803c-a37b-e6ed5b3689ad
    title: ES6 텀플릿 리터널 방식 ( 문장을 ``베틱으로 감쌈 )
excerpt: ES6 버전 텀플릿 리터널 방식 ( 문장을 ``베틱으로 감쌈) --- ✏️ 특정 문자열 안에 변수를 넣으려면 문자와 변수를 분리시켜야하는데 이때 텀플릿 리터널 방식을 사용한다. 전체 문장을 ``으로 감싸고 변수는 ${변수명}로 적음 예제 javascript ex) const name = "강남순" const age = "
cover: null
icon: null
notionProperties:
  Tags: JS
  상태: 완료
schema_version: 1
parent_id: 1d4eda9b-0fe1-80a2-95f7-e975482b1dcd
created: 2025-04-19T04:44:06.969Z
updated: 2025-04-19T04:48:09.788Z
legacy_path: Main/리액트-c6a3a1072bb9/React + GSAP-e975482b1dcd/ES6 텀플릿 리터널 방식 ( 문장을 ``베틱으로 감쌈 )-e6ed5b3689ad/index.md
legacy_category: 리액트
source_url: https://beautiful-college-c84.notion.site/1daeda9b0fe1803ca37be6ed5b3689ad
---
<a id="1daeda9b0fe18098ac8ad788cb4e20ab"></a>

## ES6 버전 텀플릿 리터널 방식 ( 문장을 <code>&#96;&#96;</code>베틱으로 감쌈)

---

> ✏️ 
> 
> <a id="1daeda9b0fe1809584e4c60bc0057796"></a>
> 
> 특정 문자열 안에 변수를 넣으려면 문자와 변수를 분리시켜야하는데 이때 텀플릿 리터널 방식을 사용한다&#46;
> 
> > 전체 문장을 <code>&#96;&#96;</code>으로 감싸고  변수는  <code>&#36;{변수명}</code>로 적음

<a id="1daeda9b0fe1809a8507d21f2c4e235b"></a>

<strong>예제</strong>

<a id="1daeda9b0fe1802088cac73088eb0647"></a>

```javascript
ex)
const name = "강남순"
const age = "20";

console.log(" 안녕하세요 내이름은 " + name +"이고, 나이는 " + age + "살 입니다.") // es5 버전
console.log(`안녕하세요 내이름은 ${name}이고, 나이는 ${age}입니다`) // es6 버전
```
