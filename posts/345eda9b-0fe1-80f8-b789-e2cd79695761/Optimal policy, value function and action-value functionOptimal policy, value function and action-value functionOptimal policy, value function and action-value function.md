---
order: 11
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 345eda9b-0fe1-80f8-b789-e2cd79695761
title: Optimal policy, value function and action-value functionOptimal policy, value function and action-value functionOptimal policy, value function and action-value function
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 31deda9b-0fe1-80d6-826b-c54fbb1123ff
    title: 강화학습
  - id: 320eda9b-0fe1-80d1-842c-e609cad65258
    title: 스크래치부터 시작하는 강화학습의 모든것
  - id: 345eda9b-0fe1-80f8-b789-e2cd79695761
    title: Optimal policy, value function and action-value functionOptimal policy, value function and action-value functionOptimal policy, value function and action-value function
excerpt: "Better policy 에 대한 표현 - \\pi_1 ≥ \\pi_2 일때 모든 상태 S에 속하는 state s 에 대해서 \\pi_1의 value 가 항상 \\pi_2의 value 보다 크다 - 필요 충분 조건 - optimal policy \\pi_* - 가장 큰 \\pi ( max_{\\pi} ) - \\pi_* ≥ \\pi - "
cover: null
icon: null
notionProperties:
  상태: 완료
schema_version: 1
parent_id: 320eda9b-0fe1-80d1-842c-e609cad65258
created: 2026-04-17T07:48:23.407Z
updated: 2026-05-20T11:18:42.981Z
legacy_path: Main/강화학습-c54fbb1123ff/스크래치부터 시작하는 강화학습의 모든것-e609cad65258/Optimal policy, value function and action-val-e2cd79695761/index.md
legacy_category: 강화학습
source_url: https://beautiful-college-c84.notion.site/345eda9b0fe180f8b789e2cd79695761
---
<a id="35beda9b0fe1807e99f9c824809ee3a8"></a>

### Better policy 에 대한 표현

![](d3bc8f013b90797d.webp)

- <code class="language-math">&#92;pi&#95;1</code> ≥ <code class="language-math">&#92;pi&#95;2</code> 일때 모든 상태 S에 속하는 state s 에 대해서 <code class="language-math">&#92;pi&#95;1</code><code>의 value</code> 가 항상 <code class="language-math">&#92;pi&#95;2</code><code>의 value</code> 보다 크다 
    - 필요 충분 조건

![](2b95f0d65c7cf291.webp)

- optimal policy <code class="language-math">&#92;pi&#95;&#42;</code> 
    - 가장 큰 <code class="language-math">&#92;pi</code>  ( <code class="language-math">max&#95;{&#92;pi}</code> )

    - <code class="language-math">&#92;pi&#95;&#42;</code> ≥ <code class="language-math">&#92;pi</code> 

- optimal value function <code class="language-math">V^&#42;</code>
    - policy <code class="language-math">&#92;pi</code> 에 대해서 얻을 수 있는 가장 큰 value function

    - <code class="language-math">V^&#42;(s) = max&#95;{&#92;pi} V^{&#92;pi}(s)</code>

- optimal action&#45;value function <code class="language-math">Q^&#42;</code>
    - policy <code class="language-math">&#92;pi</code> 에 대해서 얻을 수 있는 가장 큰 action&#45;value function

    - <code class="language-math">Q^&#42;(s,a) = max&#95;{&#92;pi} Q^{&#92;pi}(s, a)</code>

<a id="35beda9b0fe1804eb4aec6598caf2d6c"></a>

### 이론 (Theorem)

> optimal policy <code class="language-math">&#92;pi&#95;&#42;</code>, optimal value function <code class="language-math">V^&#42;</code>, optimal action&#45;value function <code class="language-math">Q^&#42;</code> 에 대해서 아래 이론(Theorem)이 성립한다&#46; 

![](f73af57c95f57699.webp)

1. 어떤 MDP에 대해서 optimal policy <code class="language-math">&#92;pi&#95;&#42;</code> 는 하나 이상 존재한다&#46; 

1. 모든 optimal policy <code class="language-math">&#92;pi&#95;&#42;</code> 는 모두 optimal value function <code class="language-math">V^&#42;</code> 을 가진다&#46; 

1. 모든 optimal policy <code class="language-math">&#92;pi&#95;&#42;</code> 는 모두 optimal action&#45;value function <code class="language-math">Q^&#42;</code> 을 가진다&#46; 

> 어떤 MDP에 대해서든지  optimal policy <code class="language-math">&#92;pi&#95;&#42;</code> , optimal value function <code class="language-math">V^&#42;</code>, optimal action&#45;value function <code class="language-math">Q^&#42;</code>에 대해서 아래 이론이 성립함

> 만약 optimal action&#45;value function이 주어졌다면, optimal policy를 쉽게 찾을 수 있다&#46;

![](35414041363ed7c2.webp)

- 어떤 MDP라도, deterministic optimal policy를 갖고 있다&#46;

<a id="35beda9b0fe180eb881ecd2ca13826d8"></a>

### Deterministic optimal policy의 예시

![](8d5c1a0ea2d76e34.webp)

- 빨간색 화살표의 방향으로 행동을 취해 가장 빠르게 최대 보상을 얻을 수 있음

<a id="35beda9b0fe180b9b591fa424cc33067"></a>

### Bellman optimality equation <u>for Value function</u>

![](eac4b15e50bae6bd.webp)

- 주어진 state s에서 optimal value (가장 높은 값)은 optimal value function에서 가장 좋은 action을 고른 것과 같다&#46; 

![  • 백업 다이어그램: Bellman optimality equation for Value function](f725ff7a1862643d.webp)

- <code class="language-math">R(s, a, s&#39;) &#43; &#92;gamma V^&#42;(s&#39;)</code><code>의 평균값</code>이  max가 되는 action a를 선택한다&#46; 

<a id="35beda9b0fe1801391e7e5f0c0b8f27a"></a>

### 비교&#58; Value function에 대한 Bellman <u>optimality</u> equation, Bellman equation

> ✏️ 
> 
> <a id="35beda9b0fe180ca925ffae46d432b84"></a>
> 
> Bellman optimality equation 은 최대의 action만을 고려한 값이기 때문에 <code class="language-math">&#92;Sigma&#95;{a&#95;{t}}</code><code> → </code><code class="language-math">max&#95;a</code> 가 된다&#46; 

<a id="35beda9b0fe18035b360e67803cd9aa7"></a>

#### Bellman optimality equation for Value function

![](4ae677e17f26a6bd.webp)

<a id="35beda9b0fe180fe9625c32933f05e72"></a>

#### Bellman equation for Value function

![](a1a970c6758f6c6e.webp)

<a id="35beda9b0fe18046a68dc50cf277e965"></a>

### Bellman optimality equation <u>for Action&#45;Value function</u>

<a id="35beda9b0fe1805c9967cb42cfb6dd52"></a>

<strong>Bellman equation for Action&#45;Value function</strong>

![](17a3b2d6cb1a79b7.webp)

<a id="35beda9b0fe18089b54de20b3d44ee12"></a>

<strong>Bellman </strong><strong><u>optimality</u></strong><strong> equation for Action&#45;Value function</strong>

![](caf1325d4d9bddc9.webp)

- 최대화하는 action  값에 대한 action&#45;value function

![  • 백업 다이어그램](e5aaeaabb6e7f82f.webp)

1. s, a 에서 트랜지션이 먼저 발생 → s’으로 가는 다양한 경우의 수가 존재
    - 이 트랜지션은 환경에 의한 것으로 에이전트가 컨트롤할 수 없음
        - 트랜지션 발생 후 보상까지 컨트롤 x

1. 이후 어떤 행동을 취할 지 에이전트가 컨트롤 가능함<br>그 중 항상 Optimal value function을 최대화하는 action을 고름

<a id="35beda9b0fe180f4b039c4d34ded9747"></a>

#### Bellman optimality equation은 <u>non&#45;linear equation</u>으로, 행렬화가 불가능하다&#46; 

<a id="35beda9b0fe1808887d8e01b17245a6c"></a>

#### Bellman optimality equation은 

![](f69cd045a17a88af.webp)

- 왜 행렬화가 불가능한가? 
    <a id="35beda9b0fe1808ca848f6eaf9360bf3"></a>

    즉, 왜 non&#45;linear equation인가? 

![](f95b2cb2048e29db.webp)

- bellman equation은 행렬화를 통해 풀 수 있지만, 매우 많은 계산 비용이 든다&#46; 

- 많은 컴퓨팅 자원이 필요하며 현실적으로 어렵다&#46; 
    - 비효율적인 듯 함

<a id="35beda9b0fe18070ac3be01db58a67ba"></a>

### Bellman optimality equation 예제

![](b95a7ec9152e5d7f.webp)

- <strong>Value function에 대한 bellman optimality equation</strong>
    ![](c4a765271eb1a374.webp)

    ![](6539d8277a4ea5df.webp)

    - 각 state에서 action에 대한 value function의 max 값을 적용한다&#46; 

    - <code class="language-math">V^&#42;</code> 값을 알지 못하기 때문에 현재는 구할 수 없음 

- <strong>Action&#45;Value function에 대한 bellman optimality equation</strong>
    ![](a7931967b493a468.webp)

    - 각 state에서 action에 대한 action&#45;value function의 max 값을 적용한다&#46; 

    - <code class="language-math">Q^&#42;</code> 값을 알지 못하기 때문에 현재는 구할 수 없음
