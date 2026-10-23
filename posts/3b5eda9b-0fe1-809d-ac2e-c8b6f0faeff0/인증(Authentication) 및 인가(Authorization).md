---
order: 3
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 3b5eda9b-0fe1-809d-ac2e-c8b6f0faeff0
title: 인증(Authentication) 및 인가(Authorization)
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-817c-b119-d6a1706fbaf8
    title: 대규모 시스템 설계
  - id: 39feda9b-0fe1-80af-b2fb-e0517980dbb9
    title: MSA 환경에서 REST API, gRPC, GraphQL로 마스터하는 백엔드 API 개발
  - id: 3b5eda9b-0fe1-809d-ac2e-c8b6f0faeff0
    title: 인증(Authentication) 및 인가(Authorization)
excerpt: API Gateway에서 인증 및 인가 처리 방법 --- API Gateway에서의 인증, 인가 ✏️ API Gateway에서 인증 및 인가 처리의 중요성 - 보안 강화 - 확장성 및 유연성 제공 - 효율적인 관리 및 유지보수 - 사용자 경험 개선 - 규정 준수 및 표준화 지원 API Gateway의 역할 - 어플리케이션
cover: null
icon: null
notionProperties:
  상태: 완료
schema_version: 1
parent_id: 39feda9b-0fe1-80af-b2fb-e0517980dbb9
created: 2026-08-07T12:20:05.820Z
updated: 2026-10-01T09:10:53.485Z
legacy_path: Main/대규모 시스템 설계-d6a1706fbaf8/MSA 환경에서 REST API, gRPC, GraphQL로 마스터하는 백엔드 A-e0517980dbb9/인증(Authentication) 및 인가(Authorization)-c8b6f0faeff0/index.md
legacy_category: 대규모 시스템 설계
source_url: https://beautiful-college-c84.notion.site/3b5eda9b0fe1809dac2ec8b6f0faeff0
---
<a id="3ebeda9b0fe180d7b7d1dc5f96a8b62f"></a>

## API Gateway에서 인증 및 인가 처리 방법

---

<a id="3ebeda9b0fe180fd96d1d5bcfe2869f8"></a>

###  API Gateway에서의 인증, 인가 

> ✏️ 
> 
> <a id="3ebeda9b0fe180439848f4f3e45227d2"></a>
> 
> API Gateway에서 인증 및 인가 처리의 중요성
> 
> - <code>보안 강화</code>
> 
> - <code>확장성 및 유연성 제공</code>
> 
> - <code>효율적인 관리 및 유지보수</code>
> 
> - <code>사용자 경험 개선</code>
> 
> - <code>규정 준수 및 표준화 지원</code>

<details>
<summary>API Gateway의 역할</summary>

![](4e05e72ba8484740.webp)

- 어플리케이션과 백엔드 서비스 간의 통신을 중개하는 역할

</details>

<details>
<summary>API Gateway에서 인증 (Authentication)</summary>

- <code>인증의 종류</code>
    - 기본 인증 (Basic Authentication)

    - 토큰 기반 인증 (Token&#45;based Authentication)
        - ex) JWT (JSON Web Tokens)

    - OAuth, OpenID Connect 같은 제 3자 인증 방법론

- <code>API Gateway에서의 역할</code>
    - API 요청을 받을 때마다 요청자의 신원을 확인

    - 올바른 자격 증명 없이는 접근 불가능하도록 제한

</details>

<details>
<summary>API Gateway에서 인가 (Authorization)</summary>

- 인가의 종류
    - 역할 기반 접근 제어 (<code>RBAC&#58; Role&#45;Based Access Control</code>)

    - 속성 기반 접근 제어 (<code>ABAC&#58; Attribute&#45;Based Access Control</code>)

    - 정책 기반 접근 제어 (<code>PBAC&#58; Policy&#45;Based Access Control</code>)

- API Gateway에서의 역할
    - 인증된 사용자 요청에 대해 허용된 작업만 수행하도록 관리

    - 사용자의 역할과 권한에 따라 자원 접근을 제어

</details>

<a id="3ebeda9b0fe18082b3e2ca79e55e9530"></a>

###  API Gateway에서 인증 및 인가 구현을 위한 여러가지 패턴

> ✏️ 
> 
> - 직접 인증
> 
> - 백엔드로 토큰 전달
> 
> - 외부 인증 서비스 
> 
> - API 키 관리

<details>
<summary>API Gateway에서 인증 및 인가 구현을 위한 여러가지 패턴&#58; <code>직접 인증</code></summary>

![](ee96ce0f494dd49e.webp)

</details>

<details>
<summary>API Gateway에서 인증 및 인가 구현을 위한 여러가지 패턴&#58; <code>백엔드로 토큰 전달</code></summary>

![](fd0f0755451b08ce.webp)

</details>

<details>
<summary>API Gateway에서 인증 및 인가 구현을 위한 여러가지 패턴&#58; <code>외부 인증 서비스</code></summary>

![](cc383a1d2b93a692.webp)

</details>

<details>
<summary>API Gateway에서 인증 및 인가 구현을 위한 여러가지 패턴&#58; <code>API 키 관리</code></summary>

![](1b05132bdb9c475b.webp)

</details>
