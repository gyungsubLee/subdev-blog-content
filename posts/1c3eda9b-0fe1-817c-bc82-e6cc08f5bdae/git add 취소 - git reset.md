---
order: 11
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1c3eda9b-0fe1-817c-bc82-e6cc08f5bdae
title: git add 취소 - git reset
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-81f9-b76e-c9d937ee7825
    title: Git
  - id: 1c3eda9b-0fe1-819d-89dc-fb5c624de379
    title: "Note: Git CLI"
  - id: 1c3eda9b-0fe1-817c-bc82-e6cc08f5bdae
    title: git add 취소 - git reset
excerpt: "- reset 명령어를 이용하여 전체 파일을 unstaged 상태로 되돌릴 수 있다 bash git reset - reset 뒤에 파일명을 입력을 하면 개별로 취소 가능 bash git reset HEAD [파일명]"
cover: null
icon: null
notionProperties:
  point: git unstaged 상태로 되돌리기
  Reference: "[https://shape-coding.tistory.com/entry/Git-Git-Add-%EC%B7%A8%EC%86%8C%ED%95%98%EA%B8%B0](https://shape-coding.tistory.com/entry/Git-Git-Add-%EC%B7%A8%EC%86%8C%ED%95%98%EA%B8%B0)"
  상태: 완료
schema_version: 1
parent_id: 1c3eda9b-0fe1-819d-89dc-fb5c624de379
created: 2025-03-27T07:47:52.780Z
updated: 2025-03-27T07:47:52.780Z
legacy_path: Main/Git-c9d937ee7825/Note- Git CLI-fb5c624de379/git add 취소 - git reset-e6cc08f5bdae/index.md
legacy_category: Git
source_url: https://beautiful-college-c84.notion.site/1c3eda9b0fe1817cbc82e6cc08f5bdae
---
- <code>reset</code> 명령어를 이용하여 전체 파일을 <code>unstaged</code> 상태로 되돌릴 수 있다

<a id="1c3eda9b0fe18166ac61e242f4e9813d"></a>

```bash
git reset
```

- <code>reset</code> 뒤에 파일명을 입력을 하면 개별로 취소 가능

<a id="1c3eda9b0fe1813d8ce8ffc57c0a0560"></a>

```bash
git reset HEAD [파일명]
```
