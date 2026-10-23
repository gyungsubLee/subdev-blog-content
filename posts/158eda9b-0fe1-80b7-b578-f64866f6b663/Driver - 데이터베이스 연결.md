---
order: 3
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 158eda9b-0fe1-80b7-b578-f64866f6b663
title: Driver - 데이터베이스 연결
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 108eda9b-0fe1-80a6-8a2b-c21df3ab9492
    title: 내일 배움 캠프 ( 백엔드 코스 7기)
  - id: 158eda9b-0fe1-8083-a08b-e1249279d10f
    title: "[ sparta ] JPA 실무 스프링 백엔드 - 심화형"
  - id: 158eda9b-0fe1-80b7-b578-f64866f6b663
    title: Driver - 데이터베이스 연결
excerpt: 데이터베이스 Driver 역할 및 종류 --- 📖 데이터베이스 드라이버 DB Driver)는 애플리케이션과 데이터베이스 간의 통신을 중개하는 역할한다. - 애플리케이션 요청을 DB가 이해할 수 있는 언어로 변환하여 처리 드라이버의 종류 - 다양한 DB 시스템 마다 호환되는 드라이버가 있다. - Oracle, MySQL,
cover: null
icon: null
notionProperties:
  상태: 완료
  VpFa: ⭐️⭐️
  Tags: Driver
  Sub Chapter: |-
    • DB Driver 역할 및 종륲
    • DB Driver 동작
schema_version: 1
parent_id: 158eda9b-0fe1-8083-a08b-e1249279d10f
created: 2024-12-10T04:50:25.396Z
updated: 2026-04-04T13:50:26.242Z
legacy_path: Main/내일 배움 캠프 ( 백엔드 코스 7기)-c21df3ab9492/[ sparta ] JPA 실무 스프링 백엔드 - 심화형-e1249279d10f/Driver - 데이터베이스 연결-f64866f6b663/index.md
legacy_category: 내일 배움 캠프 ( 백엔드 코스 7기)
source_url: https://beautiful-college-c84.notion.site/158eda9b0fe180b7b578f64866f6b663
---
<a id="158eda9b0fe18186a02ec71efa7b2258"></a>

## <strong> 데이터베이스 Driver 역할 및 종류</strong>

---

> 📖 
> 
> <a id="158eda9b0fe18118804fef441eb6327d"></a>
> 
> <code>데이터베이스 드라이버 DB Driver)</code>는 <strong><u>애플리케이션과 데이터베이스 간의 통신을 중개</u></strong>하는 역할한다&#46;
> 
> - <strong><u>애플리케이션 요청</u></strong>을 <strong>DB가 이해할 수 있는 언어로 변환</strong>하여 처리

<details>
<summary>드라이버의 종류</summary>

![](918b02216d0513f6.webp)

- 다양한 DB 시스템 마다 호환되는 드라이버가 있다&#46; 
    - <code>Oracle</code>, <code>MySQL</code>, <code>PostgreSQL</code> 등 각 <strong><u>DB 제품에 맞는 특정 드라이버가 필요</u></strong>함

</details>

<a id="158eda9b0fe180b18db4d5b0c45a8a3d"></a>

## 데이터베이스 Driver 동작

---

> 📖 
> 
> <a id="69987cc860734d67ad28e652684e85e6"></a>
> 
> <code>DB Driver</code>는 <strong><u>애플리케이션과  데이터베이스 간의 데이터 교환을 조절하고 관리</u></strong>하는 역할을 한다&#46; 

> ✏️ <strong><u>JDBC Driver Manager</u></strong>는 애플리케이션이 실행되고 있는 <strong><u>런타임 시점</u></strong> 아래와 같은 동작을 한다&#46; 
> 
> ![](e9c0c4b13b825a45.webp)
> 
> 1. <code>Connection(연결)</code>을 생성하여 <strong><u>쿼리를 요청할 수 있는 상태</u></strong>로 만듬
> 
> 1. <code>Statement(상태)</code>를 생성하여 <strong><u>쿼리를 요청</u></strong>함
> 
> 1. <code>ResultSet(결과셋)</code>을 생성해 <strong><u>쿼리 결과를 받</u></strong>아올 수 있도록함

<details>
<summary>Driver 동작 방식</summary>

<a id="158eda9b0fe180029156e5c6a53daad6"></a>

1&#46; 연결 초기화

- 요청 수신
    - 애플리케이션은 데이터베이스 작업을 시작하기 위해 드라이버에 연결을 요청한다&#46; 

    - 이는 마치 항공편이 이륙 허가를 받기 위해 관제탑에 요청하는 것과 유사하다&#46; 

- 연결 설정
    - 드라이버는 데이터베이스 서버에 로그인하고 필요한 설정을 수행하여 연결을 완료한다&#46; 

    - 이 과정은 네트워크 정보, 인증 자격 증명 등을 사용하여 이루어진다&#46; 

<a id="158eda9b0fe180c2a5b5da0721cf42af"></a>

2&#46; SQL 전송 및 실행

- SQL 명령 변환
    - 애플리케이션에서 발송된 SQL 명령을 받은 드라이버는 <strong><u>해당 명령을 데이터베이스가 이해할 수 있는 형태로 변환</u></strong>한다&#46; 

- 명령 처리
    - 변환된 명령은 데이터베이스 서버로 전송되어 실행된다&#46;

    - 데이터베이스는 쿼리를 처리하고, 요구된 데이터를 검색하거나 데이터에 변화를 준다&#46;

<a id="158eda9b0fe1801290a3d372a7d2ac5c"></a>

3&#46; 결과 처리

- 결과 수신
    - 데이터베이스에서 작업의 결과를 보내면, 드라이버는 이 결과를 받아 애플리케이션에서 실행할 수 있는 형태로 변환한다&#46; 

- 결과 전달
    - 최종적으로, 드라이버는 이 결과를 애플리케이션에 전달한다&#46; 

    - 애플리케이션은 이 정보를 사용자에게 표시하거나 다음 작업을 진행한다&#46; 

<a id="158eda9b0fe180dfbbe6cef35cb68290"></a>

4&#46; 연결 종료

- 연결 해제
    - 작업이 완료되면, 드라이버는 데이터베이스 서버와의 연결을 종료한다&#46; 

    - 자원을 정리하고 다음 세션을 위해 시스템을 초기화합니다&#46;

</details>
