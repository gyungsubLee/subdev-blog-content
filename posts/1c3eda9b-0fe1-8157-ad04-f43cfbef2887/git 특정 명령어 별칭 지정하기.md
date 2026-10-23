---
order: 28
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1c3eda9b-0fe1-8157-ad04-f43cfbef2887
title: git 특정 명령어 별칭 지정하기
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-81f9-b76e-c9d937ee7825
    title: Git
  - id: 1c3eda9b-0fe1-819d-89dc-fb5c624de379
    title: "Note: Git CLI"
  - id: 1c3eda9b-0fe1-8157-ad04-f43cfbef2887
    title: git 특정 명령어 별칭 지정하기
excerpt: "별칭(alias) 설정으로 사용자 정의 단축키 만들기 --- 더 짧은 명령어나 익숙한 이름을 원하면 Git 별칭을 설정할 수 있다. 별칭 설정 방법 - Git 별칭 - git config 명령으로 설정 bash git config --global alias.[설정할 별칭] [기존 명령어] case 1 ) switch - "
cover: null
icon: null
notionProperties:
  상태: 완료
schema_version: 1
parent_id: 1c3eda9b-0fe1-819d-89dc-fb5c624de379
created: 2025-03-27T07:47:52.778Z
updated: 2025-03-27T07:47:52.778Z
legacy_path: Main/Git-c9d937ee7825/Note- Git CLI-fb5c624de379/git 특정 명령어 별칭 지정하기-f43cfbef2887/index.md
legacy_category: Git
source_url: https://beautiful-college-c84.notion.site/1c3eda9b0fe18157ad04f43cfbef2887
---
<a id="1c3eda9b0fe181f8beb4ca14ffc3ccd4"></a>

## <strong> 별칭(alias) 설정으로 사용자 정의 단축키 만들기</strong>

---

<a id="1c3eda9b0fe1811aa59fc52c76daf128"></a>

더 짧은 명령어나 익숙한 이름을 원하면 Git 별칭을 설정할 수 있다&#46;

<a id="1c3eda9b0fe1819aa64ec1596404192f"></a>

### <strong>별칭 설정 방법</strong>

- Git 별칭 &#45; git config 명령으로 설정
    <a id="1c3eda9b0fe1818fb3cfd3177a14d31e"></a>

    ```bash
    git config --global alias.[설정할 별칭] [기존 명령어]
    ```

    <details>
    <summary>case 1 ) <code>switch &#45;</code> → <code>prev</code></summary>

    <a id="1c3eda9b0fe181a28beec05c256f2cfb"></a>

    ```bash
    git config --global alias.prev 'switch -'
    ```

    - git prev 명령으로 이전 브랜치로 전환(<code>switch &#45;</code>) 가능
        <a id="1c3eda9b0fe181f0900ac226ea74a909"></a>

        ```bash
        git prev
        ```

    </details>
