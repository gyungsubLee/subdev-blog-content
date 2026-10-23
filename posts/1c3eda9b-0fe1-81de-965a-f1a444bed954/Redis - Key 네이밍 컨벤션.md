---
order: 11
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1c3eda9b-0fe1-81de-965a-f1a444bed954
title: Redis - Key 네이밍 컨벤션
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-81b8-a968-f6b1b2a79b94
    title: Redis
  - id: 1c3eda9b-0fe1-81c7-ae23-cfbc9fd6e83a
    title: 비전공자도 이해할 수 있는 Redis - 캐싱 [ 리펙토링 필요 ]
  - id: 1c3eda9b-0fe1-81de-965a-f1a444bed954
    title: Redis - Key 네이밍 컨벤션
excerpt: Redis - Key 네이밍 컨벤션 --- 📖 Redis애서 Key 이름은 굉장히 중요하다. 따라서 해당 챕터에서는 현업에서 자주 사용하는 Key 네이밍 컨벤션을 학습한다. - 필요에 따라 응용해서 사용 현업에서 자주 활용하는 네이밍 컨벤션 ✏️ 콜론(:)을 활용, 계층적으로 의미 구분 - 테이블명:PK:컬럼 - ex)
cover: null
icon: null
notionProperties:
  상태: 완료
schema_version: 1
parent_id: 1c3eda9b-0fe1-81c7-ae23-cfbc9fd6e83a
created: 2025-03-27T07:47:52.770Z
updated: 2025-03-27T07:47:52.770Z
legacy_path: Main/Redis-f6b1b2a79b94/비전공자도 이해할 수 있는 Redis - 캐싱 [ 리펙토링 필요 ]-cfbc9fd6e83a/Redis - Key 네이밍 컨벤션-f1a444bed954/index.md
legacy_category: Redis
source_url: https://beautiful-college-c84.notion.site/1c3eda9b0fe181de965af1a444bed954
---
<a id="1c3eda9b0fe1814c9b07edc6a2cb384a"></a>

## Redis &#45; Key 네이밍 컨벤션 

---

> 📖 
> 
> <a id="1c3eda9b0fe18100bd3ff140abc00345"></a>
> 
> Redis애서 <strong><u>Key 이름은 굉장히 중요</u></strong>하다&#46; 
> 
> <a id="1c3eda9b0fe181c09313f7bf53da8010"></a>
> 
> 따라서 해당 챕터에서는 <strong><u>현업에서 자주 사용</u></strong>하는 <strong><u>Key 네이밍 컨벤션</u></strong>을 학습한다&#46; 
> 
> - 필요에 따라 응용해서 사용

<details>
<summary>현업에서 자주 활용하는 네이밍 컨벤션</summary>

> ✏️ 
> 
> <a id="1c3eda9b0fe181f0b1bccfb137647e1c"></a>
> 
> <code>콜론</code>(<code>&#58;</code>)을 활용, <strong><u>계층적</u></strong>으로 <strong>의미 구분</strong>
> 
> - <strong><code>테이블명</code></strong><strong><code>&#58;</code></strong><strong><code>PK</code></strong><strong><code>&#58;</code></strong><strong><code>컬럼</code></strong>

- ex)
    - <strong><code>users</code></strong><strong><code>&#58;</code></strong><strong><code>100</code></strong><strong><code>&#58;</code></strong><strong><code>profile</code></strong>
        - <u>사용자들(users)</u> 중에서 <u>PK가 100</u>인 사용자(user)의 <u>프로필(profile)</u>

    - <strong><code>products</code></strong><strong><code>&#58;</code></strong><strong><code>123</code></strong><strong><code>&#58;</code></strong><strong><code>details</code></strong>
        - <u>상품들(products)</u> 중에서 <u>PK가 123</u>인 상품(product)의 <u>세부사항(details)</u>

- 해당 방식의 장점
    | 장점 | 설명 |
    | --- | --- |
    | <strong><code>가독성 향상</code></strong> | 데이터의 의미와 용도를 쉽게 파악할 수 있다&#46;  |
    | <strong><code>일관성</code></strong> | 컨벤션을 따름으로써 코드의 일관성을 높이고 유지보수가 쉬워진다&#46;  |
    | <strong><code>검색 및 필터링 용이</code></strong> | 패턴 매칭을 사용해 특정 유형의 Key를 쉽게 찾을 수 있다&#46; |
    | <strong><code>확장성</code></strong> | 서로 다른 Key와 이름이 겹쳐 충돌할 일이 적어진다&#46;  |

</details>
