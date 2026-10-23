---
order: 98
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: fffeda9b-0fe1-8127-82d2-d3b05d34bef7
title: Lv4. 가장 높은 월급을 받는 직원은?
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 108eda9b-0fe1-80a6-8a2b-c21df3ab9492
    title: 내일 배움 캠프 ( 백엔드 코스 7기)
  - id: fffeda9b-0fe1-8127-82d2-d3b05d34bef7
    title: Lv4. 가장 높은 월급을 받는 직원은?
excerpt: "📖 SQL의 기본적인 쿼리문을 작성할 수 있다면, 달리기반 과제에 도전해보아요. 단순 문법을 사용하는 것 뿐 아니라 내가 정말 원하는 데이터를 출력하기 위한 한 걸음이 될 거예요! 💪🏻과제를 수행하고나 나면 할 수 있어요! - JOIN, 서브쿼리, GROUP BY, HAVING 등 SQL 기능을 조합하여 사용할 수 "
cover: null
icon: 💸
notionProperties: {}
schema_version: 1
parent_id: 108eda9b-0fe1-80a6-8a2b-c21df3ab9492
created: 2024-09-23T11:03:34.060Z
updated: 2024-09-23T11:04:12.791Z
legacy_path: Main/내일 배움 캠프 ( 백엔드 코스 7기)-c21df3ab9492/Lv4. 가장 높은 월급을 받는 직원은--d3b05d34bef7/index.md
legacy_category: 내일 배움 캠프 ( 백엔드 코스 7기)
source_url: https://beautiful-college-c84.notion.site/fffeda9b0fe1812782d2d3b05d34bef7
---
> 📖 SQL의 기본적인 쿼리문을 작성할 수 있다면, 달리기반 과제에 도전해보아요&#46; <br>단순 문법을 사용하는 것 뿐 아니라 내가 정말 원하는 데이터를 출력하기 위한 한 걸음이 될 거예요&#33; 

<a id="fffeda9b0fe181ce9443ed6b0696f20a"></a>

### 💪🏻과제를 수행하고나 나면 할 수 있어요&#33;

- <code>JOIN</code>, 서브쿼리, <code>GROUP BY</code>, <code>HAVING</code> 등 SQL 기능을 조합하여 사용할 수 있다&#46; 

- <code>GROUP BY</code>와 <code>HAVING</code>을 사용해 특정 조건을 만족하는 집계 결과를 필터링할 수 있다&#46;

- 여러 테이블을 연결하고 필요한 데이터를 추출할 수 있는 능력을 기를 수 있다&#46;

- 쿼리의 성능을 고려해 필요한 데이터를 가장 효율적으로 얻을 수 있는 방법을 찾는 능력을 기를 수 있다&#46; 

> ⚡ <strong>Notification&#58; 과제 시작 전 확인할 내용&#33;</strong>

<a id="fffeda9b0fe1815bb3ebfcb2d07fb5b7"></a>

### ✅ 과제 시작 전 다음 내용을 셀프 체크해보세요&#46; 

- [ ] <code>SELECT</code>, <code>FROM</code>, <code>WHERE</code>, <code>JOIN</code> 등의 기본적인 SQL 문법과 구조에 대한 이해

- [ ] <code>COUNT</code>, <code>SUM</code>, <code>AVG</code>, <code>MAX</code>, <code>MIN</code> 등 집계 함수의 사용법

- [ ] 서브쿼리(내부 쿼리)의 개념과 사용법, 그리고 이를 메인 쿼리와 결합하는 방법

- [ ] <code>HAVING</code> 절을 사용해 그룹화된 데이터에서 특정 조건을 만족하는 결과만 필터링하는 방법

<a id="fffeda9b0fe18157af60c929f13df091"></a>

<a href="https://beautiful-college-c84.notion.site/6969102902394ba3998014546ede7e9f">페이지</a> 

> 🍀 <strong>본격적으로 시작해 볼까요?</strong>

<a id="fffeda9b0fe1812682fbdb0be6e0a356"></a>

<strong>Employees</strong> 테이블&#58;

| EmployeeID | Name | Department | Salary | ManagerID |
| --- | --- | --- | --- | --- |
| 1 | Alice | HR | 70000 | NULL |
| 2 | Bob | IT | 90000 | 1 |
| 3 | Charlie | IT | 80000 | 2 |
| 4 | David | IT | 85000 | 2 |
| 5 | Eve | HR | 75000 | 1 |
| 6 | Frank | Finance | 95000 | NULL |
| 7 | Grace | Finance | 80000 | 6 |
| 8 | Heidi | IT | 95000 | 2 |

<a id="fffeda9b0fe181ec8f99fc73b6af3a39"></a>

### 요구사항&#58;

1. 각 직원의 이름, 부서, 월급, 그리고 그 직원이 속한 부서에서 가장 높은 월급을 받고 있는 직원의 이름과 월급을 조회하는 SQL 쿼리를 작성해주세요&#46; 
    1. 기대결과
        | Name | Department | Salary | Top&#95;Earner | Top&#95;Salary |
        | --- | --- | --- | --- | --- |
        | Alice | HR | 70000 | Eve | 75000 |
        | Bob | IT | 90000 | Heidi | 95000 |
        | Charlie | IT | 80000 | Heidi | 95000 |
        | David | IT | 85000 | Heidi | 95000 |
        | Eve | HR | 75000 | Eve | 75000 |
        | Frank | Finance | 95000 | Frank | 95000 |
        | Grace | Finance | 80000 | Frank | 95000 |
        | Heidi | IT | 95000 | Heidi | 95000 |

1. 부서별로 평균 월급이 가장 높은 부서의 이름과 해당 부서의 평균 월급을 조회하는 SQL 쿼리를 작성해주세요&#46;
    1. 기대결과
        | Department | Avg&#95;Salary |
        | --- | --- |
        | IT | 87500 |

<a id="fffeda9b0fe181ce9ae4dff7453d5c56"></a>

### 제약사항&#58;

- 두 쿼리 모두 서브쿼리, <code>JOIN</code>, <code>GROUP BY</code>, <code>HAVING</code> 등의 기능을 활용해주세요&#46; 

> 🔥 <strong>완료하셨다면?</strong>

- <strong>원활하게 작동되는 정답코드를 퀘스트로 제출해주세요 👉 </strong><strong><a href="https://forms.gle/pomadzyiNKAyw4CB8">https&#58;//forms&#46;gle/pomadzyiNKAyw4C</a></strong>
