---
order: 45
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 123eda9b-0fe1-8067-986b-c8aeed0ef6ab
title: static 으로 선언한 변수와 메서드는 그렇지 않은 변수와 메서드와 JVM - 런타임 영역에서 어떠한 차이를 보이는가?
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 108eda9b-0fe1-80a6-8a2b-c21df3ab9492
    title: 내일 배움 캠프 ( 백엔드 코스 7기)
  - id: 123eda9b-0fe1-800e-ab1a-e664218f399d
    title: To Do List
  - id: 123eda9b-0fe1-8067-986b-c8aeed0ef6ab
    title: static 으로 선언한 변수와 메서드는 그렇지 않은 변수와 메서드와 JVM - 런타임 영역에서 어떠한 차이를 보이는가?
excerpt: 🧐 priavte static final 사용 시, 값을 할당하지 않으면 컴파일 오류가 발생된다. - static 으로 선언 시, 클래스가 로드될 때 메모리에 초기화 되기 때문에..? 런타임 시에 영향을 받지 않아서 그런가? 🧐 Enum 클래스 다루는 법 🧐 클래스 변수, static 변수, 인스턴스 변수 stati
cover: null
icon: null
notionProperties:
  상태: 시작 전
  Category: 질문
schema_version: 1
parent_id: 123eda9b-0fe1-800e-ab1a-e664218f399d
created: 2024-10-18T12:30:11.740Z
updated: 2024-11-12T15:31:04.345Z
legacy_path: Main/내일 배움 캠프 ( 백엔드 코스 7기)-c21df3ab9492/To Do List-e664218f399d/static 으로 선언한 변수와 메서드는 그렇지 않은 변수와 메서드와 JVM - -c8aeed0ef6ab/index.md
legacy_category: 내일 배움 캠프 ( 백엔드 코스 7기)
source_url: https://beautiful-college-c84.notion.site/123eda9b0fe18067986bc8aeed0ef6ab
---
<details>
<summary>🧐 <code>priavte static final</code> 사용 시, 값을 할당하지 않으면 컴파일 오류가 발생된다&#46;</summary>

- static 으로 선언 시, 클래스가 로드될 때 메모리에 초기화 되기 때문에&#46;&#46;? 런타임 시에 영향을 받지 않아서 그런가?

</details>

<details>
<summary>🧐 Enum 클래스 다루는 법</summary>



</details>

<details>
<summary>🧐 클래스 변수, static 변수, 인스턴스 변수</summary>

<details>
<summary>static 변수(클래스 변수)</summary>

- 클래스가 로드 될 때,  <strong><u>메모리에 한번만 할당</u></strong>되고, <u>모든 인스턴스가 공유</u>한다 ( 싱글톤 )<br>즉, <strong>JVM이 클래스를 처음 로드할 때</strong> static 변수는 메모리에 할당되고, 프로그램 종료 시까지 유지된다&#46;
    - 메서드 영역(Method Aread)에 할당됨

- 따라서 모든 객체가 동일한 static 변수 값을 공유한다&#46;

- 객체(인스턴스)를 생성하지 않고도 클래스명으로 직접 접근 가능하다&#46;
    <details>
    <summary>ex)</summary>

    <a id="85d3091c018c4aff9a8c090d3bbb03e7"></a>

    ```java

    ```

    </details>

</details>

<details>
<summary>인스턴스 변수</summary>

- 힙(Heap) 영역에 할당된다&#46;

- 객체가 생성될 때마다, 해당 객체에 속한 인스턴스 변수가 메모리에 별도로 할당된다&#46;

- 이때 생성되는 인스턴스들은 독립적이다&#46;

</details>

</details>

<details>
<summary>🧐 클래스 멤버, 인스턴스 멤버</summary>

![](5d73b63c55f5d4fe.webp)

- 클래스(멤버)는 클래스가 로드될 때, 메모리에 한번 할당되고 모든 인스턴스가 공유한다&#46;
    <a id="2b630cef47af4bbf925339f3017233e1"></a>

    즉, 클래스 내부에 있는 멤버들도 같다&#46;

- 

</details>

<details>
<summary>🧐 인스턴스 메서드</summary>

<a id="bc6d46b3ee1b4eec9681d073924e1354"></a>

인스턴스가 생성될 때, 매번 메서드를 같이 생성한다면 메모리의 낭비가 너무 심하다&#46;

<a id="e54a7101a0ce40678777d037489929ba"></a>

따라서 클래서 메서드를 참조해서 사용한다&#46;

<a id="94a501382f864dceaa3dedba0fc6911b"></a>

사용 시에만, <code>인스턴스명&#46;메서드명()</code>으로 호출하여 사용한다&#46;

</details>

<details>
<summary>🧐 클래스 메서드와 static 메서드의 차이점</summary>



</details>

<details>
<summary>🧐 Method Area, Heap</summary>

- Method Area ( 메서드 영역 )
    - 가상 머신이 읽어 들인 <strong><u>타입 정보, 상수, 정적 변수 </u></strong>그리고 <strong><u>JIT 컴파일러가 컴파일한 코드 캐시 </u></strong>등을 저장하는데 사용한다&#46; 
        <a id="f3c33ca0db9e41f5878d9ba5cdf6a2dd"></a>

        즉, 클래스에 대한 메타데이터(클래스 정의, static 멤버, 메서드 코드 등)가 저장된다&#46; 

    - 클래스가 처음 로드될 때 해당 영역에 로드되며, 프로그램이 끝날 때까지 유지된다&#46;

- Heap
    - <strong><u>객체들이 생성</u></strong>될 때 객체의 <strong><u>인스턴스 멤버(필드 값 등)가 저장되는 공간</u></strong>이다&#46;

    - 모든 객체는 Heap에 저장된다&#46; 

</details>

<details>
<summary>🧐 Static 메서드에 어떻게 클래스 변수와 인스터스 변수가 접근할 수 있는가? </summary>



</details>
