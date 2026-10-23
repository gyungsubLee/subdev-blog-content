---
order: 24
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 340eda9b-0fe1-8068-9b3c-f1a707f244c0
title: 마르코프 보상 과정 (Markov Reward Process)
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 31deda9b-0fe1-80d6-826b-c54fbb1123ff
    title: 강화학습
  - id: 320eda9b-0fe1-80d1-842c-e609cad65258
    title: 스크래치부터 시작하는 강화학습의 모든것
  - id: 340eda9b-0fe1-8068-9b3c-f1a707f244c0
    title: 마르코프 보상 과정 (Markov Reward Process)
excerpt: 마르코프 보상 과정 (Markov Reward Process) --- - 마르코프 과정(Markov Process)에 R, \gamma 가 추가된 형태이다. - S, P 까지는 마르코프 과정(Markov Process) 과 동일 🧐 from → to - 마르코프 가정에서의 개념을 표현한다. - 다음 state 값을 구하
cover: null
icon: null
notionProperties:
  상태: 완료
schema_version: 1
parent_id: 320eda9b-0fe1-80d1-842c-e609cad65258
created: 2026-04-12T14:20:38.451Z
updated: 2026-04-28T02:57:41.905Z
legacy_path: Main/강화학습-c54fbb1123ff/스크래치부터 시작하는 강화학습의 모든것-e609cad65258/마르코프 보상 과정 (Markov Reward Process)-f1a707f244c0/index.md
legacy_category: 강화학습
source_url: https://beautiful-college-c84.notion.site/340eda9b0fe180689b3cf1a707f244c0
---
<a id="340eda9b0fe1804c87efd9d14c071e13"></a>

## 마르코프 보상 과정 (Markov Reward Process)

---

![](97e9753383e72b81.webp)

- 마르코프 과정(Markov Process)에 <code>R</code>, <code class="language-math">&#92;gamma</code> 가 추가된 형태이다&#46; 
    - S, P 까지는 마르코프 과정(Markov Process) 과 동일

<details>
<summary>🧐 from → to</summary>

![](1f09e5bd0e11195c.webp)

- 마르코프 가정에서의 개념을 표현한다&#46; 
    - 다음 state 값을 구하기 위해서는 이전 state 값이 있어야 한다&#46; 

- 이전 state(from)에서 다음 state(to)로 진행

</details>

<details>
<summary><code class="language-math">R</code> (Reward function)</summary>

<a id="341eda9b0fe180f6ab10ce2fd547d231"></a>

아래의 2가지 방법으로 표현된다&#46; 

1. <code class="language-math">S</code> 2개
    ![](9506db14a36cc6ee.webp)

    - s, s’ 둘 다 input으로 들어가는 경우

    - 두 state간의 차이 값을 보상으로 주는 경우에 많이 사용한다&#46; 

    - 아래의 S 1개의 경우를 포함한다&#46; 
        - s의 값을 무시한 채로 s’ 만을 인자로 줘 계산한다면 아래와 같다&#46; 

    - ex) s가 온도라고 했을 때, 어떤 두 state 간의 온도 차이를 보상으로 준다고 가정하면 <br>       s, s’ 두개의 인자 값이 필요하다&#46; 

1. <code class="language-math">S</code> 1개
    ![](787c02b565f07f43.webp)

    - to state 만 가지고 보상을 계산한다&#46; <br>즉, 어느 state에 도달하기만 하면 그 state를 기반으로 보상을 계산한다는 말이다&#46;

    - ex) 어떤 목적지에 주어지는 보상 같은 경우, 그 목적지에 도달했는지 아닌지 여부만 체크해 보상을 계산할 수 있다&#46;

1. 상태 s에서 기대되는 즉시 보상(expected immediate reward)
    ![](e7338d516d8bc8b0.webp)

    - 현재 상태 s에서 출발했을 때, <strong>다음 상태로 이동</strong>하면서 받는 보상의 <u>평균값</u>
        - <code class="language-math">R&#95;s = &#92;mathbb{E}&#91;R&#95;{t&#43;1} &#124; S&#95;t = s&#93;</code>
            - 현재 상태가 s일 때, 다음 timestep에서 받는 보상 <code class="language-math">R&#95;{t&#43;1}</code> 의 기댓값

        - <code class="language-math">P(s&#39; &#124; s)</code>
            - 상태 s에서 s&#39;로 갈 확률

            - Markov 성질&#58; 오직 현재 상태만 영향

        - <code class="language-math">R(s, s&#39;)</code>
            - 상태 s → s&#39;로 이동할 때 받는 보상

            - deterministic(결정론적)일 수도 있고 stochastic(확률론적)일 수도 있음<br><br>

    - 예시 1
        ![](b4b99f801368d95b.webp)

        <a id="342eda9b0fe1804e8233c41ca23c89d2"></a>

        ⇒ <code class="language-math">R&#95;s = 0&#46;2 &#92;cdot 1 &#43; 0&#46;8 &#92;cdot 2 = 0&#46;2 &#43; 1&#46;6 = 1&#46;8</code>

        <a id="342eda9b0fe18032ab89c8fc67503de6"></a>

        ⇒ <strong><u>상태 s의 기대 보상 = 1&#46;8</u></strong>

    - 예시 2
        | <strong>다음 상태 </strong>s&#39; | <strong>확률 </strong>P(s&#39;&#124;s) | <strong>보상 </strong>R(s, s&#39;) |
        | --- | --- | --- |
        | s1 | 0&#46;7 | &#43;10 |
        | s2 | 0&#46;3 | &#45;5 |

        <a id="342eda9b0fe180dcaec8f5d2fae54b21"></a>

        ⇒ <code class="language-math">R&#95;s = 0&#46;7 &#92;cdot 10 &#43; 0&#46;3 &#92;cdot (&#45;5) = 7 &#45; 1&#46;5 = 5&#46;5</code>

        <a id="342eda9b0fe1805d9dabcd8ddce7d384"></a>

        ⇒ <strong><u>상태 s의 기대 보상 = 5&#46;5</u></strong>

</details>

<details>
<summary>🧐 MDP 에서 의미하는 ‘평균’ 이란?</summary>

---

<details>
<summary>일반적인 평균 &#45; 모든 경우의 수가 동일한 확률값</summary>

> <code class="language-math">&#92;text{평균} = &#92;frac{x&#95;1 &#43; x&#95;2 &#43; &#46;&#46;&#46; &#43; x&#95;n}{n}</code>

<a id="342eda9b0fe180878e1af09339a6cd46"></a>

 일반적으로 말하는 평균은 위와 같다&#46; 

<a id="342eda9b0fe1801eb3b4ecb7a91a2aa8"></a>

그러나 이건 <strong>모든 경우가 </strong><strong><u>동일한 확률</u></strong>일 때만 성립하는<strong> </strong><strong><u>‘특수한 평균’</u></strong><strong> </strong>이다&#46;

</details>

<details>
<summary>MRP(Markov Reward Process)에서 사용하는 <strong>평균 = 기대값</strong></summary>

>  <code class="language-math">&#92;text{기대값} = &#92;sum (&#92;text{확률} &#92;times &#92;text{값})</code>

<a id="342eda9b0fe180e3bc5fc10eca69d643"></a>

MRP에서의 수식(<code class="language-math">R&#95;s = &#92;sum&#95;{s’} P(s’&#124;s) R(s, s’)</code>)은 사실 위와 같다&#46; 

<a id="342eda9b0fe18048a1a3d1c7bdf11aaa"></a>

즉, 평균이라 하지만 <strong>‘나누기 n’ 이 보이지 않</strong>는다&#46; 

</details>

<details>
<summary><strong>균등 분포 (우리가 아는 평균) </strong></summary>

| <strong>값</strong> | <strong>확률</strong> |
| --- | --- |
| <code>10</code> | <code>0&#46;5</code> |
| <code>20</code> | <code>0&#46;5</code> |

<a id="342eda9b0fe1802c9bf4d886cfe24508"></a>

<code class="language-math">= 0&#46;5 &#92;cdot 10 &#43; 0&#46;5 &#92;cdot 20 = 15</code>

<a id="342eda9b0fe1803a827cf88087f86e34"></a>

이걸 풀면 아래와 같다&#46; 

<a id="342eda9b0fe1806db77fe766e7c7d2db"></a>

= <code class="language-math">&#92;frac{10 &#43; 20}{2}</code>

<a id="342eda9b0fe180c5998eeb715ea4d49b"></a>

즉, 확률이 <code class="language-math">&#92;frac {1}{n}</code>이라 나누기 <code>n</code>과 동일해 진 것이다&#46; 

</details>

<details>
<summary><strong>일반 확률 분포 (MRP 상황)</strong></summary>

| <strong>값</strong> | <strong>확률</strong> |
| --- | --- |
| <code>10</code> | <code>0&#46;7</code> |
| <code>&#45;5</code> | <code>0&#46;3</code> |

<a id="342eda9b0fe1807aa1adc50b156ee10e"></a>

<code class="language-math">= 0&#46;7 &#92;cdot 10 &#43; 0&#46;3 &#92;cdot (&#45;5) = 5&#46;5</code>

<a id="342eda9b0fe18038a072d590b39c3809"></a>

여기서는 <strong><u>확률이 다르기</u></strong> 때문에 그래서 <strong><u>단순 평균 (n으로 나누기)</u></strong><strong><u>이 아니라</u></strong><br><strong>가중 평균(weighted average)</strong>으로 계산한다&#46; 

</details>

<a id="342eda9b0fe18042a175c75c122a019a"></a>

### 정리

- <strong>일반 평균 </strong>→ 모든 경우를 똑같이 취급

- <strong>기대값 (MRP) → 자주 발생하는 경우는 더 크게 반영</strong>

<a id="342eda9b0fe18093a16dfe89d4e47808"></a>

⇒  <strong>MRP에서의 “평균”</strong><strong> = </strong><strong>가중 평균(weighted average)</strong><strong> = </strong><strong>기대값(expected value)</strong>

<a id="342eda9b0fe1808d979af42a30efc97b"></a>

그래서 단순 평균이 아닌 <strong><u>현실에서 실제로 기대되는 값</u></strong>을 사용한다&#46; <br>즉, <strong><u>확률을 고려한 평균(= 기대값), 가중 평균</u></strong>을 사용한다&#46; 

<a id="342eda9b0fe180538990c2d7bc0272d3"></a>

MRP는 <strong><u>확률적 시스템</u></strong>이기 때문에 <u>어떤 상태는 자주 발생</u>하며 <u>어떤 상태는 거의 안 발생</u>한다&#46; 

</details>

<details>
<summary><code class="language-math">&#92;gamma</code> (Discount factor)</summary>

- 0 ≤ <code class="language-math">&#92;gamma</code> ≤ 1 의 값

</details>

<details>
<summary><strong>&#91; 복습&#93; 🧐 왜 </strong><strong><code>discount factor(</code></strong><code class="language-math">&#92;gamma</code><strong><code>)</code></strong><strong>를 사용하는가?</strong></summary>

![](8c8b376563b5c874.webp)

1. Return이 <strong><u>무한한 값을 가지지 않고 수렴</u></strong>하도록 하여 수학적인 안정성을 준다&#46; 

1. 지금 당장의 보상 혹은 먼 미래의 보상에 대한 가중치
    - <code>Discount factor</code>가 <strong><u>작</u></strong><strong>을수록</strong>, <strong>지금 당장 받는 보상이 return에 많이 포함</strong>

    - <code>Discount factor</code>가 <strong><u>클</u></strong>수록, <strong>나중에 받는 보상이 return에 많이 포함</strong>

1. 만약 환경에서 존재 가능한 모든 sequence (episode)가 유한하다면, <code class="language-math">&#92;gamma</code><code> = 1</code>로 설정 가능
    - 에피소드나 시퀀스의 길이가 유한하다면 즉, 리턴을 계산할 때 보상이 무한하게 더해지지 않고 유한하게 더해진다&#46; 

    - 이때는 <code class="language-math">&#92;gamma</code> 는 1로 설정해도 된다&#46; 

    - episode 
        - 환경과 상호작용에 관련되 모든 정보의 배열이다&#46;

        - state, action, reward 포함

</details>

<details>
<summary>마르코프 보상 과정 (Markov Reward Process) 예시</summary>

<a id="341eda9b0fe180e6ae51fa2ccc084628"></a>

<strong>예시 문제</strong>

![](dae3266056325b03.webp)

<a id="341eda9b0fe180ba88bbd60c4772f9cd"></a>

아래와 같이 진행하여 시험 통과

![](323adedda6ada838.webp)

- return 값 계산
    ![](7b2b3354804ae060.webp)

- Transition probability metrix(model)  계산
    ![](65e8ceee91c182f6.webp)

</details>

<details>
<summary>현실에서의 Markov Reward Process 예시</summary>

- 예시 1) 로또 복권
    ![](ffdbf3723003198f.webp)

    ![](c003df7d4f5a8606.webp)

    - 이전과 같이 state 와 transition probability는 모두동일하다&#46; 

</details>
