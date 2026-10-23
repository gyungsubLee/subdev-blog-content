---
order: 19
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1c3eda9b-0fe1-817a-a7c5-d6f72f5db7af
title: github 환경변수 설정
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-81f9-b76e-c9d937ee7825
    title: Git
  - id: 1c3eda9b-0fe1-819d-89dc-fb5c624de379
    title: "Note: Git CLI"
  - id: 1c3eda9b-0fe1-817a-a7c5-d6f72f5db7af
    title: github 환경변수 설정
excerpt: 페이지 Gitbub에서 action의 환경변수 설정하기 --- 환경변수 설정 1. 환경변수 설정 화면으로 이동 - 환경변수를 설정하고자 하는 repository로 이동 - setting - Secrets and variables - Actaions - .github/workspaces/.yml의 환경 변수 - Codesp
cover: null
icon: null
notionProperties:
  상태: 완료
schema_version: 1
parent_id: 1c3eda9b-0fe1-819d-89dc-fb5c624de379
created: 2025-03-27T07:47:52.779Z
updated: 2025-03-27T07:47:52.779Z
legacy_path: Main/Git-c9d937ee7825/Note- Git CLI-fb5c624de379/github 환경변수 설정-d6f72f5db7af/index.md
legacy_category: Git
source_url: https://beautiful-college-c84.notion.site/1c3eda9b0fe1817aa7c5d6f72f5db7af
---
> <a href="#/post/1c3eda9b-0fe1-8114-a6b3-c20271564094">페이지</a> 

<a id="1c3eda9b0fe1811e8c12c4a41c279a2f"></a>

## Gitbub에서 action의 환경변수 설정하기 

---

<a id="1c3eda9b0fe1813d8fb5d53a73d0e7f4"></a>

### 환경변수 설정

<details>
<summary>1&#46; 환경변수 설정 화면으로 이동</summary>

![](90476b923ad127c0.webp)

- 환경변수를 설정하고자 하는 repository로 이동

- setting &#45; Secrets and variables 
    - Actaions &#45; <code>&#46;github/workspaces/&#46;yml</code>의 환경 변수 

    - Codespaces

    - Dependbot

- new repository secret 클릭

</details>

<details>
<summary>2&#46;  환결변수 설정 &#45; 환경 변수의 key, value 값 정의</summary>

![](8b72cf0942132afd.webp)

</details>

<details>
<summary>3&#46; 아래와 같이 생성한 변수들의 목록을 확인 가능</summary>

![](2851542c81eb216b.webp)

</details>

<a id="1c3eda9b0fe18131a7eec47db4d1a666"></a>

### 환경변수의 value 값 업데이트 

<details>
<summary>1&#46; 수정 버튼 클릭</summary>

![](c01772a21d8d7b68.webp)

</details>

<details>
<summary>2&#46; value 값 업데이트 </summary>

- 이전에 생성한 값은 다시 볼 수 없음, 덮어쓰기

![](e12fca9f8b4a9f43.webp)

</details>
