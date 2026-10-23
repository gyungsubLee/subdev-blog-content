---
order: 49
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 13ceda9b-0fe1-80bc-9f2a-f77cf3b45ca0
title: CS 특강 - oop & 디자인 패턴 ( 정리 전 )
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 108eda9b-0fe1-80a6-8a2b-c21df3ab9492
    title: 내일 배움 캠프 ( 백엔드 코스 7기)
  - id: 13ceda9b-0fe1-80bc-9f2a-f77cf3b45ca0
    title: CS 특강 - oop & 디자인 패턴 ( 정리 전 )
excerpt: "📌 CS 특강 - oop & 디자인 패턴 - 진행: 이태현 튜터님 - 기간: 24.11.13(수) - Reference: [[241113] CS 특강 - 디자인 원칙과 패턴 1 [이태현 튜터님]](%5B241113%5D%20CS%20%ED%8A%B9%EA%B0%95%20-%20%EB%94%94%EC%9E%90%EC%9D"
cover: null
icon: 🎨
notionProperties: {}
schema_version: 1
parent_id: 108eda9b-0fe1-80a6-8a2b-c21df3ab9492
created: 2024-11-12T01:37:16.754Z
updated: 2026-04-03T04:55:42.547Z
legacy_path: Main/내일 배움 캠프 ( 백엔드 코스 7기)-c21df3ab9492/CS 특강 - oop & 디자인 패턴 ( 정리 전 )-f77cf3b45ca0/index.md
legacy_category: 내일 배움 캠프 ( 백엔드 코스 7기)
source_url: https://beautiful-college-c84.notion.site/13ceda9b0fe180bc9f2af77cf3b45ca0
---
> 📌 
> 
> <a id="2aaf33e2bfca4ad99f1946bb7fee6fb7"></a>
> 
> CS 특강 &#45; oop &#38; 디자인 패턴
> 
> - 진행&#58; 이태현 튜터님
> 
> - 기간&#58; 24&#46;11&#46;13(수) 
> 
> - Reference&#58; 
> 
> [[241113] CS 특강 - 디자인 원칙과 패턴 1 [이태현 튜터님]](#/post/18feda9b-0fe1-8075-984e-fdeba956376d)

<details>
<summary>Reference</summary>

<a id="158eda9b0fe1801bae31f187e83389a9"></a>

<a href="https://beautiful-college-c84.notion.site/cc7bd616fb6b4212b5e9d873153fb7da">페이지</a> 

<a id="158eda9b0fe180a7a45afa9ff3b36345"></a>

‣

</details>

> 🧷 
> 
> <a id="18feda9b0fe180489326c9379f37b9a4"></a>
> 
> 지난 시간엔 데이터베이스 설계와 기능(트랜잭션, 락)에 대해서 알아보았습니다&#46;<br>이번 특강에서는 좋은 코드를 작성하기 위한 원칙과 패턴에 대해서 알아보고자 합니다&#46;
> 
> <a id="18feda9b0fe1807fac9dee0210813f87"></a>
> 
> 아래 원칙과 패턴들을 활용하여 현재 우리가 사용하는 Java와 Spring 코드가 만들어졌음을 이해하고 하나씩 정립해 가시면 좋겠습니다&#46;
> 
> <a id="18feda9b0fe180d1aa6de12246dfdc52"></a>
> 
> 아직 구현에 익숙하지 않으신 분은 이러한 개념들이 있다는 것을 알아주셨으면 합니다&#46;
> 
> <a id="18feda9b0fe180d18f06ed09674a549a"></a>
> 
> <strong>해당 원칙들과 다자인 패턴은 기술면접에서도 단골 질문들입니다&#46;</strong>
> 
> <a id="18feda9b0fe18061b258dac738401584"></a>
> 
> <strong>(주의)</strong>
> 
> <a id="18feda9b0fe18099a669d31f06d2533b"></a>
> 
> <strong>해당 내용을 무리하게 적용하려고 하지마세요&#33;&#33;&#33; <br>원칙과 패턴을 잘못 적용하게 되면 오히려 유지보수를 헤치게 됩니다&#33;&#33;&#33;</strong>
