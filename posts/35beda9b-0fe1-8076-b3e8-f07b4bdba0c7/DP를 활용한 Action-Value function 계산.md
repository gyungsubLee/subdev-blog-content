---
order: 2
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 35beda9b-0fe1-8076-b3e8-f07b4bdba0c7
title: DP를 활용한 Action-Value function 계산
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 31deda9b-0fe1-80d6-826b-c54fbb1123ff
    title: 강화학습
  - id: 320eda9b-0fe1-80d1-842c-e609cad65258
    title: 스크래치부터 시작하는 강화학습의 모든것
  - id: 35beda9b-0fe1-8076-b3e8-f07b4bdba0c7
    title: DP를 활용한 Action-Value function 계산
excerpt: DP를 활용한 Action-Value function 계산 --- 📖 DP를 활용한 Value function을 계산하는 방법과 거의 동일하다. 또한 DP를 이용해 Action-Value function을 계산하는 방법은 쓰이지 않는다. 🤔 왜 쓰이지 않는가? - 가능한 모든 state 와 모든 action을 다 고려
cover: null
icon: null
notionProperties:
  중요도: No
  상태: 완료
schema_version: 1
parent_id: 320eda9b-0fe1-80d1-842c-e609cad65258
created: 2026-05-09T04:41:09.531Z
updated: 2026-05-20T12:13:21.469Z
legacy_path: Main/강화학습-c54fbb1123ff/스크래치부터 시작하는 강화학습의 모든것-e609cad65258/DP를 활용한 Action-Value function 계산-f07b4bdba0c7/index.md
legacy_category: 강화학습
source_url: https://beautiful-college-c84.notion.site/35beda9b0fe18076b3e8f07b4bdba0c7
---
<a id="366eda9b0fe180699ab4fabf3a0ab4a2"></a>

## DP를 활용한 Action&#45;Value function 계산

---

> 📖 
> 
> <a id="366eda9b0fe1803cb719d302929e7f95"></a>
> 
> DP를 활용한 Value function을 계산하는 방법과 거의 동일하다&#46; 
> 
> <a id="366eda9b0fe18034917dccd2e41d0548"></a>
> 
> 또한 DP를 이용해 Action&#45;Value function을 계산하는 방법은<strong> 쓰이지 않</strong>는다&#46;

> 🤔 
> 
> <a id="366eda9b0fe1803781e9f9c4705d6cad"></a>
> 
> 왜 쓰이지 않는가?
> 
> - <strong>가능한 모든 state 와 모든 action을 다 고려</strong>해야 하기 때문에 value function에 비해서도  연산량이 훨씬 많다&#46; 
> 
> - 이러한 특성으로 인해 실제로는 사용하지 않는다&#46; 

<a id="366eda9b0fe180418050cf48c403207d"></a>

### DP를 활용한 Action&#45;Value function 계산

> 
> 
> <a id="366eda9b0fe1808cb880d5aa220ce91d"></a>
> 
> <strong>Bellman equation for Action&#45;Value function</strong>
> 
> ![](512a55e098f2abc7.webp)

> 💬 
> 
> <a id="366eda9b0fe180e9aabaf1cc44b82b28"></a>
> 
> <a href="#/post/340eda9b-0fe1-812c-a3f0-f7146c5e83ef">페이지</a>  방법과 거의 동일함
> 
> - 추가적으로 action을 더해서 계산하는 것 뿐임

1. 모든 state, action에 대해 정의된 임의의 action&#45;value function을 만든다&#46; 
    ![](949538282067853c.webp)

    -  모든 조합의 벡터를 생성 
        - <code class="language-math">&#124;S&#124;</code>x <code class="language-math">&#124;A&#124;</code>  
            - <code class="language-math">&#124; 요소&#124;</code>&#58; 카디널리티, 가능한 모든 요소의 경우의 수

1. Action&#45;Value function에 대한 Bellman equation을 이용해 아래와 같이 Action&#45;Value function을 업데이트 한다&#46;
    ![](664bf788460271fd.webp)

1. 계속해서 &#91;2&#93;를 반복하다가, 충분히 수렴했다고 판단되면 멈춘다&#46;
    ![](dc026ba5fa6129c6.webp)

<a id="366eda9b0fe1800bad7fd56c34909b71"></a>

### DP를 활용한 Action&#45;Value function 계산의 특징

![](872f10bd73acf68a.webp)

1. 환경의 MDP 모델을 알아야 함
    - value function 과 동일하게 transition probability 와 reward function을 알아야 한다&#46; 

    - 즉, MDP 모델이 필요한다&#46; 

1. State space와 action space를 모두 고려하므로, 연산량이 많아 안쓰임&#46;
    - 가능한 모든 state 와 모든 action을 다 고려해야 하기 때문에 value function에 비해서도  연산량이 훨씬 많다&#46; 

    - 이러한 특성으로 인해 실제로는 사용하지 않는다&#46;
