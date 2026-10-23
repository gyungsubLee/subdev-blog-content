---
order: 20
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 345eda9b-0fe1-8053-b55d-f21cc06fd945
title: MRP에서 Value function에 대한 Bellman equation
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 31deda9b-0fe1-80d6-826b-c54fbb1123ff
    title: 강화학습
  - id: 320eda9b-0fe1-80d1-842c-e609cad65258
    title: 스크래치부터 시작하는 강화학습의 모든것
  - id: 345eda9b-0fe1-8053-b55d-f21cc06fd945
    title: MRP에서 Value function에 대한 Bellman equation
excerpt: "[사전 개념] Random Variable X의 평균에 대한 Y 표현 --- ✏️ random variable X의 Expectation(평균)이 Y 라는 새로운 variable에 대해서 위 수식과 같이 표현될 수 있다. - 전확률 법칙 기반의 기댓값 분해 (Law of Total Expectation) 식 유도 🧐 ["
cover: null
icon: null
notionProperties:
  중요도: No
  상태: 완료
schema_version: 1
parent_id: 320eda9b-0fe1-80d1-842c-e609cad65258
created: 2026-04-17T07:35:08.523Z
updated: 2026-05-09T02:51:44.215Z
legacy_path: Main/강화학습-c54fbb1123ff/스크래치부터 시작하는 강화학습의 모든것-e609cad65258/MRP에서 Value function에 대한 Bellman equation-f21cc06fd945/index.md
legacy_category: 강화학습
source_url: https://beautiful-college-c84.notion.site/345eda9b0fe18053b55df21cc06fd945
---
<a id="345eda9b0fe180fea190cfbdadde3af4"></a>

## &#91;사전 개념&#93;  Random Variable X의 평균에 대한 Y 표현

---

![](e68036e753e9af08.webp)

> ✏️ 
> 
> <a id="350eda9b0fe180faad8df2ba9e1d00c9"></a>
> 
> random variable X의 Expectation(평균)이 Y 라는 새로운 variable에 대해서 위 수식과 같이 표현될 수 있다&#46;
> 
> - <strong>전확률 법칙 기반의 기댓값 분해 (Law of Total Expectation)</strong>

<a id="350eda9b0fe180419e33ee3a03d0cb02"></a>

### <strong>식 유도 </strong>

![](74d65ca7be5c3068.webp)

<details>
<summary>🧐 &#91;의문점&#93; <code>균등 분포</code>와 <u><code>일반 확률 분포</code></u>의 차이</summary>

<a id="350eda9b0fe180e0bab6ebc9ae430aed"></a>

### <strong>균등 분포 (일반적으로 아는 평균) </strong>

| <strong>값</strong> | <strong>확률</strong> |
| --- | --- |
| <code>10</code> | <code>0&#46;5 (1/2)</code> |
| <code>20</code> | <code>0&#46;5 (1/2)</code> |

<a id="350eda9b0fe180248ba4e2cb5b6f0b47"></a>

<code class="language-math">= &#92;frac{1}{2} &#92;cdot 10 &#43; &#92;frac{1}{2} &#92;cdot 20</code>

<a id="350eda9b0fe1808081bdd971f3433b5b"></a>

= <code class="language-math">&#92;frac{10 &#43; 20}{2}</code>

<a id="350eda9b0fe1801b850cf9ae20371199"></a>

<code class="language-math"> = 15</code>

<a id="350eda9b0fe18056ab85fe6875fde886"></a>

즉, 확률이 <code class="language-math">&#92;frac {1}{n}</code>이라 나누기 <code>n</code>과 동일해 진 것이다&#46; 

<a id="350eda9b0fe18066b86fef3c775a43a9"></a>

### <strong>일반 확률 분포  &#45; </strong><strong>가중 평균(weighted average)</strong><strong>을 통한 평균 계산</strong>

| <strong>값</strong> | <strong>확률</strong> |
| --- | --- |
| <code>10</code> | <code>0&#46;7</code> |
| <code>&#45;5</code> | <code>0&#46;3</code> |

<a id="350eda9b0fe180829b9cc29c0e684e35"></a>

<code class="language-math">= 0&#46;7 &#92;cdot 10 &#43; 0&#46;3 &#92;cdot (&#45;5) = 5&#46;5</code>

<a id="350eda9b0fe180518ddfe1ec9e9ecf0d"></a>

여기서는 <strong><u>확률이 다르기</u></strong> 때문에 그래서 <strong><u>단순 평균 (n으로 나누기)</u></strong><strong><u>이 아니라 각각 요소들의 확률인 </u></strong><br><strong>가중 평균(weighted average)</strong>으로 계산한다&#46; 

<a id="350eda9b0fe180339c9bdbeb283380f8"></a>

<br>

</details>

<a id="350eda9b0fe1800e863de33ad8150087"></a>

일반적으로 흔히 아는 발생 확률이 모두 동일한 균등 분포의 방식으로 평균을 구하는 것이 아닌

<a id="350eda9b0fe18006a64df0821061afff"></a>

각 경우마다 발생 확률이 다른 <strong><u>가중 확률</u></strong>로  평균을 구하는 일반 확률 분포로 평균값을 구한다&#46;

<a id="350eda9b0fe180d2ab7ad978e4202fd5"></a>

<code class="language-math">⇒ E&#91;x&#93; = &#92;Sigma&#95;x P(x)x</code>

<details>
<summary><strong>전확률 법칙 기반의 기댓값 분해 (Law of Total Expectation)</strong></summary>

> <code class="language-math">E&#91;X&#93; = &#92;sum&#95;{y} p(y) E&#91;X &#92;mid y&#93;</code>

<a id="345eda9b0fe180edabdae64d3f57c472"></a>

<strong>구성요소</strong>

- <code class="language-math">p(y)</code>&#58; 특정 조건 y가 발생할 확률

- <code class="language-math">E&#91;X &#124; y&#93;</code>&#58; 그 조건에서의 평균값

<a id="345eda9b0fe1805e845bea01499fb945"></a>

<strong>의미</strong>

- <strong>전체 평균 = (각 상활별 평균) x (그 상활이 일어날 확률)의 합</strong>

<a id="345eda9b0fe1800499efe459d8b00201"></a>

<strong>Value Function과의 연결</strong>

<a id="345eda9b0fe180d2b973e8d1b4ee0cde"></a>

강화학습 에서는 해당 식이 아래와 같이 쓰인다&#46; 

> <code class="language-math">V(s) = &#92;sum &#92;pi(a &#92;mid s) Q(s, a)</code>

- 상태(<code>s</code>)의 가치는 <br>가능한 행동들의 가치(<code class="language-math">Q(s, a)</code>)를<br>정책 확률(<code class="language-math">&#92;pi(a &#92;mid s)</code>)로 <br>가중 평균한 것을 말한다&#46; 

<a id="345eda9b0fe1807c8d18d774894770a1"></a>

<strong>예시</strong>

- 상황
    - 상태 s에서 행동 2개
        - a1&#58; 70% → 보상 기대값 10

        - a2&#58; 30% → 보상 기댓값 2

- 계산
    - <code class="language-math">V(s) = 0&#46;7 &#42; 10 &#43; 0&#46;3 &#42; 2 = 7 &#43; 0&#46;6 = 7&#46;6</code>

</details>

<a id="34eeda9b0fe18089b2cae14f4ac560e6"></a>

## MRP <code class="language-math">&#60;S, P, R, &#92;gamma&#62;</code>에서 Value function에 대한 Bellan equation

---

<a id="350eda9b0fe1803fa923d6f2a1f67a50"></a>

### <strong>유도 방법 1</strong>

![](a16b2658efc3adc8.webp)

- 시점 t 에서의 <strong>총 미래 보상</strong> 
    ![](0e894cb30186250a.webp)

- <code class="language-math">V(S&#95;{t&#43;1})</code>에서 <code class="language-math">S</code>도 Random variable이기 때문에 Expectaion을 취하여 계산한다&#46; 
    ![](f8b47e8ecc5b6315.webp)

- 평균은 발생 가능한 경우의 수에 대한 <code>가중 확률 &#42; (reword &#43; value)</code>로  구한다&#46; 
    ![](83ee9511076979f0.webp)

    - MRP 이기 때문에 Action을 고려하지 않는다&#46; 

<a id="34eeda9b0fe180d8860bdca3230da062"></a>

### <strong>유도 방법 2</strong>

![](bf357656b90276af.webp)

- <code class="language-math">S&#95;{t&#43;1}</code>에 대한 표현으로 변형
    ![](a4beb2464a26003b.webp)

    - 위 &#91;사전개념&#93; 활용 &#45; 식 유도 방법은 위 참조

- 나머지 내용은 유도 방식 1과 동일

<a id="345eda9b0fe18062b3fcfe9bade9485e"></a>

### 정리 &#45; Bellman equation for Value function (MRP)

![  • 백업 다이어그램: ⁍ → ⁍에서의 ⁍에 대한 관계식](b272eeeccc84389b.webp)

<a id="350eda9b0fe18045a63bff1082e3a18b"></a>

### Bellman equation for Value function (MRP)

![](dcb2bd2d3e9a5cab.webp)

<a id="350eda9b0fe1804a8ed2fe264fcf55d4"></a>

### 예제

![](61a5861169903eb5.webp)

1. <code class="language-math">s&#95;0</code> 에 대한 value functiond에 대한 bellman equation
    ![](154bca67970c15e3.webp)

1. <code class="language-math">s&#95;3</code> 에 대한 value functiond에 대한 bellman equation
    ![](88c3adda08d2d769.webp)

    - 가능한 next state가 아닌 경우,  transition probability(전이확률)이 0이기 때문에 생략한다&#46;
