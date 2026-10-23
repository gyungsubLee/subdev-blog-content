---
order: 9
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 340eda9b-0fe1-812c-a3f0-f7146c5e83ef
title: DP를 활용한 policy evaluation 계산
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 31deda9b-0fe1-80d6-826b-c54fbb1123ff
    title: 강화학습
  - id: 320eda9b-0fe1-80d1-842c-e609cad65258
    title: 스크래치부터 시작하는 강화학습의 모든것
  - id: 340eda9b-0fe1-812c-a3f0-f7146c5e83ef
    title: DP를 활용한 policy evaluation 계산
excerpt: "Dynamic Programming을 활용한 policy evaluation: Iterative Policy Evaluation --- 🤔 Policy evaluation 임의의 policy \\pi 의 value function V^{\\pi}를 계산하는 방법을 의미 🤔 Dynamic programming - 1950 "
cover: null
icon: null
notionProperties:
  AE<<: 🧐 질문,복습
  태그: Policy Evaluation
  상태: 완료
schema_version: 1
parent_id: 320eda9b-0fe1-80d1-842c-e609cad65258
created: 2026-04-12T14:17:59.380Z
updated: 2026-05-20T11:54:36.825Z
legacy_path: Main/강화학습-c54fbb1123ff/스크래치부터 시작하는 강화학습의 모든것-e609cad65258/DP를 활용한 policy evaluation 계산-f7146c5e83ef/index.md
legacy_category: 강화학습
source_url: https://beautiful-college-c84.notion.site/340eda9b0fe1812ca3f0f7146c5e83ef
---
<a id="35beda9b0fe18033a638cdc0850b5aa9"></a>

## Dynamic Programming을 활용한 policy evaluation&#58; <code>Iterative Policy Evaluation</code>

---

> 🤔 
> 
> <a id="35beda9b0fe1806a88faebbc48cddc67"></a>
> 
> <strong>Policy evaluation</strong>
> 
> <a id="35beda9b0fe1805db8d0e333adf8cb32"></a>
> 
> 임의의 policy <code class="language-math">&#92;pi</code> 의 value function <code class="language-math">V^{&#92;pi}</code>를 계산하는 방법을 의미

> 🤔 
> 
> <a id="35beda9b0fe180efb941eca2d113c5ff"></a>
> 
> <strong>Dynamic programming</strong>
> 
> - 1950 Richard Bellman에 의해 고안된 최적화 방법
> 
> - 크고 복잡한 문제를 <strong>작은 문제로 쪼개고 되풀이 되는(recursive) 형태로 푸는</strong> 방법론
>     ![  • 해당 내용만이 DP의 정의가 아님](bcd28fa90b7d71f7.webp)
> 
>     - <code>Total&#95;Cost n</code> = <code>Total&#95;Cost n&#45;1</code> &#43; <code>Cost n</code>

<a id="35beda9b0fe1803ea7c7f3efcbcb401e"></a>

### Dynamic Programming을 활용한 policy evaluation

> 
> 
> <a id="35beda9b0fe180c48caac53afc71e7ce"></a>
> 
> <strong>Bellman equation for Value function (MDP)</strong>
> 
> ![](7ea5f19c49f46d7d.webp)

> 해당 알고리즘을 <code>iterative policy evaluation</code>이라 한다&#46; 

1.  <strong>모든 state</strong>에 대해 정의된 임의의 <strong>value function</strong>을 만든다&#46; <br>(보통 table 혹은 array로 만듦)
    ![](3e4c7ff7a3a98b10.webp)

1.  Value function에 대한 <strong>Bellman equation</strong>을 이용해 아래와 같이 Value function을 <strong>업데이트</strong> 한다&#46; 
    ![](692a01c08db27d29.webp)

    - <code class="language-math">V&#95;k(s&#39;)</code> 를 통해서 <code class="language-math">V&#95;{k&#43;1}(s)</code>을 만드는 과정이다&#46;

1.  계속해서 <code>2</code>를 반복하다가, <strong><u>충분히 수렴</u></strong>했다고 판단되면 멈춘다&#46; 
    - 미리 설정한 threshold 값  이하로 Value function의 변화량이 낮아질 때
        ![](13431a5e0bed16b2.webp)



- 충분히 수렴했다는 것은 어떻게 판단할 수 있나?
    - 미리 설정한 threshold 값  이하로 Value function의 변화량이 낮아질 때 수렴했다고 판단한다&#46; 
        <a id="366eda9b0fe180c58b3ac7044a773172"></a>

        ⇒ k를 계속 증가시키면서 V를 업데이트(<code class="language-math">max&#95;a &#124;V&#95;k(s) &#45; V&#95;{k&#45;1}(s)&#124;</code>) 하는데 이 값이 <code class="language-math">&#92;delta</code> 이하로 떨어지면 변화량이 작기 때문에 거의 수렴했다고 판단하는 것이다&#46;

        <a id="366eda9b0fe180e9b7f3c617edea7e20"></a>

        ⇒ <code class="language-math">max&#95;a &#124;V&#95;k(s) &#45; V&#95;{k&#45;1}(s)&#124; &#60; &#92;delta</code>

- <code class="language-math">V&#95;k</code> 가 <code class="language-math">V^{&#92;pi}</code> 와 비슷해진다는 것을 어떻게 판단하는가?
    - 만약 <code class="language-math">&#92;gamma &#60; 1</code> 이고 <code>2</code>를 <strong><u>무한히 반복</u></strong>한다면, <strong>실제</strong> Value function <code class="language-math">V^{&#92;pi}</code> 에 수렴한다&#46;
        - 이론적으로 증명됨 

    - 이를 수학적으로 표현한 것이 아래와 같다&#46; 
        ![](08607570cf16d3c9.webp)

    - 그러나 실제 상황에서는 무한히 반복할 수 없다&#46; 

<a id="35beda9b0fe1809d8fb1fd6f47d05f21"></a>

### iterative policy evaluation

![](302d646b6cb73982.webp)

1. policy 정의
    ![](2f5fec0579998705.webp)

    - 해당 policy로 value function을 계산하는 것이 목적이다&#46;

1. value function 초기화
    ![](488e21fd12aaf4e0.webp)

    - 환경에 존재하는 모든 state에 대해서 value function의 값을 초기화한다&#46; 

    - 0 혹은 어떤 랜덤한 실수로 설정해도 괜찮다&#46; 

1. 변수 설정
    ![](1725be8e5ec475e6.webp)

    - 충분히 수렴했다는 것을 확인하기 위한 <code class="language-math">&#92;delta </code> 값을 양수로 설정

    - policy evaludation이 진행되는 동안 value function의 변화량 중 가장 큰 값을 저장하기 위한 변수 <code class="language-math">&#92;Delta</code> 를 <code class="language-math">&#92;delta </code> 와 같게 설정한다&#46; 
        - <code class="language-math">&#92;Delta  = &#92;delta</code> ( 대문자 델타 = 소문자 델타 )

    - value function이 얼마나 evaluation 됐는지 나타내는 k는 0으로 초기화한다&#46; 

1. While 문부터 policy evaluation이 시작된다&#46; 
    ![](71e3b9d82614b95c.webp)

    - <code class="language-math">&#92;Delta</code>가 <code class="language-math">&#92;delta</code>(thredhold) 보다 크거나 같다면 충분히 수렴하지 않았다고 판단하고 policy evaluation 반복해서 진행한다&#46; 

    - policy evaluation 시작 시, value function의 변화량 중 가장 큰 값을 저장하기 위한 <code class="language-math">&#92;Delta</code>는 0으로 초기화한다&#46; 

<a id="35beda9b0fe18041a380f126eca40799"></a>

### DP(Dynamic Programming)을 활용한 iterative policy evaluation의 특징

![](f3558d62aea7a8d7.webp)

1. 환경의 <strong>MDP 모델</strong>을 알아야 한다&#46;
    - bellman equation을 구하기 위해서는 <code>transition probability</code>가 필요하고 <code>reward function</code>도 필요하다 

    - 위 2개가 모두 MDP에 속한 요소이기 때문이다&#46; <br>즉, MDP 모델을 알아야 한다&#46;

1. <strong>State space</strong>가 <strong><u>너무 큰 경우</u></strong>에는 Computation이 많이 요구되므로 사용하기 어려움&#46;
    - 모든 state에 대해서 반복하기 때문에 state 개수가 많아지면 계산해야 될 양이 굉장히 많아진다&#46; 
        - O(<code class="language-math">n^2</code>)으로 연산량 증가
