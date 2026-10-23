---
order: 0
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 3c2eda9b-0fe1-8077-9baa-cfb834f0938b
title: CPU
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 3c0eda9b-0fe1-8001-9c81-efd292f28e5f
    title: 구조적인 문제 해결을 위한 컴퓨터공학
  - id: 3c2eda9b-0fe1-8077-9baa-cfb834f0938b
    title: CPU
excerpt: CPU 구성요소 --- ☝🏻 CPU는 대단히 정교하게 설계되어 있는 부품인 만큼 모든 구성요소를 확인할 수 없다. 그 중 가장 중요한 3가지만 확인 해본다. CPU 핵심 구성 요소 세가지 - ALU (산술논리연산장치) - 연산을 수행하는 장치 ( 계산(+, *)을 담당하는 회로 ) - 더하기, 곱셉, 오버플로우 검출 등
cover: null
icon: null
notionProperties:
  sub chapter: CPU 구성요소, 레지스터, 명령어 사이클/ 인터럽트, 멀티코어/멀티프로세스, 명령어 병렬 처리-파이프라이닝, 비순차적 명령어 처리
  상태: 완료
schema_version: 1
parent_id: 3c0eda9b-0fe1-8001-9c81-efd292f28e5f
created: 2026-08-20T11:37:21.142Z
updated: 2026-10-04T14:55:08.384Z
legacy_path: Main/구조적인 문제 해결을 위한 컴퓨터공학-efd292f28e5f/CPU-cfb834f0938b/index.md
legacy_category: 구조적인 문제 해결을 위한 컴퓨터공학
source_url: https://beautiful-college-c84.notion.site/3c2eda9b0fe180779baacfb834f0938b
---
<a id="3d3eda9b0fe180839839d1232ab84542"></a>

## CPU 구성요소

---

> ☝🏻 
> 
> <a id="3eaeda9b0fe180cf9778f95d233a09d0"></a>
> 
> CPU는 대단히 정교하게 설계되어 있는 부품인 만큼 모든 구성요소를 확인할 수 없다&#46; 그 중 가장 중요한 3가지만 확인 해본다&#46; 

> 
> 
> <a id="3d3eda9b0fe1801e9731c38ef856cb35"></a>
> 
> <strong>CPU 핵심 구성 요소 세가지</strong>
> 
> ![](668ee5e9da4e2987.webp)
> 
> - <code>ALU (산술논리연산장치)</code>
>     - 연산을 수행하는 장치 ( 계산(<code>&#43;</code>, <code>&#42;</code>)을 담당하는 회로 )
>         - 더하기, 곱셉, 오버플로우 검출 등 다양한 회로들이 포함되어 있음
>             - <code>빼기</code>&#58; 2의 보수를 처리한 뒤 <strong><u>더하기 연산</u></strong>으로 처리됨
> 
> - <code>제어 장치</code>
>     - <strong><u>명령어를 해석</u></strong>하고 <strong><u>제어 신호를 보</u></strong>내는 장치
>         - <code>제어 신호</code>&#58; 컴퓨터 부품들한테 어떤 동작을 할지 알려주는 일종의 전기신호다
> 
>         - 다른 입출력 장치들도 제어신호를 내보냄
> 
> - <code>레지스터(들)</code>
>     - 명령어 처리 전후로 값을 임시 저장하는 장치
> 
>     - 여러 종류가 있으며, 특수한 목적을 가지는 레지스터들도 있다&#46; 

> ☝🏻 
> 
> <a id="3d4eda9b0fe1805f91ace909c6287577"></a>
> 
> 개발자에게는 <strong><u>레지스터</u></strong>가 가장 중요하다&#46; 
> 
> <a id="3d4eda9b0fe180fba23dc81e05b8ef81"></a>
> 
> 특별한 직군을 제외하고 ALU, 제어장치를  코드나 명령어로 다룰 일은 거의 없다&#46; 
> 
> <a id="3d4eda9b0fe180109ee0c3bea2ce751c"></a>
> 
> 그러나 레지스터는 <strong><u>일부 로우 레벨을 개발</u></strong>하거나, <strong><u>보안 관련된 직업</u></strong>의 경우, 레지스터를 알아야 한다&#46; 
> 
> <a id="3d7eda9b0fe1803f8c0cc273dac43b07"></a>
> 
> <code>레지스터</code>는 <strong><u>명령어 처리 전후로 처리되는 값들을 저장</u></strong>하고 있는<strong><u> 저장장치</u></strong>다 따라서 <strong><u>레지스터에 어떤 값이 담기는 지 관찰</u></strong>하면 <strong>명령어 처리 과정을 엿볼 수 있</strong>다&#46; 
> 
> - 레지스터는 다양한 종류가 있고, 특별한 목적을 갖고 있는 레지스터도 있다&#46; 
> 
> - CPU 종류마다 레지스터 이름, 개수, 동작방식(주소 지정의 방식), 용량 등이 달라질 수 있다&#46; 그 중 공통적으로 다루는 것들만을 학습한다&#46; 

<a id="3d4eda9b0fe180198a4ad9f684b8fc9f"></a>

### ALU 

> ✏️ 
> 
> <a id="3d7eda9b0fe1809dbda2fda502378145"></a>
> 
> ALU ( 계산기 회로, 계산을 담당하는 회로의 묶음)
> 
> ![](f5813ce7c5144620.webp)
> 
> - 레지스터로부터 피연산자(연산의 대상)을 받아들인다&#46;
> 
> - 제어 장치로부터 제어 신호(연산할 작업)을 받아들인다&#46; 
> 
> - 연산의 결과를 레지스터, 플래그 레지스터에 저장한다&#46; 

- ex) <code>1 &#43; 2 = 3</code>
    > 레지스터에 프로그램 연산(제어신호) 전후로 담기는 값들이 있기 때문에 레지스터를 관찰하면 로우 레벨을 잘 관찰할 수 있다&#46; 

    - 피연산자&#58; <code>1</code>, <code>2</code>
        - AU

    - 제어신호&#58; <code>&#43;</code>
        - ALU가 해야되는 연산

    - 결과값&#58; <code>3</code>
        - ALU가 내보는 return 값

- 플래그 레지스터&#58; <code>연산 결과에 대한 부가 정보 저장</code>
    > 자세한 설명 아래 참조 

    <a id="3d7eda9b0fe1801aad9ce555dc550e92"></a>

    연산을 하는 과정에서 <strong><u>부가적인 정보</u></strong>를 참조해야 될 때가 있다&#46; 

    1. <code>오버플로우</code>
        - 레지스터에 담는 결과값이 레지스터의 크가보다 커질 수 있다&#46;  

    1. <code>값 부호</code> 
        - 연산 결과가 음수, 양수 인지 

<a id="3d7eda9b0fe18058bb37da3b99667f24"></a>

### 플래그 레지스터

<a id="3d3eda9b0fe1803d8cc6eaae8a1e4ae7"></a>

## 레지스터

---

> 

<a id="3d3eda9b0fe180dca076cefe1158b926"></a>

## 명령어 사이클, 인터럽트

---

> 

<a id="3d3eda9b0fe180a188efc5434378bb1b"></a>

## 멀티코어, 멀티프로세스

---

> 

<a id="3d3eda9b0fe1801b9451d43b2aa7dba3"></a>

## 명령어 병렬 처리 &#45; 파이프라이닝

---

> 

<a id="3d3eda9b0fe180739dcbc5d6da787a0f"></a>

## 비순차적 명령어 처리

---

>
