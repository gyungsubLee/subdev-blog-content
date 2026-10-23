---
order: 23
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1c3eda9b-0fe1-81e0-85d3-ed61eb5b8c62
title: git message template - local 설정
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-81f9-b76e-c9d937ee7825
    title: Git
  - id: 1c3eda9b-0fe1-819d-89dc-fb5c624de379
    title: "Note: Git CLI"
  - id: 1c3eda9b-0fe1-81e0-85d3-ed61eb5b8c62
    title: git message template - local 설정
excerpt: "템플릿 파일 생성 --- bash ~ : root 경로 ./: 현재 프로젝트 경로에 생성 nano 에디터를 사용해 파일 생성 및 메세지 작성 nano ,/.git-commit-template git template 지정 bash git message 템플릿 설정 git config commit.template [템플릿 파"
cover: null
icon: null
notionProperties:
  상태: 완료
schema_version: 1
parent_id: 1c3eda9b-0fe1-819d-89dc-fb5c624de379
created: 2025-03-27T07:47:52.779Z
updated: 2025-03-27T07:47:52.779Z
legacy_path: Main/Git-c9d937ee7825/Note- Git CLI-fb5c624de379/git message template - local 설정-ed61eb5b8c62/index.md
legacy_category: Git
source_url: https://beautiful-college-c84.notion.site/1c3eda9b0fe181e085d3ed61eb5b8c62
---
<a id="1c3eda9b0fe181f9b308c39fceebe3f0"></a>

### 템플릿 파일 생성

---

<a id="1c3eda9b0fe181b8baf1f717e60a73a1"></a>

```bash
# ~ : root 경로
# ./: 현재 프로젝트 경로에 생성 

# nano 에디터를 사용해 파일 생성 및 메세지 작성
nano ,/.git-commit-template
```

<a id="1c3eda9b0fe181168f79e8d552b643b2"></a>

### git template 지정

<a id="1c3eda9b0fe1811ba451c13ab8339e47"></a>

```bash
# git message 템플릿 설정
git config commit.template [템플릿 파일 path]

# --global: 전역 설정, 명시를 하지 않으면 특정 프로젝트에만 적용


# ex)
git config commit.template ./.git-message-template
```
