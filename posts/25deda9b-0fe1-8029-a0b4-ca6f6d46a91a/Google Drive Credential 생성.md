---
order: 5
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 25deda9b-0fe1-8029-a0b4-ca6f6d46a91a
title: Google Drive Credential 생성
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 26deda9b-0fe1-8020-9b16-fdc2892a939e
    title: n8n
  - id: 257eda9b-0fe1-8046-a1e9-f6d115f59bb4
    title: 업무자동화 AI 에이전트 ( n8n )
  - id: 25deda9b-0fe1-8029-a0b4-ca6f6d46a91a
    title: Google Drive Credential 생성
excerpt: 목차 - Google Cloud - project - 1. Google Cloud Console - OAuth Client 생성 - 2. n8n Credentials 등록 - 1. Server Action Google Cloud - project 생성 - 상단 메뉴 - 프로젝트 선택 - 새 프로젝트 - 생성할 프로젝트 정
cover: fb3b1ee7da4a15e0.webp
icon: 9bed2eae1e079b4b.avif
notionProperties: {}
schema_version: 1
parent_id: 257eda9b-0fe1-8046-a1e9-f6d115f59bb4
created: 2025-08-28T10:29:35.731Z
updated: 2025-08-29T11:16:03.938Z
legacy_path: Main/n8n-fdc2892a939e/업무자동화 AI 에이전트 ( n8n )-f6d115f59bb4/Google Drive Credential 생성-ca6f6d46a91a/index.md
legacy_category: n8n
source_url: https://beautiful-college-c84.notion.site/25deda9b0fe18029a0b4ca6f6d46a91a
---
> 
> 
> <a id="25deda9b0fe181e99af9d6855c436388"></a>
> 
> <strong>목차</strong>
> 
> - [Google Cloud - project](#25deda9b0fe180b082c5c3ecd672df1f)
> - [1. Google Cloud Console - OAuth Client 생성](#25deda9b0fe180fb8b5cff87349138bf)
> - [2. n8n  Credentials 등록](#25deda9b0fe18079af53d9de26b11704)
> - [1. Server Action](#25deda9b0fe18178b32fc4dca3bce3c8)

<a id="25deda9b0fe180b082c5c3ecd672df1f"></a>

### Google Cloud &#45; project

<details>
<summary>생성</summary>

![](397ea6aaaad6682c.webp)

- 상단 메뉴 &#45; 프로젝트 선택 &#45; 새 프로젝트 

![](e23bf0a3af0bb652.webp)

- 생성할 프로젝트 정보 입력 및 생성
    - 프로젝트 이름 ( 이후 변경 불가 )

    - 조직 ( 있을 시 선택 )

![](b2139ee3cf13e303.webp)

- 위 화면과 같이 정상 생성된 것을 확인할 수 있음

</details>

<details>
<summary>삭제</summary>

![](26568145f2d0950c.webp)

- 왼쪽 메뉴 &#45; IAM 및 관리자 &#45; 리소스 관리

![](34e6af3508010197.webp)

- 삭제하려는 프로젝트 선택 &#45; 삭제 클릭

![](6981394fe84cb905.webp)

- 삭제 대기 중인 리소스로 해당 프로젝트 업로드?
    - 삭제하는데 시간이 걸림

</details>

<details>
<summary>3&#46; </summary>

![](8e39448c4ef7ab6b.webp)

![](ee30e81d3012a9af.webp)

</details>

<a id="25deda9b0fe18094bb65eecee2c4647f"></a>

‣

<a id="25deda9b0fe180fb8b5cff87349138bf"></a>

### 1&#46; Google Cloud Console &#45; <code>OAuth Client</code> 생성

> ✏️ 
> 
> <a id="25deda9b0fe180048b35e5e3c4e67d92"></a>
> 
> Google Drive API는 보통 <code>OAuth2</code>로 인증한다&#46; 
> 
> - ‣
> 
> - 유사 작업&#58; <a href="https://beautiful-college-c84.notion.site/218eda9b0fe18075bcaee4dd6de996c6">페이지</a> 

<details>
<summary>1&#46; Google Cloud Console 접속 → 프로젝트 생성</summary>

![](397ea6aaaad6682c.webp)

- 상단 메뉴 &#45; 프로젝트 선택 &#45; 새 프로젝트 

![](e23bf0a3af0bb652.webp)

- 생성할 프로젝트 정보 입력 및 생성
    - 프로젝트 이름 ( 이후 변경 불가 )

    - 조직 ( 있을 시 선택 )

![](b2139ee3cf13e303.webp)

- 위 화면과 같이 정상 생성된 것을 확인할 수 있음

</details>

<details>
<summary>2&#46; Google Drive API <code>enable(사용)</code> 설정</summary>

![](23f9af80c8c1f638.webp)

- 왼쪽 메뉴 &#45; API 및 서비스(<strong>API &#38; Services) &#45; 라이브러리(Library)</strong>

![](0e6b48ba77f94427.webp)

- Google Drive API 검색

![](755f9874a85bbabc.webp)

- Enable(사용) 클릭

</details>

<details>
<summary>3&#46; OAuth 클라이언트 ID 생성</summary>

- OAuth 클라이언트 ID를 만들려면 먼저 동의 화면을 구성해야 한다&#46;
    ![](f54662c4838c7759.webp)

    ![](8c23d235328a20e1.webp)

</details>

<a id="25deda9b0fe18079af53d9de26b11704"></a>

### 2&#46; n8n  Credentials 등록

![](a9e444c492431850.webp)

- 메인 화면 &#45; Credentials &#45; Add first credentails

![](2553d1f1003506a3.webp)

- <code>Google Drive OAuth2 API</code> 검색

<a id="25deda9b0fe18178b32fc4dca3bce3c8"></a>

## 1&#46; Server Action
