---
order: 25
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1c3eda9b-0fe1-812b-9c87-e58b2234814a
title: git 제외 - .gitignore
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-81f9-b76e-c9d937ee7825
    title: Git
  - id: 1c3eda9b-0fe1-819d-89dc-fb5c624de379
    title: "Note: Git CLI"
  - id: 1c3eda9b-0fe1-812b-9c87-e58b2234814a
    title: git 제외 - .gitignore
excerpt: "Git 관리에서 특정 파일/폴더를 제외해야 하는 경우 ( .gitignore) Reference https://git-scm.com/docs/gitignore https://www.yalco.kr/@git-github/1-6/ 📌 Case - 포함할 필요가 없는 경우: 자동 생성, 다운로드 되는 파일들(빌드 결과물, 라"
cover: null
icon: null
notionProperties:
  상태: 완료
schema_version: 1
parent_id: 1c3eda9b-0fe1-819d-89dc-fb5c624de379
created: 2025-03-27T07:47:52.778Z
updated: 2025-03-27T07:47:52.778Z
legacy_path: Main/Git-c9d937ee7825/Note- Git CLI-fb5c624de379/git 제외 - .gitignore-e58b2234814a/index.md
legacy_category: Git
source_url: https://beautiful-college-c84.notion.site/1c3eda9b0fe1812b9c87e58b2234814a
---
<a id="1c3eda9b0fe181ba8ea0f6bfbd357a2a"></a>

### Git 관리에서 특정 파일/폴더를 제외해야 하는 경우 ( <code>&#46;gitignore</code>)

<details>
<summary><strong>Reference</strong></summary>

<a id="1c3eda9b0fe18132abaaf902f25d3b54"></a>

<a href="https://git-scm.com/docs/gitignore">https&#58;//git&#45;scm&#46;com/docs/gitignore</a>

<a id="1c3eda9b0fe18120906ef2c48124ac75"></a>

<a href="https://www.yalco.kr/@git-github/1-6/">https&#58;//www&#46;yalco&#46;kr/&#64;git&#45;github/1&#45;6/</a>

</details>

> 📌 <strong>Case</strong>
> 
> - <strong>포함할 필요가 없는 경우</strong>&#58;  자동 생성, 다운로드 되는 파일들(빌드 결과물, 라이브러리)
> 
> - <strong>포함하지 말하야 하는 경우</strong>&#58; 보안상 민간한 정보들이 담긴 파일들

- <strong><code>&#46;gitignore</code></strong><strong> 형식</strong>
    <a id="1c3eda9b0fe1811193c4e3392f942569"></a>

    ```bash
    # 이렇게 #를 사용해서 주석

    # 모든 file.c
    file.c

    # 최상위 폴더의 file.c
    /file.c

    # 모든 .c 확장자 파일
    *.c

    # .c 확장자지만 무시하지 않을 파일
    !not_ignore_this.c

    # logs란 이름의 파일 또는 폴더와 그 내용들
    logs

    # logs란 이름의 폴더와 그 내용들
    logs/

    # logs 폴더 바로 안의 debug.log와 .c 파일들
    logs/debug.log
    logs/*.c

    # logs 폴더 바로 안, 또는 그 안의 다른 폴더(들) 안의 debug.log
    logs/**/debug.log
    ```
