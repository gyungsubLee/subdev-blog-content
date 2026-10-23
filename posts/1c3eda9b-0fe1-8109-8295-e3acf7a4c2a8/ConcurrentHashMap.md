---
order: 2
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1c3eda9b-0fe1-8109-8295-e3acf7a4c2a8
title: ConcurrentHashMap
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-81e9-9396-e5365dccd8d6
    title: 자료구조
  - id: 1c3eda9b-0fe1-8109-8295-e3acf7a4c2a8
    title: ConcurrentHashMap
excerpt: Reference ‣ ‣ ‣ HashMap의 단점 및 이를 보안하는 ConcurrentHashmap --- 일반적으로 HashMap은 멀티스레드 환경에서 스레드 안전을 보장 하지 않는다. 따라서 race condition(경쟁 조건), invalid state(잘못된 상태)가 발생될 수있다. - 쓰기에서 원자적인 연산 처
cover: null
icon: null
notionProperties:
  상태: 진행 중
  날짜: 2025-01-05
  다중 선택: ⭐️⭐️⭐️
schema_version: 1
parent_id: 1c3eda9b-0fe1-81e9-9396-e5365dccd8d6
created: 2025-03-27T07:47:12.310Z
updated: 2025-04-09T06:32:51.877Z
legacy_path: Main/자료구조-e5365dccd8d6/ConcurrentHashMap-e3acf7a4c2a8/index.md
legacy_category: 자료구조
source_url: https://beautiful-college-c84.notion.site/1c3eda9b0fe181098295e3acf7a4c2a8
---
<details>
<summary>Reference</summary>

<a id="1c3eda9b0fe1813189b1d741e2b4ca9c"></a>

‣

<a id="1c3eda9b0fe181bf9376eeab835c620f"></a>

‣

<a id="1c3eda9b0fe181fe818dceca166a1c27"></a>

‣

</details>

<a id="1c3eda9b0fe181f88b60ee35c7d894c9"></a>

## HashMap의 단점 및 이를 보안하는 ConcurrentHashmap

---

<a id="1c3eda9b0fe1817d8a75f6c87087e618"></a>

일반적으로 HashMap은 멀티스레드 환경에서 <strong><u>스레드 안전을 보장 하지 않</u></strong>는다&#46;

<a id="1c3eda9b0fe181cdb37ed98254774607"></a>

따라서<strong> race condition(경쟁 조건)</strong><strong>,</strong><strong> invalid state(잘못된 상태)</strong>가 발생될 수있다&#46; 

- 쓰기에서 원자적인 연산 처리가 되지 않아, 한 값이 다른 값을 덮어쓸 수 있고, <br>이는 Map이 일관되지 않는 상태가 될 수 있다&#46; 

- 데이터의 <strong><u>일관성, 정합성</u></strong>을 보장하지 않음

<a id="1c3eda9b0fe18156bfe5da0b7d245263"></a>

이를 해결하기 위해 Java에서는 <strong><u>스레드 안정선이 내장된 ConcurrentHashMap을 제공</u></strong>한다&#46; 

> 탄생 배경

- <strong>ConcurrentHashMap</strong>은 자바 1&#46;5에서 도입되었으며, 주로 멀티스레드 환경에서의 성능 문제를 해결하기 위해 설계되었다&#46; 

- 기존의 HashMap이나 Hashtable은 멀티스레드 환경에서 <strong><u>데이터 정합성을 보장하지 못</u></strong>하거나<strong><u> 성능이 크게 저하</u></strong>되는 문제가 있었다&#46; <code>Hashtable</code>은 <strong><u>모든 메서드에 대해 동기화를 사용</u></strong>하여 <u>안전성을 확보</u>했지만, 그로 인해 <strong><u>성능이 크게 떨</u></strong>어졌다&#46;

- 이를 해결하기 위해 <strong>ConcurrentHashMap</strong>이 도입되었으며, <strong><u>부분적인 락(lock)</u></strong>을 사용하여 <strong><u>성능을 향상</u></strong>시키면서도 <strong><u>Thread Safety를 보장</u></strong>할 수 있었다&#46;

![](98d469489a96720f.webp)

![](78ae45f362a0c15d.webp)

![](306704c616ce424e.webp)
