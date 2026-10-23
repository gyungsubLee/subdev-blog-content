---
order: 0
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1ceeda9b-0fe1-80dc-a88d-e278787f6f8a
title: "모던 자바: Java 8 변경점"
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-81ae-909e-cd1f71740107
    title: Spring ( Java )
  - id: 1c3eda9b-0fe1-818f-97a3-c9faaae63332
    title: "[sparta] Java 문법 종합반 (중단)"
  - id: 1ceeda9b-0fe1-80dc-a88d-e278787f6f8a
    title: "모던 자바: Java 8 변경점"
excerpt: "모던 자바: Java 8 변경점 --- 📖 자바 8 이후, 함수형 프로그래밍에 대한 기술이 도입되었다. - 람다 - 스트림 프로그래밍 언어의 진화 시장에서 프로그래머가 해결해야 하는 문제는 계속 변화한다. 문제가 변화되기 때문에 프로그래밍 언어에 요구되는 기능들도 변화하다. 따라서 시대에 맞는 기능들을 제공하지 않는 언"
cover: null
icon: null
notionProperties:
  상태: 진행 중
schema_version: 1
parent_id: 1c3eda9b-0fe1-818f-97a3-c9faaae63332
created: 2025-04-07T15:17:37.519Z
updated: 2025-05-26T01:43:04.571Z
legacy_path: Main/Spring ( Java )-cd1f71740107/[sparta] Java 문법 종합반 (중단)-c9faaae63332/모던 자바- Java 8 변경점-e278787f6f8a/index.md
legacy_category: Spring ( Java )
source_url: https://beautiful-college-c84.notion.site/1ceeda9b0fe180dca88de278787f6f8a
---
<a id="1dceda9b0fe180d6a0a3f2bb64c5c8ad"></a>

## 모던 자바&#58; Java 8 변경점

---

> 📖 
> 
> <a id="1dceda9b0fe1804b9aa5e2f7a6e814fb"></a>
> 
> 자바 8 이후, 함수형 프로그래밍에 대한 기술이 도입되었다&#46; 
> 
> - 람다
> 
> - 스트림

<details>
<summary>프로그래밍 언어의 진화</summary>

<a id="1dceda9b0fe180d68befcc949e24da25"></a>

시장에서 프로그래머가 해결해야 하는 문제는 계속 변화한다&#46;

<a id="1dceda9b0fe18074afa2c645e64e5b1a"></a>

문제가 변화되기 때문에 프로그래밍 언어에 요구되는 기능들도 변화하다&#46;

<a id="1dceda9b0fe180cea661dcbcd9d93552"></a>

따라서 시대에 맞는 기능들을 제공하지 않는 언어들은 새로운 언어의 탄생을 야기한다&#46; 

<a id="1dceda9b0fe1804d90cad3b0eb6c8b22"></a>

그리고 해당 언어들이 프로덕션 레벨에 도달하는 동안 적용하지 못하면 해당 언어는 도태되기 시작한다 &#46;

<a id="1dceda9b0fe180688515e2266578be53"></a>

예를 들어 C/C&#43;&#43; 같은 언어들은 프로그램 실행에 대한 비용이 크지 않고, 하드웨어적인 보편성, 호환성에 큰 장점을 가지고 있었기 때문에 시장에서 가장 지배적인 입지를 차지 했었다&#46; 

<a id="1dceda9b0fe180df80f5e82845828f14"></a>

하지만 언어의 난이도와 다른 요인들의 영향으로 예기치 않은 종료 및 보안 이슈 증가 등 안정성이 떨어졌다&#46;

<a id="1dceda9b0fe1803aabbff544514217d7"></a>

그러던 와중 하드웨어는 꾸준히 진화를 거듭했고,  그 진화 결과  프로그램을 실행시키는 자원을 더 많이 사용할 수 있게되면서 더 안정성이 높은 c&#35;, java 와 같은 언어들이 각광받게 된다&#46; 

- 물론 안정성이 높아진 만큼 성능이 상대적으로 떨어졌다&#46;

> ✏️ 
> 
> <a id="1dceda9b0fe1806c9ca4e2309a57278c"></a>
> 
> c/c&#43;&#43; 은 여전히 성능이 매우 중요한 분야나, 아주 작은 컴퓨팅 자원만을 필요로 하는 소형 하드웨어 쪽에서는 아직도 메이저 한 언어이다&#46;  
> 
> - 물론 러스트가 위협하고 있다&#46;  ( 이미 따라잡지 않았나? )
> 
> <a id="1dceda9b0fe180a9b5eacbd7bc7ecaa5"></a>
> 
> 다만 상향 평준화된 컴퓨터나 서버 장비 처럼 더 높은 자원을 활용하는 환경에서는 더 높은 안정성을 가지는 언어가 니즈에 부합했을 뿐이다 &#46;

</details>

<details>
<summary><strong>Java 8</strong></summary>

> ✏️ 
> 
> <a id="1dceda9b0fe180fca388d1b65a9604eb"></a>
> 
> 자바는 객체 지향 패러다임과, jvm만 설치되어 있다면, 어디서나 실행시킬 수 있다는 장점이 있다&#46; 

- 자바는 캡슐화, 상속, 다형성 등 객체지향 프로그램의 많은 장점을 가지고 생산성과 안정성을 확보한다&#46; 

- JVM만 설치되어 있다면, 어떤 환경이라도 프로그램을 실행시킬 수 있다&#46; 

- 이와 같은 이유로 웹 어플리케이션 시장에서 가장 사람받는 언어 중 하나로 거듭나게 되었다&#46;

> ❗ 
> 
> <a id="1ffeda9b0fe180c99b93e70dd3df18d4"></a>
> 
> 그러나 하드웨어의 진화와 새로운 요구사항의 탄생으로 자바 역시 새로운 생태계의 변화에 직면하게 되었다&#46;

<details>
<summary>1&#46; 병렬 처리</summary>

<a id="1ffeda9b0fe1803ab8e3cca06b91b26e"></a>

앱의 발전함에 따라 유저들이 기하급수적으로 늘어났다&#46; 또한 하드웨어의 발전으로 멀티 코어 컴퓨터와 같은 병렬 프로세싱이 가능한 장비들이 보급되면서 새로운 요구사항에 직면하게 되었다&#46; 

<a id="1ffeda9b0fe180ecb56dc8a4ade351f3"></a>

이에 따라 자바 언어도 병렬처리를 위해,  <code>Multi&#45;Thread</code>에 대한 지원을 하게된다&#46;

- ‣

</details>

<details>
<summary>2&#46; 함수형 프로그래밍</summary>

> ✏️ 
> 
> <a id="1ffeda9b0fe18051add3f09b89ba3bc3"></a>
> 
> 함수형 프로그래밍은, 객체 지향 프로그래밍처럼 프로그래밍 패러다임의 한 종류이다&#46;

<details>
<summary>객체 지향 프로그래밍</summary>

- 프로그램을 객체들의 협력과 상호작용으로 바라보고 구현한다&#46; 

- 이러한 객체들을 정의하기 위해, 추상화 등과 같은 개념들을 사용한다&#46;
    - 코드 재사용성 ↑

    - 코드 유지보수, 확장 용이

    - 코드를 신뢰성 있게 사용하기 쉬워진다&#46;

</details>

<details>
<summary>함수형 프로그래밍</summary>

> ✏️ 
> 
> <a id="1ffeda9b0fe1806e948ff0071978519f"></a>
> 
> 수학의 함수처럼, 특정한 데이터에 의존하지 않고 관련없는 데이터를 변경하지도 않으며, 결과값이 오직 입력값에만 영향을 받는 함수를 순수함수라 한다&#46;

- 검증이 쉽다&#46; ( 필요한 부분만 검증 가능 )

- 성능 최적화가 쉽다 <br>( 특정 input에 대한 output 재사용 할 수 있음 &#45; 캐싱 )

- 동시성 문제를 해결하기 쉽다&#46; <br>( 함수는 다른 값의 변경을 야기하지 않음 )

</details>

</details>

</details>

<details>
<summary>&#91; 코드 &#93;</summary>

<a id="1dceda9b0fe1807ea8a6df3c3cc14729"></a>

```java

```

</details>
