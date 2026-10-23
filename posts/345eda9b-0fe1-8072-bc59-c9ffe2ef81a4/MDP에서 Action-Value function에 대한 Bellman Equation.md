---
order: 23
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 345eda9b-0fe1-8072-bc59-c9ffe2ef81a4
title: MDP에서 Action-Value function에 대한 Bellman Equation
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 31deda9b-0fe1-80d6-826b-c54fbb1123ff
    title: 강화학습
  - id: 320eda9b-0fe1-80d1-842c-e609cad65258
    title: 스크래치부터 시작하는 강화학습의 모든것
  - id: 345eda9b-0fe1-8072-bc59-c9ffe2ef81a4
    title: MDP에서 Action-Value function에 대한 Bellman Equation
excerpt: 🤔 Action Value function은 Action을 고려한 관계식이다. 즉, action을 고려하지 않는 MRP에서 Action-Value function은 존재하지 않는다. MDP <S, A, P, R ,\gamma>에서 Action-Value function에 대한 Bellman Equation --- Act
cover: null
icon: null
notionProperties:
  상태: 완료
schema_version: 1
parent_id: 320eda9b-0fe1-80d1-842c-e609cad65258
created: 2026-04-17T07:48:22.014Z
updated: 2026-04-28T13:50:55.334Z
legacy_path: Main/강화학습-c54fbb1123ff/스크래치부터 시작하는 강화학습의 모든것-e609cad65258/MDP에서 Action-Value function에 대한 Bellman Equat-c9ffe2ef81a4/index.md
legacy_category: 강화학습
source_url: https://beautiful-college-c84.notion.site/345eda9b0fe18072bc59c9ffe2ef81a4
---
> 🤔 
> 
> <a id="350eda9b0fe180daab28c9ec717f0a95"></a>
> 
> Action Value function은 Action을 고려한 관계식이다&#46; <br>즉, action을 고려하지 않는 MRP에서 Action&#45;Value function은 존재하지 않는다&#46;

<a id="350eda9b0fe180698fa9d248a26bab13"></a>

## MDP <code class="language-math">&#60;S, A, P, R ,&#92;gamma&#62;</code>에서 Action&#45;Value function에 대한 Bellman Equation

---

<a id="350eda9b0fe1808f999bc9644e9f6e22"></a>

### Action Value Function

![](8634db2f3ee8e94f.webp)

<a id="350eda9b0fe180e88864e6109d8b6fd1"></a>

### 유도 방법 1

![](bdf3051868092ae4.webp)

- <code class="language-math">A&#95;{t&#43;1}</code>은 Random variable이기 때문에  평균(Expectation)으로 구한다&#46;
    ![](0e0d31295db36f6f.webp)

<a id="350eda9b0fe180ad9054fa972dfd0355"></a>

### 유도 방법 2

![](6bc4b9f74fe20791.webp)

- <code class="language-math">s&#95;{t&#43;1}</code>에 대한 식 변형
    ![](a628a2c10104a34e.webp)

- <code class="language-math">s&#95;t</code>, <code class="language-math">a&#95;t</code>, <code class="language-math">s&#95;{t&#43;1}</code> 이 주어지면 Reward function을 계산할 수 있다&#46; <br>즉, 더이상 Random variable이 아닌 <strong><u>상수</u></strong>로써 <code class="language-math">E&#95;{&#92;pi}&#91;…&#93;</code>을 빠져나올 수 있다&#46; 
    ![](8c4523ba52609421.webp)

- <code class="language-math">a&#95;{t&#43;1}</code>에 대한 식 변형
    ![](4385acbcf6b839c8.webp)

<a id="350eda9b0fe1800d8722cd2fc44542ae"></a>

### 정리 &#45; Bellman equation for Action&#45;Value function

![  • 백업 다이어그램](d9089f344e051a0f.webp)

<a id="350eda9b0fe180d1a9fadddbb33368a5"></a>

### Bellman equation for Action&#45;Value function

![](e0693ea74a6f31db.webp)

<a id="350eda9b0fe180d2bb62e79a331f70f4"></a>

### 예제 

![](ebf4f4729f9e17d6.webp)

- <code class="language-math">Q^{&#92;pi}(s&#95;2, a&#95;0)</code>
    ![](bbb48fd939b92e5a.webp)

<a id="350eda9b0fe180bbb1d4ca3103ac02ea"></a>

## MDP <code class="language-math">&#60;S, A, P, R ,&#92;gamma&#62;</code>에서 <code>Value function</code>, <code>Action&#45;Value function</code> 관련 수식

---

<a id="350eda9b0fe180ee93e6e6064a739371"></a>

### Action&#45;Value function을 활용한 Value function 표현

![](f12ddc13f0b3c6b2.webp)

<a id="350eda9b0fe180098b51fac3c538be23"></a>

### Value function을 활용한 Action&#45;Value function 표현

![](32c11b6a27de7982.webp)
