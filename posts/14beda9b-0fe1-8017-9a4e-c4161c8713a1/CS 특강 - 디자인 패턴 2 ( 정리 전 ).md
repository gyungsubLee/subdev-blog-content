---
order: 2
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 14beda9b-0fe1-8017-9a4e-c4161c8713a1
title: CS 특강 - 디자인 패턴 2 ( 정리 전 )
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 108eda9b-0fe1-80a6-8a2b-c21df3ab9492
    title: 내일 배움 캠프 ( 백엔드 코스 7기)
  - id: 152eda9b-0fe1-807b-9fea-d50a10c7203e
    title: 데이터베이스 특강 2 ( 정리 중 )
  - id: 14beda9b-0fe1-8017-9a4e-c4161c8713a1
    title: CS 특강 - 디자인 패턴 2 ( 정리 전 )
excerpt: "📌 CS 특강 - 디자인 패턴 - 진행: 이태현 튜터님 - 기간: 24.11.27(수) - reference: [[241127] CS 특강 - 디자인 원칙과 패턴 2 [이태현 튜터님]](%5B241127%5D%20CS%20%ED%8A%B9%EA%B0%95%20-%20%EB%94%94%EC%9E%90%EC%9D%B8%20"
cover: null
icon: 🎨
notionProperties: {}
schema_version: 1
parent_id: 152eda9b-0fe1-807b-9fea-d50a10c7203e
created: 2024-11-27T00:40:53.828Z
updated: 2026-02-24T22:54:31.291Z
legacy_path: Main/내일 배움 캠프 ( 백엔드 코스 7기)-c21df3ab9492/데이터베이스 특강 2 ( 정리 중 )-d50a10c7203e/CS 특강 - 디자인 패턴 2 ( 정리 전 )-c4161c8713a1/index.md
legacy_category: 내일 배움 캠프 ( 백엔드 코스 7기)
source_url: https://beautiful-college-c84.notion.site/14beda9b0fe180179a4ec4161c8713a1
---
> 📌 
> 
> <a id="1ea925fa5da44f14b04927bf56363e40"></a>
> 
> CS 특강 &#45; 디자인 패턴
> 
> - 진행&#58; 이태현 튜터님
> 
> - 기간&#58; 24&#46;11&#46;27(수) 
> 
> - reference&#58; 
> 
> [[241127] CS 특강 - 디자인 원칙과 패턴 2 [이태현 튜터님]](#/post/18feda9b-0fe1-80fe-bc18-e1fd06b2e96e)

<details>
<summary>reference</summary>

<a id="157eda9b0fe18007b9c1d030207e3c26"></a>

‣

<a id="157eda9b0fe180c28c8ae2e73fee7eae"></a>

<a href="https://beautiful-college-c84.notion.site/46eaee0e5e154011bc839dc525947dab">페이지</a> 

[design_pattern.zip](7a25496654d0d839.zip)

</details>

<a id="8f19426e8eff41ac9834fee0dd9ba0bc"></a>

### 2&#46; 

<a id="14beda9b0fe180e49228fecd85ad5ebb"></a>

고정적이지 않는 것을 

<a id="14beda9b0fe1801f9eace87ed81e71f2"></a>

모놀로식 아키텍처

<a id="14beda9b0fe180cfa412ce8f47091f70"></a>

→ MSA, 도메인 분산 아키텍처 

<a id="14beda9b0fe1806284fff360f0ff63a6"></a>

→ 실무에서는 앱이 커지면 어쩔 수 없기 변경할 수 밖에 없는 이유이다&#46; 

<a id="14beda9b0fe18021b651defd3f5fad0b"></a>

테스트 코드 

<a id="14beda9b0fe180ec9cb7e2d02c95031b"></a>

싱글톤 패턴으로 객체를 관리하는 경우, 

<a id="14beda9b0fe180c48630fe55bcb07771"></a>

더블 체크 락

<a id="14ceda9b0fe18051b33eff23198b1a3b"></a>

### 질문

---

- 빌더 패턴의 경우, setter를 통해 필드 값을 설정하고 Builder를 객체를 생성자에 넘기기 때문에<br>생성자만 사용하는 경우와  다르게  ‘필드의 값을 강제할 수 없다’라는 단점이 있다고 알고 있는데, <br>이런 경우 어떻게 해결 가능한지 의문점이 듭니다&#46;
    - 롬복 경우, 커스터마이징을 통해 가능은 하다

- 예제로 사용한 코드는 강의 자료에 같이 공유가 될까요?


- 팩토리 코드


<a id="14ceda9b0fe180b49831f104adb4154d"></a>

NumberFormat&#46;getCu
