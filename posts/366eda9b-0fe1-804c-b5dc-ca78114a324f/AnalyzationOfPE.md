---
order: 1
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 366eda9b-0fe1-804c-b5dc-ca78114a324f
title: AnalyzationOfPE
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 31deda9b-0fe1-80d6-826b-c54fbb1123ff
    title: 강화학습
  - id: 320eda9b-0fe1-80d1-842c-e609cad65258
    title: 스크래치부터 시작하는 강화학습의 모든것
  - id: 366eda9b-0fe1-804c-b5dc-ca78114a324f
    title: AnalyzationOfPE
excerpt: AnalyzationOfPE --- Contraction mapping theorem을 활용한 policy evaluation의 수렴점 분석 - value-function에 대한 bellman equation 행렬화 - 이와 같이 policy evaluation 도 벡터화 해서 행렬화 가능 - (R^n, d_\infty)
cover: null
icon: null
notionProperties:
  Point: 유도식 상세 설명 정리 필요
  상태: 진행 중
schema_version: 1
parent_id: 320eda9b-0fe1-80d1-842c-e609cad65258
created: 2026-05-20T11:52:50.380Z
updated: 2026-06-17T12:20:01.965Z
legacy_path: Main/강화학습-c54fbb1123ff/스크래치부터 시작하는 강화학습의 모든것-e609cad65258/AnalyzationOfPE-ca78114a324f/index.md
legacy_category: 강화학습
source_url: https://beautiful-college-c84.notion.site/366eda9b0fe1804cb5dcca78114a324f
---
<a id="382eda9b0fe180b98404c205a3255e94"></a>

## AnalyzationOfPE

---

<a id="382eda9b0fe18067b004df6c9d3e6adb"></a>

### <strong>Contraction mapping theorem을 활용한 policy evaluation의 수렴점 분석</strong>

![](244323be860c557c.webp)

- value&#45;function에 대한 bellman equation 행렬화
    ![](47c7041f5ee52cd7.webp)

- 이와 같이 policy evaluation 도 벡터화 해서 행렬화 가능
    ![](ab49c4c97151f73b.webp)

- <code class="language-math">(R^n, d&#95;&#92;infty)</code>  라는 metric space에서 <code class="language-math">T^&#92;pi</code>는 contraction mapping 이다&#46;
    ![](39ca1668868e72e1.webp)

    - <code class="language-math">R^n</code>&#58; n 차원 실수 공간

    - <code class="language-math">d&#95;&#92;infty</code>&#58; 
        - p&#45;norm 에서 p 가 <code class="language-math">&#92;infty</code> 인 경우

        - 즉, distant metrix 로 사용

<a id="382eda9b0fe18051949bfdb124173d98"></a>

### 증명 &#45; <code class="language-math">T^{&#92;pi}(V&#95;k)</code> 가 contraction mapping 인가

![](62ee1985ec5b3491.webp)

- contraction mapping 이론
    ![](9d74574d5447d746.webp)

![](5ffeb3a0ba9f5c4b.webp)

![](992f02700e4d2e69.webp)

![](e25fe58aa1af8460.webp)

![](714fcc2807797060.webp)

![](d40da0a7cb94ef48.webp)

![](b7bd1533ba8c1783.webp)

![](05bf6a84951368f6.webp)

<a id="382eda9b0fe180d6aa2cf65c34807521"></a>

#### 정리 

![](e8d4d37188735524.webp)
