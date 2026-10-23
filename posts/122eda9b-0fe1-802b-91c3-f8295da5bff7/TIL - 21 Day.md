---
order: 41
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 122eda9b-0fe1-802b-91c3-f8295da5bff7
title: TIL - 21 Day
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 108eda9b-0fe1-80a6-8a2b-c21df3ab9492
    title: 내일 배움 캠프 ( 백엔드 코스 7기)
  - id: 10aeda9b-0fe1-8045-a8c4-f10918253453
    title: TIL
  - id: 122eda9b-0fe1-802b-91c3-f8295da5bff7
    title: TIL - 21 Day
excerpt: 💡 PDS 다이어리 참조 PlAN - [ ] 알고리즘 코드 카타 - 과제 - 계산기 - [x] 결과 값 저장, 삭제, 수정 개발 - [x] README 작성 - [ ] 리펙토링 후, 반복 연산처리 안됨 → 수정 필요 - 자바 문법 강의 - [ ] 3주차 - 객체 지향 다시 정리 - [ ] 4주차 - 예외처리, 제네릭 정
cover: null
icon: null
notionProperties:
  날짜: 2024-10-17
  Category: TIL,질문
  Keyword: |-
    • 과제 제출
    • 질문) 클래스의 책임, 시스템 설계
  데일리 스크럼: "[페이지](https://beautiful-college-c84.notion.site/122eda9b0fe1807a87dff223b8e9a52d)"
schema_version: 1
parent_id: 10aeda9b-0fe1-8045-a8c4-f10918253453
created: 2024-10-17T02:04:38.127Z
updated: 2024-10-19T03:10:12.948Z
legacy_path: Main/내일 배움 캠프 ( 백엔드 코스 7기)-c21df3ab9492/TIL-f10918253453/TIL - 21 Day-f8295da5bff7/index.md
legacy_category: 내일 배움 캠프 ( 백엔드 코스 7기)
source_url: https://beautiful-college-c84.notion.site/122eda9b0fe1802b91c3f8295da5bff7
---
> 💡 
> 
> <a id="122eda9b0fe181f5b71fd68bdde33874"></a>
> 
> PDS 다이어리 참조

<details>
<summary><strong>PlAN</strong></summary>

- [ ] <del>알고리즘 코드 카타 </del>

- 과제 &#45; 계산기 
    - [x] 결과 값 저장, 삭제, 수정 개발

    - [x] README 작성

    - [ ] 리펙토링 후, 반복 연산처리 안됨 → 수정 필요

- 자바 문법 강의
    - [ ] <del>3주차 &#45; 객체 지향 다시 정리</del>

    - [ ] <del>4주차 &#45; 예외처리, 제네릭 정리</del>

- [x] 질문한 내용 정리하기 &#45; 거의 3시간 걸린 듯…?


</details>

<a id="122eda9b0fe181849b47ca6b7f0098c2"></a>

### DO

<details>
<summary>과제 &#45; 계산기 </summary>

[Calculator_with_java](https://github.com/gyungsubLee/Calculator_with_java)

- Lv2 까지 완료

<details>
<summary>🧐 <code>캡슐화</code>, <code>메서드화</code></summary>

> <code>캡슐화</code>에 대한 개념을 잘못 이해하고 있었음

<details>
<summary>캡슐화 </summary>

- 객체의 상태 데이터(필드) <code>private</code> 선언

- 해당 필드를 <code>getter</code>, <code>setter</code>를 통해 외부에서 접근 및 수정

- 이를 통해 외부에서 데이터를 직접 접근하고 못하게 숨기고 , <br>대신 메서드를 통해서만 접근(getter) 및 수정(setter) 가능하게 제한하여

- <strong>코드의 </strong><strong><u>무결성을</u></strong><strong> 유지</strong>하고, <strong>변경에 대해 </strong><strong><u>안전</u></strong><strong>한 구조를 만</strong>든다&#46;

<details>
<summary>ex) </summary>

<a id="122eda9b0fe180d88e39dc95bb022555"></a>

```java
public class Person {
    private String name;  // private 선언

		// getter
    public String getName() {  // 메서드를 통해서만 접근 가능
        return name;
    }

		// setter
    public void setName(String name) {
        this.name = name;
    }
}
```

</details>

</details>

<details>
<summary>메서드화</summary>

- 단순히 어떤 로직이나 코드를 <strong>하나의 메서드로 분리</strong>하는 것

- 코드의 <strong>재사용성, 가독성 ↑</strong>

<details>
<summary>ex)</summary>

<a id="122eda9b0fe180dc95a0cd9232ed0ee9"></a>

```java
public class Calculator {

		// 메서드화
    public int add(int a, int b) {
        return a + b;
    }
}
```

</details>

</details>

</details>

</details>

<details>
<summary>중요) 시스템 설계 시, 클래스의 책임에 대하여 </summary>

<a id="124eda9b0fe180f8a40be4cb4afe62c2"></a>

<a href="#/post/124eda9b-0fe1-8069-9236-e2762e90aaa7">페이지</a> 

</details>

<a id="122eda9b0fe1814ca52bd4999099e9d9"></a>

### SEE 

<details>
<summary>학습 방법 수정</summary>

<a id="122eda9b0fe181a7bab3da870ecf1bd1"></a>

무작정 정리를 하려고 보니 머리에 하나도 안들어 온다&#46;

<a id="122eda9b0fe180d6b2fdd3e5706ea29c"></a>

→ <strong><u>공부 범위를 정</u></strong>하고 읽으면서 <u>이해가 안되는 부분 질문으로 정의</u>하고 <u>해당 질문을 해결하는 형식</u>으로 학습을 진행 해야겠다&#46; 

</details>

<details>
<summary>Plan 수정</summary>

- 너무 많은 양을 계획으로 잡는다 → 조급한 마음에 더 진행이 안된다&#46; 

- <strong><u>One thing</u></strong>이다&#46; 우선 <strong><u>오늘 꼭 끝내야하는 하나부</u></strong>터 정하고 그게 끝나면 다음 계획을 진행하자 

</details>

<details>
<summary>자바 문법 종합반 프로젝트 구조 수정 필요</summary>

> <a href="https://beautiful-college-c84.notion.site/213de689e18f49d7bfbbb2d46e7663d8">페이지</a> 

- 데이터베이스 생성 후, 더 세부적으로 바꾸기 

- 기존에 정리하던 것 처럼 데이터베이스로 구분하고 각 페이지에서 더 세부적으로 작성

</details>

<details>
<summary>질문하기 </summary>

- 튜터님에게 질문하여 답변을 받는게  굉장히 비용적인 측면에서도, 효율적인 측면에서도 value가 높은 행위이다&#46; 더 적극적으로 행동할 필요가 있다&#46; 

- 개인적으로는 ‘박진상 튜터님’, ‘최원빈’ 튜터님이 잘 맞는 것 같다&#46; 
    - 더 데이터를 수집할 필요가 있음

    <a id="122eda9b0fe180d4a4b3dd31e48e5761"></a>

    ⇒ 다음 주 내로 최소 한번 씩 질문해보기 

</details>

<details>
<summary>수면 시간 최소 7시간 필수</summary>

- 어제 과제 수정 때문에 거의 오전 4시에 잠을 잤다&#46; 

- 4시간 반 정도 수면을 취한 것 같은데,

- 오늘 무슨 정신으로 지냈는지도 모르겠다&#46; 

- 학습 효율이 거의 0에 가깝다&#46; 
    <a id="122eda9b0fe180b5a981dc20be6535fe"></a>

    ⇒ 취침&#58;  12시  &#126; 1시 

</details>
