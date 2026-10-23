---
order: 19
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 350eda9b-0fe1-80cf-aa47-d942aafc6bdb
title: MDP에서 Value function에 대한 Bellman equation
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 31deda9b-0fe1-80d6-826b-c54fbb1123ff
    title: 강화학습
  - id: 320eda9b-0fe1-80d1-842c-e609cad65258
    title: 스크래치부터 시작하는 강화학습의 모든것
  - id: 350eda9b-0fe1-80cf-aa47-d942aafc6bdb
    title: MDP에서 Value function에 대한 Bellman equation
excerpt: MRP에서 state가 주어졌을 때 얻게 되는 평균 보상 (R_s = E[R_{t+1} | S_t = s]) --- 식 유도 - MDP는 state transition에 action 도 포함되기 때문에 반드시 action을 고려해야 한다. - 현재 state(S_t)에서 가능한 action(a_t)과 next state(
cover: null
icon: null
notionProperties:
  중요도: No
  상태: 완료
schema_version: 1
parent_id: 320eda9b-0fe1-80d1-842c-e609cad65258
created: 2026-04-28T04:24:27.600Z
updated: 2026-05-09T02:51:54.790Z
legacy_path: Main/강화학습-c54fbb1123ff/스크래치부터 시작하는 강화학습의 모든것-e609cad65258/MDP에서 Value function에 대한 Bellman equation-d942aafc6bdb/index.md
legacy_category: 강화학습
source_url: https://beautiful-college-c84.notion.site/350eda9b0fe180cfaa47d942aafc6bdb
---
<a id="350eda9b0fe180b7ae3aefee2c21caf9"></a>

## MRP에서 state가 주어졌을 때 얻게 되는 평균 보상<br>(<code class="language-math">R&#95;s = E&#91;R&#95;{t&#43;1} &#124; S&#95;t = s&#93;</code>)

---

<a id="350eda9b0fe1806b86f8c2fcf7d5ba97"></a>

### 식 유도

![](1eed8704bfb6c3cf.webp)

- MDP는 state transition에 action 도 포함되기 때문에 반드시 action을 고려해야 한다&#46;

- 현재 state(<code class="language-math">S&#95;t</code>)에서 가능한 action(<code class="language-math">a&#95;t</code>)과 next state(<code class="language-math">S&#95;{t&#43;1}</code>)를 모두 고려하여 Reward를 계산한다&#46;  
    ![](eeb63739f3b09451.webp)

- 결국 ‘<code>policy &#42; transition probability &#42; reward</code>의 평균(expectation)’을 구하는 것이다&#46;
    ![](da7464b7fd74dd15.webp)

    - <code>policy</code>&#58; 현재 state <code class="language-math">s&#95;t</code>에서 특정 행동 <code class="language-math">a&#95;t</code>가 선택될 확률

    - <code>transition probability</code>&#58; 그 행동이 선택되었을 때를 가정하고 <code class="language-math">s&#95;{t&#43;1}</code>로 갈 확률

    - <code>reward</code>&#58; 현재 state <code class="language-math">s&#95;t</code>에서 action <code class="language-math">a&#95;t</code>를 통해 다음 state <code class="language-math">s&#95;{t&#43;1}</code>로 갔을 때의 보상

<a id="350eda9b0fe180799ac5df5df5b0a49a"></a>

### 백업 다이어그램

![](8749381b2bc52734.webp)

- 현재 state <code class="language-math">s&#95;t</code>에서 action <code class="language-math">a&#95;t</code>를 통해 다음 state <code class="language-math">s&#95;{t&#43;1}</code>로 갔을 때의 보상을 <code class="language-math">R(s&#95;t, a&#95;t, s&#95;{t&#43;1})</code>로 표현한 다이어그램이다&#46; 

<a id="345eda9b0fe1804c8e49d10cca6819fd"></a>

## MDP <code class="language-math">&#60;S, A, P, R, &#92;gamma&#62;</code>에서의 Value function에 대한 Bellman equation

---

![](982d7aff1ea31948.webp)

> ✏️ 
> 
> - return 도 random variable이다&#46; 
> 
> - value function은 어떤 <strong>state</strong>가 <strong><u>얼마나 좋거나 나쁜지</u></strong>에 대한 <strong><u>척도</u></strong>이다&#46;
>     - 어떤 state <code class="language-math">V^{&#92;pi}(s&#95;t)</code>가 큰 값이면 해당 state에서는 평균적으로 높은 return 받을 수 있다
> 
>     - return을 많이 받을 수 있는 state가 강화학습에서는 좋은 state이다

<a id="350eda9b0fe1804db22eda9a6bc76deb"></a>

### 유도 방법 1

![](9b4291a05b38c6c7.webp)

- 이전 MRP의 식 유도와 거의 유사하다&#46; 
    - <a href="#/post/345eda9b-0fe1-8053-b55d-f21cc06fd945">페이지</a> 

- 시점 t 에서의 <strong>총 미래 보상</strong> 
    ![](0e894cb30186250a.webp)

- MDP이기 때문에 Action을 고려하여 계산한다&#46;
    ![](2d5b027ef8a59a6e.webp)

<a id="350eda9b0fe180a890b0d1f6e67ee0a6"></a>

### 유도 방법 2

![](f46fd44ffb107bf9.webp)

- 시점 t 에서의 <strong>총 미래 보상</strong> 
    ![](0e894cb30186250a.webp)

- <code class="language-math">a&#95;t</code>, <code class="language-math">s&#95;{t&#43;1}</code> variable 대한 식으로 변형
    ![](a96d62ee5225f381.webp)

- <code class="language-math">s&#95;t</code>, <code class="language-math">a&#95;t</code>, <code class="language-math">s&#95;{t&#43;1}</code> 이 주어지면 Reward function을 계산할 수 있다&#46; <br>즉, 더이상 Random variable이 아닌 <strong><u>상수</u></strong>로써 <code class="language-math">E&#95;{&#92;pi}&#91;…&#93;</code>을 빠져나올 수 있다&#46; 
    ![](086dadf49ec4e284.webp)

- MDP에서는 <code class="language-math">s&#95;{t&#43;1}</code> 이 주어지면 <code class="language-math">a&#95;t</code>, <code class="language-math">s&#95;t</code> 를 생략할 수 있다&#46; 
    ![](db1df72e90c389cb.webp)

    - <code class="language-math">s&#95;{t&#43;1}</code>에  <code class="language-math">a&#95;t</code>, <code class="language-math">s&#95;t</code>의 값이 포함되어 있다&#46; <br>따라서 생략 가능하다&#46;

<a id="350eda9b0fe180b4b105f537c9aaf236"></a>

### 정리 &#45; Bellman equation for Value function (MDP)

![  • 백업 다이어그램: ⁍에서 가능한 ⁍ 를 통해 ⁍ 갔을 경우의 모든Reward(⁍)에 평균값](1e3f451f39ea4bce.webp)

<a id="350eda9b0fe180f7b347e16e7ef51d0f"></a>

### Bellman equation for Value function (MDP)

![](90953023dc0a04b2.webp)

<a id="350eda9b0fe1801180c5ed577f590ce4"></a>

### 예제

![](a96f0ce38291929b.webp)

- <code class="language-math">V(S&#95;1)</code>
    ![](07a557d94f02c677.webp)

- <code class="language-math">V(S&#95;3)</code>
    ![](e3a35bd8b2bf044c.webp)

    - 계산은 위와 동일하기 때문에 생략함
