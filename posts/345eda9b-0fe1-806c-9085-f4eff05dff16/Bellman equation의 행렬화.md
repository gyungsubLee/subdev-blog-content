---
order: 21
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 345eda9b-0fe1-806c-9085-f4eff05dff16
title: Bellman equation의 행렬화
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 31deda9b-0fe1-80d6-826b-c54fbb1123ff
    title: 강화학습
  - id: 320eda9b-0fe1-80d1-842c-e609cad65258
    title: 스크래치부터 시작하는 강화학습의 모든것
  - id: 345eda9b-0fe1-806c-9085-f4eff05dff16
    title: Bellman equation의 행렬화
excerpt: MRP에서 Value function에 대한 Bellman equation의 행렬화 Value function의 Bellman equation을 행렬화하여 가치함수 계산 MRP에 대한 Value function의 Bellman equation에서 위 식의 관계를 만족한다. - MRP에서는 policy가 존재하지 않기 때문
cover: null
icon: null
notionProperties:
  상태: 완료
schema_version: 1
parent_id: 320eda9b-0fe1-80d1-842c-e609cad65258
created: 2026-04-17T07:48:46.764Z
updated: 2026-04-30T06:33:23.864Z
legacy_path: Main/강화학습-c54fbb1123ff/스크래치부터 시작하는 강화학습의 모든것-e609cad65258/Bellman equation의 행렬화-f4eff05dff16/index.md
legacy_category: 강화학습
source_url: https://beautiful-college-c84.notion.site/345eda9b0fe1806c9085f4eff05dff16
---
<a id="352eda9b0fe18076b7aac1dd707ff786"></a>

## <code>MRP</code>에서 <code>Value function</code>에 대한 Bellman equation의 행렬화

<a id="351eda9b0fe1806ba66dd4f7b2d410c2"></a>

### Value function의 Bellman equation을 행렬화하여 가치함수 계산

![](4b9f9e8049b7fbab.webp)

<a id="352eda9b0fe180bc8cb2f2eea69adce9"></a>

MRP에 대한 Value function의 Bellman equation에서 위 식의 관계를 만족한다&#46; 

- MRP에서는 policy가 존재하지 않기 때문에 <code class="language-math">&#92;pi</code> 기호를 생략한다&#46;

![](367f55094bef3646.webp)

- <code class="language-math">&#124;s&#124;</code>
    - Cardinality s

    - s라는 집합에 있는 원소 개수<br>즉, 가능한 모든 state 대한 개수를 의미한다&#46; 

<a id="352eda9b0fe18009af5eed73f364b461"></a>

### 증명

![](a75169607c5144b5.webp)

- <code class="language-math">V(s&#39;) = R(s&#39;) &#43; &#92;gamma &#92;Sigma&#95;{s&#39;} P(s&#39; &#124;s&#39;) V(s&#39;)</code> <br>성립하는 것을 확인할 수 있다&#46; 

<a id="352eda9b0fe180c49b41d13c85d5e78b"></a>

### Value function 계산&#58; <code class="language-math">P</code><code>, </code><code class="language-math">&#92;bar{R}</code><code>  → </code><code class="language-math">V</code>

![](3fec646ec2a76c26.webp)

<details>
<summary>ex) <code class="language-math">P=I, &#92;gamma = 0&#46;9</code></summary>

![](44b90406a149d98a.webp)

- <code class="language-math">P = I</code> 인 경우, 대각선만 1&#46;0이 된다&#46; 
    ![](76e224aa7fb1077f.webp)

    - 동일한 state로 전이하는 재귀 구조만 가능하다&#46;

- <code class="language-math">&#92;bar{R} (S^1)</code>
    ![](f8c8515db4efffc7.webp)

</details>

<a id="352eda9b0fe180d4a6d4c6e48f72e67b"></a>

### 예제

![](632935fe58fccb37.webp)

- <code class="language-math">P</code>, <code class="language-math">&#92;bar{R}</code> 을 통해 Value function을 구할 수 있다&#46; 

<a id="352eda9b0fe180afb72ec6f4ba3f4ec1"></a>

## <code>MDP</code>에서 <code>Value function</code>에 대한 Bellman equation의 행렬화

> ✏️ 
> 
> <a id="352eda9b0fe180e782e3f16b6091a6ce"></a>
> 
> MDP 에서 부터는 policy가 포함된다&#46;

<a id="352eda9b0fe18087aad2f7e74811c7f0"></a>

### MDP에서 Value function에 대한 Bellman equation의 행렬화

![](5329f97a2309b674.webp)

![](61760158eb621902.webp)

- policy에 대한 value function 
    ![](fbce2fff559aeeb3.webp)

- policy에 대한 reward function
    ![](247d4eb9751e07d4.webp)

- policy에 대한 transition probability
    ![](6aa9dae4bd330e82.webp)

<a id="351eda9b0fe1802faf19e3a39b9bbe68"></a>

### Value function 계산 &#45; <code class="language-math">P^{&#92;pi}</code><code>, </code><code class="language-math">&#92;bar{R}^{&#92;pi}</code><code> → </code><code class="language-math">V^{&#92;pi}</code>

![](f444d36bef0793aa.webp)

- 일일이 가능한 리턴을 직접 다 따져보고 가능한 리턴의 확률이 얼마인지 계산 후 평균을 구하는 것이 아닌 

- <code class="language-math">P^{&#92;pi}</code><code>(</code><strong><u><code>트랜지션 프로빌리티)</code></u></strong> 와 <code class="language-math">&#92;bar{R}^{&#92;pi}</code><strong><u><code>(리워드의 함수)</code></u></strong>만 알고있으면 <code class="language-math">V^{&#92;pi}</code><code>(value function)</code>을 구할 수 있다&#46; 

<a id="352eda9b0fe18087a3bcf603cdfd97b2"></a>

### 예제

![](7bd266886a980cdf.webp)

<a id="352eda9b0fe1806db68ddc3f13201e45"></a>

## <code>MDP</code>에서 <code>Action&#45;Value function</code>에 대한 Bellman equation의 행렬화

<a id="352eda9b0fe18055b6f6fd9b9c1c0512"></a>

### MDP에서 Action&#45;Value function의 Bellman equation을 행렬화

![](3b487e218f2dc30a.webp)

![](bc316aef90101d13.webp)

- policy에 대한 Action&#45;Value function
    ![](e1834ab05bb97e30.webp)

- policy에 대한 Reward function
    ![](83848c47431bfd73.webp)

- policy에 대한 Transition Probability
    ![](17c8f6950990d4b3.webp)

    ![](92bd1d8da4f779ae.webp)

<a id="352eda9b0fe1801f8113e05a0d13bbae"></a>

### 증명

![](64e10b7484b32822.webp)

<a id="352eda9b0fe180899e47f7285c62e9af"></a>

### Action&#45;Value function 계산 &#45; <code class="language-math">P^{&#92;pi}</code><code>, </code><code class="language-math">&#92;bar{R}</code><code> → </code><code class="language-math">Q^{&#92;pi} </code>

![](4e20e30cef46709c.webp)

- <code class="language-math">P^{&#92;pi}</code><code>(</code><strong><u><code>트랜지션 프로빌리티)</code></u></strong> 와 <code class="language-math">&#92;bar{R}</code><strong><u><code>(리워드의 함수)</code></u></strong>를 통해 <code class="language-math">Q^{&#92;pi}</code><code>(Action&#45;Value function)</code>을 구할 수 있다&#46;
