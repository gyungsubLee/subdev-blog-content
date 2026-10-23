---
order: 5
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1c3eda9b-0fe1-8142-849b-c38dbd275657
title: 임시저장소 - git stash
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-81f9-b76e-c9d937ee7825
    title: Git
  - id: 1c3eda9b-0fe1-819d-89dc-fb5c624de379
    title: "Note: Git CLI"
  - id: 1c3eda9b-0fe1-8142-849b-c38dbd275657
    title: 임시저장소 - git stash
excerpt: "1. 작업 내역 저장하기 bash git stash 2. 저장 내역 확인하기 bash git stash list 3-1. 저장한 작업 내역 꺼내오기 pop 시, 저장한 작업 리스트 내역은 삭제된다. bash git stash pop 3-2. 저장한 작업 내역 불러오기 작없을 리스트에서 삭제없이 불러온다. bash git "
cover: null
icon: null
notionProperties:
  Reference: "[https://megaton111.cafe24.com/2018/04/12/git-stash/](https://megaton111.cafe24.com/2018/04/12/git-stash/)"
  상태: 완료
schema_version: 1
parent_id: 1c3eda9b-0fe1-819d-89dc-fb5c624de379
created: 2025-03-27T07:47:52.781Z
updated: 2025-03-27T07:47:52.781Z
legacy_path: Main/Git-c9d937ee7825/Note- Git CLI-fb5c624de379/임시저장소 - git stash-c38dbd275657/index.md
legacy_category: Git
source_url: https://beautiful-college-c84.notion.site/1c3eda9b0fe18142849bc38dbd275657
---
<a id="1c3eda9b0fe1814ba5f0f6bb72150f1b"></a>

### 1&#46; 작업 내역 저장하기 

<a id="1c3eda9b0fe181ac8e18e6fae74ccce7"></a>

```bash
git stash
```

<a id="1c3eda9b0fe18177a82cd5aa6b9bb386"></a>

### 2&#46; 저장 내역 확인하기

<a id="1c3eda9b0fe181409d56ecf610e3e080"></a>

```bash
git stash list
```

<a id="1c3eda9b0fe181249ec6cc28aab97643"></a>

### 3&#45;1&#46; 저장한 작업 내역 꺼내오기 

<a id="1c3eda9b0fe181f89e73c3b66e6f5687"></a>

pop 시, 저장한 작업 리스트 내역은 삭제된다&#46; 

<a id="1c3eda9b0fe181419e38c115e4db3d0a"></a>

```bash
git stash pop
```

<a id="1c3eda9b0fe181228390cc461b42c940"></a>

### 3&#45;2&#46; 저장한 작업 내역 불러오기 

<a id="1c3eda9b0fe181b3a7c1f8abf908c6b9"></a>

작없을 리스트에서  삭제없이 불러온다&#46; 

<a id="1c3eda9b0fe1818f82d8db92015e62e1"></a>

```bash
git stash apply
```

<a id="1c3eda9b0fe1817ea38bc71aa6c9dd81"></a>

### 4&#45;1&#46; 가장 최근에 저장한 작업 삭제하기

<a id="1c3eda9b0fe181ccb7a8ca90651b7d00"></a>

가장 최근에 저장한 내역을 삭제한다&#46; 

<a id="1c3eda9b0fe1814a92cac5eb58011a54"></a>

```bash
git stash drop
```

<a id="1c3eda9b0fe18183ae17c2b1bd2529be"></a>

### 4&#45;2&#46; 특정 작업 내역 삭제하기 

<a id="1c3eda9b0fe1816482a8c8d57a0054b0"></a>

stash&#64;{0} 내역을 삭제한다&#46;

<a id="1c3eda9b0fe181be944ae55abe07c944"></a>

```bash
1
git stash drop stash@{0}
```

<a id="1c3eda9b0fe181d1ab2edc3e45555466"></a>

### 5&#46; 저장한 전체 작업 내역 삭제하기 

<a id="1c3eda9b0fe18185a610e575d1353de7"></a>

```bash
git stash clear
```
