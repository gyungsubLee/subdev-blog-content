---
order: 8
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1c3eda9b-0fe1-816a-96cc-c0a4a0ff46a8
title: commit 되돌리기 - git reset
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-81f9-b76e-c9d937ee7825
    title: Git
  - id: 1c3eda9b-0fe1-819d-89dc-fb5c624de379
    title: "Note: Git CLI"
  - id: 1c3eda9b-0fe1-816a-96cc-c0a4a0ff46a8
    title: commit 되돌리기 - git reset
excerpt: "페이지 ⚠️ reset을 협업에서 사용하는 경우 다른 사람들의 history와 충돌이 발생되어 심각한 오류가 발생된다. 따라서 한번 공유가 된 코드는 revert를 사용하야 되돌려야 한다. 돌아가고자 하는 이전 commit으로 돌아가 해당 commit 이후 내용들은 history에서 지워진다. —hard: 강제 실행 <h"
cover: null
icon: null
notionProperties:
  상태: 완료
schema_version: 1
parent_id: 1c3eda9b-0fe1-819d-89dc-fb5c624de379
created: 2025-03-27T07:47:52.781Z
updated: 2025-03-27T07:47:52.781Z
legacy_path: Main/Git-c9d937ee7825/Note- Git CLI-fb5c624de379/commit 되돌리기 - git reset-c0a4a0ff46a8/index.md
legacy_category: Git
source_url: https://beautiful-college-c84.notion.site/1c3eda9b0fe1816a96ccc0a4a0ff46a8
---
<a id="1c3eda9b0fe1818788ecc95ff570410f"></a>

<a href="#/post/1c3eda9b-0fe1-8136-9ee1-e1f7b953e3c0">페이지</a>

> ⚠️ <strong>reset</strong>을 협업에서 사용하는 경우 다른 사람들의 history와 충돌이 발생되어 심각한 오류가 발생된다&#46;  따라서 <strong>한번 공유가 된 코드는  </strong><strong><code>revert</code></strong><strong>를 사용하야 되돌려야 한다&#46;</strong>
> 
> ![](54c8569cb7d374c0.webp)

<a id="1c3eda9b0fe1810dab9af02a71ac8d4b"></a>

돌아가고자 하는 <strong>이전 commit으로 돌아가</strong>  <strong><u>해당 commit 이후 내용들은 history에서 지워진다&#46; </u></strong>

![](b028346f9b0c4c1b.webp)

> <code>—hard</code>&#58; 강제 실행<br><code>&#60;hash&#62;</code>&#58; git log 로 확인

<a id="1c3eda9b0fe181e3805cd7b7ba764c15"></a>

```bash
git reset --hard  <hash>
```

- git log 확인 
    ![](3a716e7baa40558b.webp)
