---
order: 17
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1c3eda9b-0fe1-81a7-bb1f-e11a5330a326
title: 삭제된 commit 내역 복구하기
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-81f9-b76e-c9d937ee7825
    title: Git
  - id: 1c3eda9b-0fe1-819d-89dc-fb5c624de379
    title: "Note: Git CLI"
  - id: 1c3eda9b-0fe1-81a7-bb1f-e11a5330a326
    title: 삭제된 commit 내역 복구하기
excerpt: "1. 작업 내용 복구 - git reflog 1. 최근 작업의 모든 기록을 확인 가능 bash git reflog 결과 예시 bash b1c2d3e (HEAD - main) HEAD@{0}: reset: moving to HEAD@{1} a1b2c3d HEAD@{1}: commit: Added feature X e4f5g"
cover: null
icon: null
notionProperties:
  point: git reflog
  상태: 완료
schema_version: 1
parent_id: 1c3eda9b-0fe1-819d-89dc-fb5c624de379
created: 2025-03-27T07:47:52.779Z
updated: 2025-03-27T07:47:52.779Z
legacy_path: Main/Git-c9d937ee7825/Note- Git CLI-fb5c624de379/삭제된 commit 내역 복구하기-e11a5330a326/index.md
legacy_category: Git
source_url: https://beautiful-college-c84.notion.site/1c3eda9b0fe181a7bb1fe11a5330a326
---
1. 작업 내용 복구 &#45; <code>git reflog</code>
    <a id="1c3eda9b0fe181c7b17ff33d0d40b037"></a>

    1&#46;  최근 작업의 모든 기록을 확인 가능

    <a id="1c3eda9b0fe181d39392e3906dfd9d43"></a>

    ```bash
    git reflog
    ```

    <details>
    <summary>결과 예시 </summary>

    <a id="1c3eda9b0fe1813eac82e6ced7ebf854"></a>

    ```bash
    b1c2d3e (HEAD -> main) HEAD@{0}: reset: moving to HEAD@{1}
    a1b2c3d HEAD@{1}: commit: Added feature X
    e4f5g6h HEAD@{2}: commit: Refactored module Y
    ```

    ![](2abafb30fe381e2c.webp)

    </details>

    1.  이전 상태로 복구 
        - 원하는 커밋 상태로 복구

        - reset이 아닌 checkout으로 작업 내역을 보존할 수 있다&#46;

        <a id="1c3eda9b0fe181a8ab19f7c654e1b487"></a>

        ```bash
        git checkout -b recover-branch a1b2c3d

        # a1b2c3d: 복구하려는 커밋 해시
        # 새로운 브랜치 recover-branch로 체크아웃하여 기존 작업 내용을 복원
        ```

    1. <strong>파일 복구 확인 </strong>
        - 복구된 브랜치에서 파일과 변경 사항이 복원되었는지 확인

        - 필요에 따라 작업을 추가적으로 수정

    1. <strong>다시 원래 브랜치로 병합 (선택 사항)</strong>
        - 복구한 브랜치의 내용을 원래 브랜치로 병합

        <a id="1c3eda9b0fe181bb9e11cdfd731bbbea"></a>

        ```bash
        git checkout [ 병할할 브런치 ]
        git merge recover-branch # 복구를 위해 임시 생성한 브랜치 
        ```



<a id="1c3eda9b0fe181aba599c609fa55b527"></a>

Tip)  <strong>git stash로 작업 보존 습관화</strong>

- reset 명령 전에 작업 내용을 안전하게 보존하려면 항상 stash를 활용
    <a id="1c3eda9b0fe1818da3cadedd166680bc"></a>

    ```bash
    git stash

    git stash pop
    ```
