---
order: 0
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 366eda9b-0fe1-80b3-b891-d1ca2af6b55e
title: Contraction mapping theorem
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 31deda9b-0fe1-80d6-826b-c54fbb1123ff
    title: 강화학습
  - id: 320eda9b-0fe1-80d1-842c-e609cad65258
    title: 스크래치부터 시작하는 강화학습의 모든것
  - id: 366eda9b-0fe1-80b3-b891-d1ca2af6b55e
    title: Contraction mapping theorem
excerpt: "Contraction mapping theorem --- Metric space - 순서가 정해진 쌍 (M, d)가 아래의 조건을 만족할 때 이를, Metric space 라고 한다. - M: 집합 - d(distance): M에 대한 metric - x, y, z \\in M 에 대해서 아래의 조건을 만족해야 한다. 1."
cover: null
icon: null
notionProperties:
  상태: 완료
schema_version: 1
parent_id: 320eda9b-0fe1-80d1-842c-e609cad65258
created: 2026-05-20T12:13:56.230Z
updated: 2026-06-19T11:44:37.200Z
legacy_path: Main/강화학습-c54fbb1123ff/스크래치부터 시작하는 강화학습의 모든것-e609cad65258/Contraction mapping theorem-d1ca2af6b55e/index.md
legacy_category: 강화학습
source_url: https://beautiful-college-c84.notion.site/366eda9b0fe180b3b891d1ca2af6b55e
---
<a id="382eda9b0fe1800db9e4cb807d1a9051"></a>

## Contraction mapping theorem

---

<a id="382eda9b0fe18027a663d9690d5fc115"></a>

### <strong>Metric space</strong>

![](78ffbded513c7b9d.webp)

- 순서가 정해진 쌍 (M, d)가 아래의 조건을 만족할 때 이를, <code>Metric space</code> 라고 한다&#46;
    ![](d5a792de9bb5c3e6.webp)

    - <code>M</code>&#58; 집합

    - <code>d(distance)</code>&#58; M에 대한 metric

- <code class="language-math">x, y, z &#92;in M</code> 에 대해서 아래의 조건을 만족해야 한다&#46; 
    1. <code class="language-math">x</code> 에서 시작해서 <code class="language-math">x</code> 까지의 거리는 <code class="language-math">0</code> 이어야 한다&#46; 
        ![](a184f761fb3aed58.webp)

    1. 다른 두 점 사이의 거리는 항상 양수여야 한다&#46; 
        ![](088cc153a9d04f66.webp)

    1. x 에서 y까지의 거리와 y에서 x까지의 거리가 동일해야 한다&#46;
        ![](c669c13b2264d699.webp)

    1. x 에서 z 까지의 거리가 중간 y 점을 거친 것 보다 작거나 같아야 한다&#46; (<code>triangular inequality</code>)<br>
        ![](d2654ea9caa1824c.webp)

        ![  • triangular inequality](76c108a60a2dd009.webp)

<a id="382eda9b0fe180a29b7dde55d330be08"></a>

### <strong>p&#45;norm</strong>

> ✏️ 
> 
> <a id="384eda9b0fe1801d8f9bf28163993773"></a>
> 
> <code>p&#45;norm</code>은 벡터의 <strong>크기(magnitude)</strong> 또는 <strong>거리(distance)</strong> 를 측정하는 일반화된 방법을 말한다&#46; 
> 
> <a id="384eda9b0fe180a98295cb67ee47fcd9"></a>
> 
> 수학적으로는 아래와 같이 정의된다&#46; 
> 
> ![](ac9f25b870022254.webp)

![](218f68c068e204f1.webp)

- <code class="language-math">&#124;&#124;x&#124;&#124;&#95;p</code>
    ![](edd75a56ca11d24b.webp)

    - 유클리디안 거리 식과 동일

- 앞 선 Metric space 의 조건을 아래 식들이 만족한다&#46;
    ![](ae4e5ec042bd5fb0.webp)

<a id="382eda9b0fe18097a64dcd1430030892"></a>

### <strong>Contraction mapping</strong>

![](2c04344ef58b2014.webp)

<a id="382eda9b0fe18052933ac70e4092e580"></a>

(X, d) 가 metric space 이고,  X → X 로 가는 매핑 함수를 지날 때

- X&#58; 매트릭 스페이스에서 거리의 점이 되는 원소들의 집합

- d&#58; 거리를 재는 척도

- 매핑 함수(X → X)
    ![](579c96f945988e97.webp)

<a id="382eda9b0fe18058a9a7d0f3a25a58fc"></a>

만약 constant <code>c</code>가 <code>0 ≤ c ≤ 1</code> 일 때, 이 함수를 contraction mapping 또는 contraction 이라 부른다&#46; 

![](b1cd400c893ffb32.webp)

- X 에 존재하는 x, y 의 모든 원소를 만족할 때 성립한다&#46;
    ![](713d74f54953556e.webp)

    - 이때 매핑함수의 c가 <code>0 ≤ c ≤ 1</code> 이기 때문에 위 그림과 같이 원본 함수보다 작은 분포를 가지게 된다&#46;

    - T(x), T(y) 두 점 사이의 거리가 까워진다&#46; 

<a id="382eda9b0fe1801db4b2ede757145b3b"></a>

### <strong>Contraction mapping theorem</strong>

![](4f1ff8b68f599345.webp)

- 설명 1
    ![](58746a6f48731203.webp)

    - 점 <code class="language-math">x^&#42;</code>에 transfoemation <code class="language-math">T(x)</code>를 씌울 때 다시 자기 자신을 만족하는  점 <code class="language-math">x^&#42;</code> 는 고유하다&#46;  이러한 점을 fixed point(고정 점)이라고 한다&#46;

- 설명 2
    ![](bb5d7107a70bd5b1.webp)

    - <code class="language-math">x&#95;0 &#92;in X</code> 일 때 <code class="language-math">x&#95;n = T^n(x&#95;0)</code>  즉,  <code class="language-math">x&#95;0</code> 에 transformation 함수를 n 번 씌운 것이 된다&#46;

    - 따라서 <code class="language-math">n → &#92;infty</code> 갈 때 <code class="language-math">x^&#42;</code> 는 fixed point가 된다&#46;
