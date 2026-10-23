---
order: 27
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 340eda9b-0fe1-8063-8de2-cda6be3f0f6f
title: 마르코프 과정 (Markov Process)
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 31deda9b-0fe1-80d6-826b-c54fbb1123ff
    title: 강화학습
  - id: 320eda9b-0fe1-80d1-842c-e609cad65258
    title: 스크래치부터 시작하는 강화학습의 모든것
  - id: 340eda9b-0fe1-8063-8de2-cda6be3f0f6f
    title: 마르코프 과정 (Markov Process)
excerpt: 마르코프 과정 (Markov Process) --- 📖 마르코프 과정(Markov Process)은 마르코프 가정을 만족하는 연속적인 일련의 상태이다. 마르코프 과정은 일련의 상태 <S_1, S_2, \cdots , S_t>와 상태 전이 확률(state transition probability)로 구성된다. 마르코프 과
cover: null
icon: null
notionProperties:
  상태: 완료
schema_version: 1
parent_id: 320eda9b-0fe1-80d1-842c-e609cad65258
created: 2026-04-12T14:20:37.274Z
updated: 2026-04-12T14:20:54.951Z
legacy_path: Main/강화학습-c54fbb1123ff/스크래치부터 시작하는 강화학습의 모든것-e609cad65258/마르코프 과정 (Markov Process)-cda6be3f0f6f/index.md
legacy_category: 강화학습
source_url: https://beautiful-college-c84.notion.site/340eda9b0fe180638de2cda6be3f0f6f
---
<a id="340eda9b0fe1808a8da3f83bc9d426d6"></a>

## 마르코프 과정 (Markov Process)

---

> 📖 
> 
> <a id="340eda9b0fe180769591e789f4a2fd51"></a>
> 
> 마르코프 과정(Markov Process)은 <strong>마르코프 가정을 만족</strong>하는 <strong><u>연속적인 일련의 상태</u></strong>이다&#46; 마르코프 과정은 일련의 상태 <code class="language-math">&#60;S&#95;1, S&#95;2, &#92;cdots , S&#95;t&#62;</code>와 <code>상태 전이 확률(state transition probability)</code>로 구성된다&#46; 

<a id="340eda9b0fe1802b9d71d313eb5d2eda"></a>

### 마르코프 과정 (Markov Process)

![](07a9900481a27e26.webp)

![](4fb6e8090f441a40.webp)

- finite state space (유한한 state 집합)

- random variable S가 취할 수 있는 가능한 모든 값의 집합

![](c26dd698253a057b.webp)

- Transition probability model (metrix)

- <code class="language-math">P(S&#95;{t&#43;1} = s&#95;{t&#43;1} &#124; S&#95;{t} = s&#95;{t})</code>

![](95f66bbcb3f00c10.webp)

- P라는 함수가 S(state) 두개를 받아서 0 &#126; 1 사이의 확률값,  실수를 가진다는 의미인다&#46; 

<a id="340eda9b0fe180b992dfd60c98989e25"></a>

### <strong>상태 전이 확률(state transition probability)에 대한 매트릭스(P) 표현</strong>

![](f6885269719dc0cf.webp)

- state space가 <code class="language-math">s&#95;0</code>, <code class="language-math">s&#95;1</code>, <code class="language-math"> s&#95;2</code> 3개가 있다고 가정했을 때, <br>Transition이 일어날 수 있는 경우는 위 3 x 3 매트릭스로 표현할 수 있다&#46; 

- 현재 state에다 다음 state로 갈 모든 확률의 합은 1이다&#46; 
    - <code class="language-math">s&#95;0</code>→ <code class="language-math">s&#95;0</code> = 0&#46;2, 

    - <code class="language-math">s&#95;o</code> → <code class="language-math">s&#95;1</code> = 0&#46;1 

    - <code class="language-math">s&#95;o</code> → <code class="language-math"> s&#95;2</code> = 0&#46;7
        <a id="340eda9b0fe18038b131f04668f1bbe7"></a>

        ⇒ 0&#46;2 &#43; 0&#46;1 &#43; 0&#46;7 = 1

<a id="340eda9b0fe180388d72e7b6846589b5"></a>

### <strong>n&#45;th order Markov process</strong>

![](85a5f71a308b7d76.webp)

<a id="340eda9b0fe1808682bcd548141c4c64"></a>

<em>→ </em><strong><u>미래 정보를 예측</u></strong>하기 위해 <strong><u>모든 과거 상태</u></strong>가 <strong>다 필요하지 않</strong>고, <strong><u>가장 최근의 n개의 상태</u></strong>만 있어도 충분하다&#46;

- <code class="language-math">P(S&#95;{t&#43;1} = s&#95;{t&#43;1} &#92;mid S&#95;t=s&#95;t, &#92;dots , S0 = s0)</code>
    <a id="340eda9b0fe180669b06c9901668f97f"></a>

    <code class="language-math">= P(S&#95;{t&#43;1} = s&#95;{t&#43;1}&#124;S&#95;{t} = s&#95;t, &#92;dots ,</code>  <code class="language-math">S&#95;{t&#45;n&#43;1} = s&#95;{t&#45;n&#43;1}</code> <code class="language-math">)</code>

<a id="340eda9b0fe18019bb46fa1d7781bc2b"></a>

→ 앞서 살펴본 마르코프 프로세스는 <strong>first order Markov process</strong> 라고 할 수 있다&#46; 

<a id="340eda9b0fe1804c83a2c43685401b98"></a>

### 마르코프 프로세스 예시

- 그래프, 매트릭 예시
    ![](d04e51aab73bf22b.webp)

- 현실에서의 Markov process 예시
    <details>
    <summary><strong>예시 1) 로또 복권</strong></summary>

    ![](c1ab35ebadaf27d3.webp)

    - 어떻게 state를 설정하느냐에 따라 마르코프 프로세스가 될 수도 있고 안될 수 도 있다&#46; 
        ![](b128a6e20d76013b.webp)

        - <code class="language-math">t</code> 까지 뽑힌 공이기 때문에 <code class="language-math">S&#95;t</code>에 이전 state들이 포함되어 있다&#46; 

        ![](ace4d80b61d2f0bf.webp)

        - <code class="language-math">t</code> 에 뽑힌 공이기 때문에 <code class="language-math">S&#95;t</code>에 이전 state들을 모두 알아야 한다&#46;

    </details>

    <details>
    <summary><strong>예시 2) 지하철 도착시간</strong></summary>

    ![](28a2117c4596f547.webp)

    - 다음 정거장에서 도착 시간은 이전 정거장에서의 도착 시간만 알면 유추할 수 있다&#46; 

    </details>
