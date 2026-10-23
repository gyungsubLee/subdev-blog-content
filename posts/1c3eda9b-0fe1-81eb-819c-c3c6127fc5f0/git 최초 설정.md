---
order: 4
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1c3eda9b-0fe1-81eb-819c-c3c6127fc5f0
title: git 최초 설정
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-81f9-b76e-c9d937ee7825
    title: Git
  - id: 1c3eda9b-0fe1-819d-89dc-fb5c624de379
    title: "Note: Git CLI"
  - id: 1c3eda9b-0fe1-81eb-819c-c3c6127fc5f0
    title: git 최초 설정
excerpt: Git 전역으로 사용자 이름과 이메일 주소 설정하기 → github 계정과 별개임 - 설정 bash git config --global user.name "(본인 이름)" bash git config --global user.email "(본인 이메일)" - 확인 bash git config --global user.na
cover: null
icon: null
notionProperties:
  상태: 완료
schema_version: 1
parent_id: 1c3eda9b-0fe1-819d-89dc-fb5c624de379
created: 2025-03-27T07:47:52.781Z
updated: 2025-03-27T07:47:52.781Z
legacy_path: Main/Git-c9d937ee7825/Note- Git CLI-fb5c624de379/git 최초 설정-c3c6127fc5f0/index.md
legacy_category: Git
source_url: https://beautiful-college-c84.notion.site/1c3eda9b0fe181eb819cc3c6127fc5f0
---
> Git 전역으로 사용자 이름과 이메일 주소 설정하기<br> → github 계정과 별개임

- 설정

<a id="1c3eda9b0fe1814d9b01c59a583a9f6d"></a>

```bash
git config --global user.name "(본인 이름)"
```

<a id="1c3eda9b0fe181078a4adf4185a963c3"></a>

```bash
git config --global user.email "(본인 이메일)"
```

- 확인

<a id="1c3eda9b0fe181258c81f16ac861cfc9"></a>

```bash
git config --global user.name
```

<a id="1c3eda9b0fe181839349ed324d574921"></a>

```bash
git config --global user.email
```

- 기본 브랜치명 변경

<a id="1c3eda9b0fe1810dbb39ca078daa148b"></a>

```bash
git config --global init.defaultBranch main
```

- 프로젝트 생성 &#45; git initialize

<a id="1c3eda9b0fe1810ab38aead5d9d75d7e"></a>

```bash
git init
```

- 파일 상태

> 👉🏻 자세한 내용  <a href="#/post/1c3eda9b-0fe1-81db-b05a-c2afad5ca59f">페이지</a> 확인

<a id="1c3eda9b0fe181a0b8dbe7e179e724ee"></a>

```bash
git status
```
