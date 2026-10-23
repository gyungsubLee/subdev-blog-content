---
order: 100
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: fffeda9b-0fe1-8109-a0b8-faf0a0d1cf29
title: Lv5. 예산이 가장 큰 프로젝트는?
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 108eda9b-0fe1-80a6-8a2b-c21df3ab9492
    title: 내일 배움 캠프 ( 백엔드 코스 7기)
  - id: fffeda9b-0fe1-8109-a0b8-faf0a0d1cf29
    title: Lv5. 예산이 가장 큰 프로젝트는?
excerpt: 📖 SQL의 기본적인 쿼리문을 작성할 수 있다면, 달리기반 과제에 도전해보아요. 단순 문법을 사용하는 것 뿐 아니라 내가 정말 원하는 데이터를 출력하기 위한 한 걸음이 될 거예요! 💪🏻과제를 수행하고나 나면 할 수 있어요! - 서브쿼리를 활용해 특정 조건을 만족하는 데이터를 필터링하고, 이를 메인 쿼리에서 활용할 수
cover: null
icon: 🦚
notionProperties: {}
schema_version: 1
parent_id: 108eda9b-0fe1-80a6-8a2b-c21df3ab9492
created: 2024-09-23T11:03:34.061Z
updated: 2024-09-23T11:04:12.791Z
legacy_path: Main/내일 배움 캠프 ( 백엔드 코스 7기)-c21df3ab9492/Lv5. 예산이 가장 큰 프로젝트는--faf0a0d1cf29/index.md
legacy_category: 내일 배움 캠프 ( 백엔드 코스 7기)
source_url: https://beautiful-college-c84.notion.site/fffeda9b0fe18109a0b8faf0a0d1cf29
---
> 📖 SQL의 기본적인 쿼리문을 작성할 수 있다면, 달리기반 과제에 도전해보아요&#46; <br>단순 문법을 사용하는 것 뿐 아니라 내가 정말 원하는 데이터를 출력하기 위한 한 걸음이 될 거예요&#33; 

<a id="fffeda9b0fe181e3a00fe1df7679a719"></a>

### 💪🏻과제를 수행하고나 나면 할 수 있어요&#33;

- 서브쿼리를 활용해 특정 조건을 만족하는 데이터를 필터링하고, 이를 메인 쿼리에서 활용할 수 있다&#46;

- 특정 조건을 기준으로 데이터를 분석하고, 원하는 결과를 추출할 수 있다&#46; 

- 다중 테이블 간의 관계를 이해할 수 있다&#46; 

> ⚡ <strong>Notification&#58; 과제 시작 전 확인할 내용&#33;</strong>

<a id="fffeda9b0fe18190a7c3f589129ca264"></a>

### ✅ 과제 시작 전 다음 내용을 셀프 체크해보세요&#46; 

- [ ] <code>SELECT</code>, <code>FROM</code>, <code>WHERE</code>, <code>JOIN</code> 등의 기본 SQL 문법을 잘 이해하고 있어야 한다&#46;

- [ ]  서브쿼리를 사용해 메인 쿼리의 조건을 강화하거나, 필터링에 활용하는 방법을 이해해야 한다&#46;

- [ ] <code>WHERE</code> 절과 서브쿼리를 결합해 특정 조건을 만족하는 데이터를 필터링할 수 있어야 한다&#46;

- [ ] 테이블 간의 관계를 파악하고, 이를 기반으로 데이터를 조인하는 방법을 알고 있다&#46;

<a id="fffeda9b0fe18177a81ee27157b12a35"></a>

<a href="https://beautiful-college-c84.notion.site/6969102902394ba3998014546ede7e9f">페이지</a> 

> 🍀 <strong>본격적으로 시작해 볼까요?</strong>

<a id="fffeda9b0fe181aea522ec40d3f9adf7"></a>

### 문제&#58;

<a id="fffeda9b0fe181db85d8f698bd13fe9e"></a>

<strong>Employees</strong> 테이블&#58;

| EmployeeID | Name | Department | Salary |
| --- | --- | --- | --- |
| 1 | Alice | HR | 5000 |
| 2 | Bob | IT | 7000 |
| 3 | Charlie | IT | 6000 |
| 4 | David | HR | 4500 |
| 5 | Eve | Sales | 5500 |
| 6 | Frank | IT | 7200 |

<a id="fffeda9b0fe181589706ed5c18c02a52"></a>

<strong>Projects</strong> 테이블&#58;

| ProjectID | ProjectName | Budget |
| --- | --- | --- |
| 101 | Alpha | 10000 |
| 102 | Beta | 15000 |
| 103 | Gamma | 12000 |
| 104 | Delta | 8000 |

<a id="fffeda9b0fe18191aa15d6fb930cfb2e"></a>

<strong>EmployeeProjects</strong> 테이블&#58;

| EmployeeID | ProjectID |
| --- | --- |
| 1 | 101 |
| 2 | 101 |
| 3 | 102 |
| 4 | 103 |
| 5 | 104 |
| 6 | 102 |
| 6 | 103 |

<a id="fffeda9b0fe181528f54e580c44535b9"></a>

### 요구사항&#58;

1. 각 직원이 속한 부서에서 가장 높은 월급을 받는 직원들만 포함된 결과를 조회하는 SQL 쿼리를 작성해주세요&#46;
    1.  출력 결과에는 직원의 이름, 부서, 그리고 월급이 포함되어야 합니다&#46; 

    1. 기대 결과
        | Name | Department | Salary |
        | --- | --- | --- |
        | Alice | HR | 5000 |
        | Frank | IT | 7200 |
        | Eve | Sales | 5500 |

1. 직원이 참여한 프로젝트 중 예산이 10,000 이상인 프로젝트만을 조회하는 SQL 쿼리를 작성해주세요&#46; 
    1. 출력 결과에는 직원 이름, 프로젝트 이름, 그리고 프로젝트 예산이 포함되어야 합니다&#46; 
        | Name | ProjectName | Budget |
        | --- | --- | --- |
        | Bob | Beta | 15000 |
        | Charlie | Beta | 15000 |
        | Frank | Beta | 15000 |
        | David | Gamma | 12000 |
        | Frank | Gamma | 12000 |

<a id="fffeda9b0fe1813eb3b0eecd404e1181"></a>

### 제약사항&#58;

- 두 쿼리 모두 서브쿼리를 사용해주세요&#46; 

- 서브쿼리를 통해 특정 조건을 만족하는 데이터를 필터링하고, 그 결과를 최종 쿼리에 반영해야 합니다&#46; 

> 🔥 <strong>완료하셨다면?</strong>

- <strong>원활하게 작동되는 정답코드를 퀘스트로 제출해주세요 👉 </strong><strong><a href="https://forms.gle/pomadzyiNKAyw4CB8">https&#58;//forms&#46;gle/pomadzyiNKAyw4C</a></strong>
