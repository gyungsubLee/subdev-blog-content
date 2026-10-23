---
order: 11
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 224eda9b-0fe1-80fc-abb4-d19e7ed2757e
title: Case3 - 확장성을 고려한 프로젝트 ( Code Deploy ) [ 실습 필요 ]
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-817b-9c95-d96fd53640c4
    title: CI/CD
  - id: 227eda9b-0fe1-80d6-bacc-e93ff1df19a3
    title: 비전공자도 이해할 수 있는 CI/CD 입문·실전
  - id: 224eda9b-0fe1-80fc-abb4-d19e7ed2757e
    title: Case3 - 확장성을 고려한 프로젝트 ( Code Deploy ) [ 실습 필요 ]
excerpt: 확장성을 고려한 프로젝트 구성 ( Code Deploy ) --- ✏️ 서버를 여러 대 이상 구동하거나 무중단 베포가 중요한 서비스일 떄 주로 활용한다. CodeDeploy 사용 이유 [CodeDeploy란 무엇인가요? - AWS CodeDeploy]() - CodeDeploy는 수많은 AWS EC2에 베포를 쉽게 할 수
cover: null
icon: null
notionProperties: {}
schema_version: 1
parent_id: 227eda9b-0fe1-80d6-bacc-e93ff1df19a3
created: 2025-07-02T08:49:35.557Z
updated: 2025-07-05T04:30:13.916Z
legacy_path: Main/CI-CD-d96fd53640c4/비전공자도 이해할 수 있는 CI-CD 입문·실전-e93ff1df19a3/Case3 - 확장성을 고려한 프로젝트 ( Code Deploy ) [ 실습 필요-d19e7ed2757e/index.md
legacy_category: CI/CD
source_url: https://beautiful-college-c84.notion.site/224eda9b0fe180fcabb4d19e7ed2757e
---
<a id="224eda9b0fe18084a348c819ca0c5778"></a>

## 확장성을 고려한 프로젝트 구성 ( Code Deploy ) 

---

![](b043785d54a31d40.webp)

> ✏️ 
> 
> <a id="224eda9b0fe180ea8355d21dd55f14ff"></a>
> 
> 서버를 여러 대 이상 구동하거나 무중단 베포가 중요한 서비스일 떄 주로 활용한다&#46; 

<a id="224eda9b0fe1804d8f0bec945e5f5b58"></a>

### CodeDeploy 사용 이유

[CodeDeploy란 무엇인가요? &#45; AWS CodeDeploy]()

- CodeDeploy는 수많은 AWS EC2에 베포를 쉽게 할 수 있도록 도와준다&#46; 

- CodeDeploy에 무중단 베포 기능이 내재되어 있어 손쉽게 무중단 베포를 진행할 수 있다&#46; 

<a id="224eda9b0fe1800c9552cca11b9e0cfb"></a>

### 장• 단점

> ✅ 
> 
> <a id="224eda9b0fe180cdb0f3ed846a6c3094"></a>
> 
> <strong>장점</strong>
> 
> - 여러 서버를  구축한 상황에서도 쉽게 자동 베포가 가능하다&#46; 
> 
> - 손쉽게 무중단 베포를 적용할 수 있다&#46;

> ❗ 
> 
> <a id="224eda9b0fe1809783d6f94285b53b8a"></a>
> 
> <strong>단점</strong>
> 
> - CodeDeploy를 사용함으로써 인프라 구조가 복잡해졌다&#46; 
> 
> - 구조가 복잡해진만큼 관리 비용, 유지보수 비용, 구현 난이도, 트러블 슈팅 어려움, 복잡도 등이 증가했다&#46;

<a id="224eda9b0fe18039858dc076aa65ee7e"></a>

## &#91; 실습 &#93; CI/CD 구축

---

<a id="224eda9b0fe1803ab81fe59278d59b25"></a>

### CodeDeploy 셋팅 / IAM 설정
