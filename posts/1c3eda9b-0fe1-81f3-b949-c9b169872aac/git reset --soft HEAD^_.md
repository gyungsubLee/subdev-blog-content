---
order: 7
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1c3eda9b-0fe1-81f3-b949-c9b169872aac
title: "git reset --soft HEAD^:"
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-81f9-b76e-c9d937ee7825
    title: Git
  - id: 1c3eda9b-0fe1-819d-89dc-fb5c624de379
    title: "Note: Git CLI"
  - id: 1c3eda9b-0fe1-81f3-b949-c9b169872aac
    title: "git reset --soft HEAD^:"
excerpt: "현재 HEAD가 가리키는 커밋 이전의 상태로 되돌리며, 커밋한 작업 내역을 staged 상태로 불러온다. bash git reset --soft HEAD^ git reset은 세 가지 옵션 - soft : HEAD가 가리키는 브랜치를 옮긴다. (변경사항은 유지, staged 상태로 만듦) - mixed(default) :"
cover: null
icon: null
notionProperties:
  point: 최근 커밋 삭제 및 작업 내역 유지하기
  Reference: "[https://jwkim96.tistory.com/184](https://jwkim96.tistory.com/184)"
  상태: 완료
schema_version: 1
parent_id: 1c3eda9b-0fe1-819d-89dc-fb5c624de379
created: 2025-03-27T07:47:52.781Z
updated: 2025-03-27T07:47:52.781Z
legacy_path: Main/Git-c9d937ee7825/Note- Git CLI-fb5c624de379/git reset --soft HEAD^--c9b169872aac/index.md
legacy_category: Git
source_url: https://beautiful-college-c84.notion.site/1c3eda9b0fe181f3b949c9b169872aac
---
<a id="1c3eda9b0fe181519db2eb098c1fb151"></a>

현재 HEAD가 가리키는 커밋 이전의 상태로 되돌리며, 커밋한 작업 내역을 staged 상태로 불러온다&#46; 

<a id="1c3eda9b0fe1813095c9efc5ebc1ff70"></a>

```bash
git reset --soft HEAD^
```

<a id="1c3eda9b0fe181b8b7a6ff41f2b9e78e"></a>

### git reset은 세 가지 옵션

- soft &#58; HEAD가 가리키는 브랜치를 옮긴다&#46; (변경사항은 유지, staged 상태로 만듦)

- mixed(default) &#58; Index를 HEAD가 가리키는 상태로 만든다&#46; (변경사항은 유지, unstaged 상태로 만듦)

- hard &#58; 워킹 디렉토리를 Index의 상태로 만든다&#46;(변경사항 없어짐)
