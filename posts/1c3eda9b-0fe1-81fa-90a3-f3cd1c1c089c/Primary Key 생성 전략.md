---
order: 4
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1c3eda9b-0fe1-81fa-90a3-f3cd1c1c089c
title: Primary Key 생성 전략
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-817c-b119-d6a1706fbaf8
    title: 대규모 시스템 설계
  - id: 1c3eda9b-0fe1-8151-a9bf-f4bde443f283
    title: 대규모 시스템 설계 - 게시판
  - id: 1c3eda9b-0fe1-81fa-90a3-f3cd1c1c089c
    title: Primary Key 생성 전략
excerpt: 1. DB - Auto Increment - 분산 DB 환경에서 PK가 중복될 수 있기 때문에, 식별자의 유일성이 보장되지 않는다. 여러 샤드에서 동일한 PK를 가지는 상황 - 클라이언트에 노출 시, 보안 문제 발생 데이터 개수 or 특정 시점의 식별자 예층 가능 - 방금 가입 시 user_id가 1000이라면 1000명
cover: null
icon: null
notionProperties:
  Tags: 개념
  상태: 완료
schema_version: 1
parent_id: 1c3eda9b-0fe1-8151-a9bf-f4bde443f283
created: 2025-03-27T07:52:18.663Z
updated: 2025-03-27T07:52:18.663Z
legacy_path: Main/대규모 시스템 설계-d6a1706fbaf8/대규모 시스템 설계 - 게시판-f4bde443f283/Primary Key 생성 전략-f3cd1c1c089c/index.md
legacy_category: 대규모 시스템 설계
source_url: https://beautiful-college-c84.notion.site/1c3eda9b0fe181fa90a3f3cd1c1c089c
---
<a id="1c3eda9b0fe181d2acbff50d1abcc638"></a>

### 1&#46; DB &#45; Auto Increment

- 분산 DB 환경에서 PK가 중복될 수 있기 때문에, 식별자의 유일성이 보장되지 않는다&#46; 
    <details>
    <summary>여러 샤드에서 동일한 PK를 가지는 상황</summary>

    ![](054eb0fd775f0bf5.webp)

    </details>

- 클라이언트에 노출 시, 보안 문제 발생
    <details>
    <summary>데이터 개수 or 특정 시점의 식별자 예층 가능</summary>

    - 방금 가입 시 user&#95;id가 1000이라면 1000명의 사용자가 있다는 것을 예측 가능

    </details>

---

- 간단하기 때문에 아래의 상황에서는 유리할 수 있다&#46; 
    - 보안적인 문제를 크게 고려하지 않는 상황

    - 단일 DB를 사용하거나 애플리이션에서 PK 중복을 직접 구분하는 상황

<a id="1c3eda9b0fe181cb8e2ef5c053bdfd59"></a>

### 2&#46; 유니크 문자열 or 숫자

- UUID or 난수를 생성하여 PK를 지정 가능
    - 정렬 데이터가 아닌 랜덤 데이터 삽입

    - 키 생성 방식 간단

- 그러나, 랜덤 데이터로 인해 성능 저하가 발생될 수 있다&#46; 
    - Clustered Index는 정렬된 상태를 유지한다&#46; 

    - 데이터 삽입 필요한 인덱스 페이지가 가득 찼다면, <br>B&#43; tree 재구성 및 페이지 분할로 디스크 I/O 비용이 추가로 발생된다&#46; 

    - PK를 이용한 범위 조회가 필요하다면, 디스크에서 랜덤 I/O가 발생하기 때문에, 순차 I/O보다 성능이 저하된다&#46; 

<a id="1c3eda9b0fe181b69453f9d4210d8a8f"></a>

### 3&#46; 유니크 정렬 문자열

- 분산 환경에 대한 PK 중복 문제 해결

- 보안 문제 해결

- 랜덤 데이터에 의한 성능 문제 해결

- UUID v7, ULD 등의 알고리즘 사용
    - 일반적으로 알려진 알고리즘은 128비트를 사용한다&#46; 

- 데이터 크기에 따라, 공간 및 성능 효율이 달라진다&#46; 
    - Clustered Index는 PK를 기준으로 만들어진다&#46; 

    - Secondary Index는 데이터에 접근할 수 있는 포인터를 가진다&#46; 
        - 즉, PK를 가지고 있다&#46; 

    - PK가 크면 클수록, 데이터는 더 많은 공간을 차지하며

    - 비교 연산에 의한 정렬/조회에 더 많은 비용을 소모한다&#46; 

<a id="1c3eda9b0fe1814394cff15722e0f260"></a>

### 4&#46; 유니크 정렬 숫자

- 분산 환경에 대한 PK 중복 문제 해결

- 보안 문제 해결

- 랜덤 데이터에 의한 성능 문제 해결

- Snowflake, TSID 등의 알고리즘
    - 64비트 사용 &#91; BIGINT &#93;

    - 정렬을 위해 타임스탬프를 나타내는 비트 수의 제한으로  키 생성을 위한 시간적인 한계가 있을 수 있다&#46; 

    - 문자열 알고리즘에서도 동일한 문제가 있으나 비트 수가 많을수록 제한이 덜할 수 있다&#46;

- 앞선 문자열 방식보다 적은 공간을 사용한다&#46; 

<a id="1c3eda9b0fe1811282f5fae41cbb426b"></a>

해당  프로젝트에서는 유니크 정렬 숫자 방식인 Snowflake 알고리즘을 사용하여 PK를 생성하였다&#46; 

<a id="1c3eda9b0fe1818687c4e871c2e14bb7"></a>

각 프로젝트의 특색에 맞는 적절한 전략을 사용하는 것이 중요하다&#46;
