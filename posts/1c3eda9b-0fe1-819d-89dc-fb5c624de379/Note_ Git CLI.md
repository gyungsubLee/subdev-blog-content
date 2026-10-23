---
order: 2
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1c3eda9b-0fe1-819d-89dc-fb5c624de379
title: "Note: Git CLI"
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-81f9-b76e-c9d937ee7825
    title: Git
  - id: 1c3eda9b-0fe1-819d-89dc-fb5c624de379
    title: "Note: Git CLI"
excerpt: .gitignore - application.properties 등록 시 .gitignore 등록이 안될 시 방법 git 최초 설정 git 제외 - .gitignore 임시저장소 - git stash 파일 상태 확인 - git status commit 확인 - git log git add 취소 - git reset com
cover: null
icon: ✏️
notionProperties: {}
schema_version: 1
parent_id: 1c3eda9b-0fe1-81f9-b76e-c9d937ee7825
created: 2025-03-27T07:47:12.308Z
updated: 2025-03-27T07:47:12.308Z
legacy_path: Main/Git-c9d937ee7825/Note- Git CLI-fb5c624de379/index.md
legacy_category: Git
source_url: https://beautiful-college-c84.notion.site/1c3eda9b0fe1819d89dcfb5c624de379
---
[.gitignore  - application.properties 등록 시](#/post/1c3eda9b-0fe1-8101-9d46-cb4561ece0f4)

[.gitignore 등록이 안될 시 방법](#/post/1c3eda9b-0fe1-817d-90a4-c33af19efbd2)

[git 최초 설정](#/post/1c3eda9b-0fe1-81eb-819c-c3c6127fc5f0)

[git 제외 - .gitignore](#/post/1c3eda9b-0fe1-812b-9c87-e58b2234814a)

[임시저장소 - git stash](#/post/1c3eda9b-0fe1-8142-849b-c38dbd275657)

[파일 상태 확인 - git status](#/post/1c3eda9b-0fe1-81db-b05a-c2afad5ca59f)

[commit 확인 - git log](#/post/1c3eda9b-0fe1-8159-91f4-decb4239635f)

[git add 취소 - git reset](#/post/1c3eda9b-0fe1-817c-bc82-e6cc08f5bdae)

[commit하기 - git commit](#/post/1c3eda9b-0fe1-814a-9729-f6e8de3a7f49)

[git reset --soft HEAD^:](#/post/1c3eda9b-0fe1-81f3-b949-c9b169872aac)

[commit 되돌리기 - git reset](#/post/1c3eda9b-0fe1-816a-96cc-c0a4a0ff46a8)

[commit 되돌리기 - git revert](#/post/1c3eda9b-0fe1-81e1-82bc-eb3287d99cae)

[브랜치  CLI 모음](#/post/1c3eda9b-0fe1-81e3-8040-e98086515d90)

[이전 브랜치로 돌아감 - git checkout -](#/post/1c3eda9b-0fe1-81af-a1e7-e5f374910495)

[브랜치 전략](#/post/1c3eda9b-0fe1-81a0-9bc1-fcff55e426af)

[git 특정 commit 까지만 push 하기](#/post/1c3eda9b-0fe1-817e-b853-f631ad034683)

[삭제된 commit 내역 복구하기](#/post/1c3eda9b-0fe1-81a7-bb1f-e11a5330a326)

[git 특정 명령어 별칭 지정하기](#/post/1c3eda9b-0fe1-8157-ad04-f43cfbef2887)

[원격 저장소 브랜치 삭제 방법](#/post/1c3eda9b-0fe1-81ca-9d1d-f38783de7b15)

[github 환경변수 설정](#/post/1c3eda9b-0fe1-817a-a7c5-d6f72f5db7af)

[github 계정 연동을 위한 토큰 생성](#/post/1c3eda9b-0fe1-815d-b376-f17c48552655)

[로컬 브랜치에 원격 메인 브랜치 최신 작업내역 가져오는 방법](#/post/1c3eda9b-0fe1-8153-868e-c3a2da0f1e04)

[git add + commit , alias 설정, + push](#/post/1c3eda9b-0fe1-8175-a89e-d9cdd18ece7d)

[git message template - local 설정](#/post/1c3eda9b-0fe1-81e0-85d3-ed61eb5b8c62)

[intellij에서 git branch 별로 비교하는 방법](#/post/1c3eda9b-0fe1-8101-808c-fc851a219958)

[git 특정 커밋으로 돌아갔다가 되돌아오기](#/post/1c3eda9b-0fe1-814b-ab64-f26466afed35)

[실수로 커밋한 .gitignore  내역 삭제하기](#/post/1c3eda9b-0fe1-817e-8162-c555b872e383)

[git 이미 커밋된 파일 추적되지 않도록 하기](#/post/1c3eda9b-0fe1-8101-9441-e3a37be64d3e)

[과거 커밋한 git 제목 수정: rebase ( reword )](#/post/1e1eda9b-0fe1-80f5-a5b4-db99cfdb9514)
