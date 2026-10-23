---
order: 0
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1e1eda9b-0fe1-80f5-a5b4-db99cfdb9514
title: "과거 커밋한 git 제목 수정: rebase ( reword )"
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-81f9-b76e-c9d937ee7825
    title: Git
  - id: 1c3eda9b-0fe1-819d-89dc-fb5c624de379
    title: "Note: Git CLI"
  - id: 1e1eda9b-0fe1-80f5-a5b4-db99cfdb9514
    title: "과거 커밋한 git 제목 수정: rebase ( reword )"
excerpt: "방법 1: rebase bash git rebase -i HEAD~N - N: 최근 몇 개 커밋까지 보고 싶은지를 정하는 숫자 - ex) HEAD~3: 최근 3개 커밋 보여줌 bash git rebase -i HEAD~3 커밋 리스트 pick 1a2b3c4 Original commit message 1 pick 5d6e7"
cover: null
icon: null
notionProperties:
  상태: 완료
schema_version: 1
parent_id: 1c3eda9b-0fe1-819d-89dc-fb5c624de379
created: 2025-04-26T10:42:50.897Z
updated: 2025-04-26T10:50:41.278Z
legacy_path: Main/Git-c9d937ee7825/Note- Git CLI-fb5c624de379/과거 커밋한 git 제목 수정- rebase ( reword )-db99cfdb9514/index.md
legacy_category: Git
source_url: https://beautiful-college-c84.notion.site/1e1eda9b0fe180f5a5b4db99cfdb9514
---
<a id="1e1eda9b0fe180dcb2d5ca5b00e5786c"></a>

### 방법 1&#58; <code>rebase</code>

<a id="1e1eda9b0fe180c68054fcd1552f0b7b"></a>

```bash
git rebase -i HEAD~N
```

- <strong><code>N</code></strong><strong>&#58; 최근 몇 개 커밋까지 보고 싶은지를 정하는 숫자</strong>

- <strong>ex) </strong><strong><code>HEAD&#126;3</code></strong><strong>&#58; 최근 3개 커밋 보여줌</strong>

<a id="1e1eda9b0fe180659991d4cd8aa7b532"></a>

```bash
git rebase -i HEAD~3

# 커밋 리스트
pick 1a2b3c4 Original commit message 1
pick 5d6e7f8 Original commit message 2
pick 9a0b1c2 Original commit message 3

# 수정하고 싶은 커밋 줄의 pick을 reword로 변경
pick 1a2b3c4 Original commit message 1
reword 5d6e7f8 Original commit message 2   <-- 수정하고 싶은 커밋
pick 9a0b1c2 Original commit message 3
```

<a id="1e1eda9b0fe180a1a33bdc3eaf368218"></a>

수정할 커밋을 <strong>reword</strong>로 변경 후 저장하면 해당하는 커밋을 바로 수정 가능하다&#46;

![](0ed3c60377a38fee.webp)

- 저장&#58; <code>ctrl</code> &#43; <code>o</code> → 종료&#58; <code>ctrl</code> &#43; <code>x</code> 

![](a6a5818a760bef29.webp)

- 위와 같이 reword로 변경한 커밋이 에디터로 바로 뜨는 것을 확인 할 수 있다&#46;
