---
order: 16
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1c3eda9b-0fe1-8101-9441-e3a37be64d3e
title: git 이미 커밋된 파일 추적되지 않도록 하기
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-81f9-b76e-c9d937ee7825
    title: Git
  - id: 1c3eda9b-0fe1-819d-89dc-fb5c624de379
    title: "Note: Git CLI"
  - id: 1c3eda9b-0fe1-8101-9441-e3a37be64d3e
    title: git 이미 커밋된 파일 추적되지 않도록 하기
excerpt: "- 이미 커밋된 파일을 추적에서 제외 (하지만 로컬에 유지) bash git rm --cached 제거 후, 제거된 내용을 commit 제거된 파일 .gitignore 에 등록 시 해당 파일은 더이상 git에 추적되지 않음 ex) bash git rm --cached config.json 제거된 내역을 commit 이후 "
cover: null
icon: null
notionProperties:
  point: "git rm —cached "
  상태: 완료
schema_version: 1
parent_id: 1c3eda9b-0fe1-819d-89dc-fb5c624de379
created: 2025-03-27T07:47:52.780Z
updated: 2025-03-27T07:47:52.780Z
legacy_path: Main/Git-c9d937ee7825/Note- Git CLI-fb5c624de379/git 이미 커밋된 파일 추적되지 않도록 하기-e3a37be64d3e/index.md
legacy_category: Git
source_url: https://beautiful-college-c84.notion.site/1c3eda9b0fe181019441e3a37be64d3e
---
- <strong>이미 커밋된 파일을 추적에서 제외 (하지만 로컬에 유지)</strong>
    <a id="1c3eda9b0fe181aab26bd53acb5ba393"></a>

    ```bash
    git rm --cached <파일명>

    # 제거 후, 제거된 내용을 commit
    # 제거된 파일 .gitignore 에 등록 시 해당 파일은 더이상 git에 추적되지 않음
    ```

    <details>
    <summary>ex)</summary>

    <a id="1c3eda9b0fe181669b3cd22262aaf4a1"></a>

    ```bash
    git rm --cached config.json

    # 제거된 내역을 commit 
    # 이후 .gitignore에 해당 파일을 추가하면 더이상 git에서 추적하지 않음
    ```

    </details>

- <strong>파일을 완전히 삭제하고 추적도 제거</strong>
    <a id="1c3eda9b0fe18108af36e0c304957ce9"></a>

    ```bash
    git rm <파일명>
    ```
