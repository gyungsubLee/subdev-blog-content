---
order: 3
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 224eda9b-0fe1-8019-b6b9-d7b7030e83a1
title: Case 0. 수동 베포 과정
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-817b-9c95-d96fd53640c4
    title: CI/CD
  - id: 227eda9b-0fe1-80d6-bacc-e93ff1df19a3
    title: 비전공자도 이해할 수 있는 CI/CD 입문·실전
  - id: 224eda9b-0fe1-8019-b6b9-d7b7030e83a1
    title: Case 0. 수동 베포 과정
excerpt: 목차 - 수동 베포 - 1. 수동 베포 - 2. 매번 Github 계정과 비밀번호를 치는 과정 없애기 수동 베포 --- 1. 수동 베포 1. 새로 코드 업데이트 및 commit, origin에 push 1. EC2에서 github 프로젝트 pull bash cd {프로젝트 경로} git pull origin main 1.
cover: null
icon: null
notionProperties: {}
schema_version: 1
parent_id: 227eda9b-0fe1-80d6-bacc-e93ff1df19a3
created: 2025-07-02T08:22:22.936Z
updated: 2025-07-05T04:47:01.465Z
legacy_path: Main/CI-CD-d96fd53640c4/비전공자도 이해할 수 있는 CI-CD 입문·실전-e93ff1df19a3/Case 0. 수동 베포 과정-d7b7030e83a1/index.md
legacy_category: CI/CD
source_url: https://beautiful-college-c84.notion.site/224eda9b0fe18019b6b9d7b7030e83a1
---
> 
> 
> <a id="227eda9b0fe18015882dfdf55bda64d2"></a>
> 
> <strong>목차</strong>
> 
> - [수동 베포 ](#222eda9b0fe180deaff8df2221b2b9e9)
> - [1. 수동 베포](#222eda9b0fe180b594baefb0f4cec3a7)
> - [2. 매번 Github 계정과 비밀번호를 치는 과정 없애기](#222eda9b0fe180f8b7cae0a10da8d1e6)

<a id="222eda9b0fe180deaff8df2221b2b9e9"></a>

## 수동 베포 

---

<a id="222eda9b0fe180b594baefb0f4cec3a7"></a>

### 1&#46; 수동 베포

1. 새로 코드 업데이트 및 commit, origin에 push

1. EC2에서 github 프로젝트 pull
    <a id="222eda9b0fe1809390bfd517a24eb88e"></a>

    ```bash
    cd {프로젝트 경로}
    git pull origin main
    ```

1. 빌드 후 재배포
    <a id="222eda9b0fe1805eab31c4d8f5e909e4"></a>

    ```bash
    npm i
    npm run build
    pm2 kill
    pm2 start dist/main.js --name "backend-server"
    ```

<a id="222eda9b0fe180f8b7cae0a10da8d1e6"></a>

### 2&#46; 매번 Github 계정과 비밀번호를 치는 과정 없애기

- <a href="#/post/227eda9b-0fe1-80fd-8121-daa9b43f7e2b">페이지</a>
