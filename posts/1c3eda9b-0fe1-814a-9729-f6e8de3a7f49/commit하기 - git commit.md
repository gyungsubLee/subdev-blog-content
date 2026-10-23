---
order: 3
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1c3eda9b-0fe1-814a-9729-f6e8de3a7f49
title: commit하기 - git commit
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-81f9-b76e-c9d937ee7825
    title: Git
  - id: 1c3eda9b-0fe1-819d-89dc-fb5c624de379
    title: "Note: Git CLI"
  - id: 1c3eda9b-0fe1-814a-9729-f6e8de3a7f49
    title: commit하기 - git commit
excerpt: "vim 명령어 ➕ 페이지 | | | | | --- | --- | --- | | 작업 | Vi 명령어 | 상세 | | 입력 시작 | i | 명령어 입력 모드에서 텍스트 입력 모드로 전환 | | 입력 종료 | ESC | 텍스트 입력 모드에서 명령어 입력 모드로 전환 | | 저장 없이 종료 | :q | | | 저장 없이 강제 "
cover: null
icon: null
notionProperties:
  상태: 완료
schema_version: 1
parent_id: 1c3eda9b-0fe1-819d-89dc-fb5c624de379
created: 2025-03-27T07:47:52.782Z
updated: 2025-03-27T07:47:52.782Z
legacy_path: Main/Git-c9d937ee7825/Note- Git CLI-fb5c624de379/commit하기 - git commit-f6e8de3a7f49/index.md
legacy_category: Git
source_url: https://beautiful-college-c84.notion.site/1c3eda9b0fe1814a9729f6e8de3a7f49
---
<a id="1c3eda9b0fe181649a97f9bf31167f02"></a>

### vim 명령어

> ➕ <a href="https://beautiful-college-c84.notion.site/b2c01c46437d4b4389373f2f94c379a3">페이지</a> 

|  |  |  |
| --- | --- | --- |
| <strong>작업</strong> | <strong>Vi 명령어</strong> | <strong>상세</strong> |
| 입력 시작 | <strong>i</strong> | 명령어 입력 모드에서 텍스트 입력 모드로 전환 |
| 입력 종료 | <code>ESC</code> | 텍스트 입력 모드에서 명령어 입력 모드로 전환 |
| 저장 없이 종료 | <strong>&#58;q</strong> |  |
| 저장 없이 강제 종료 | <strong>&#58;q&#33;</strong> | 입력한 것이 있을 때 사용 |
| 저장하고 종료 | <strong>&#58;wq</strong> | 입력한 것이 있을 때 사용 |
| 위로 스크롤 | <strong>k</strong> | <code>git log</code>등에서 내역이 길 때 사용 |
| 아래로 스크롤 | <strong>j</strong> | <code>git log</code>등에서 내역이 길 때 사용 |

- 커밋

<a id="1c3eda9b0fe1817c9d9addd7fb62d2b1"></a>

```bash
git commit
```

- 커밋 메세지까지 함께 작성

<a id="1c3eda9b0fe181f5bef2f944cf42b565"></a>

```bash
git commit -m "MESSAGE" (' ', " ")
```

- commit들 확인
    <a id="1c3eda9b0fe181ceacced38290b9c7bb"></a>

    ```bash
    git log
    ```

    - 소스트리 확인
        ![](5780c3042a44ad25.webp)

- TIP) <code>add</code> 와 <code>commit</code> 한꺼번에 하기
    > &#45;a&#58; add   &#91; 새로 추가된(untracked) 파일이 없을 때만 가능 &#93;

    <a id="1c3eda9b0fe18152a760dc485b2ae9aa"></a>

    ```bash
    git commit -am "(메세지)" 
    ```
