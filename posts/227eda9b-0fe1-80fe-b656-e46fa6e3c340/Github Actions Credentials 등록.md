---
order: 1
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 227eda9b-0fe1-80fe-b656-e46fa6e3c340
title: Github Actions Credentials 등록
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-817b-9c95-d96fd53640c4
    title: CI/CD
  - id: 227eda9b-0fe1-80d6-bacc-e93ff1df19a3
    title: 비전공자도 이해할 수 있는 CI/CD 입문·실전
  - id: 227eda9b-0fe1-80fe-b656-e46fa6e3c340
    title: Github Actions Credentials 등록
excerpt: "Github에 Secret값 설정 --- ⚠️ environment를 설정하는 경우, workflows 내에서 해당하는 scope 설정을 추가 해야한다. ex) yaml name: Deploy To EC2 on: push: branches: - main jobs: deploy: runs-on: ubuntu-latest e"
cover: null
icon: null
notionProperties: {}
schema_version: 1
parent_id: 227eda9b-0fe1-80d6-bacc-e93ff1df19a3
created: 2025-07-05T04:16:01.817Z
updated: 2025-07-05T04:52:03.681Z
legacy_path: Main/CI-CD-d96fd53640c4/비전공자도 이해할 수 있는 CI-CD 입문·실전-e93ff1df19a3/Github Actions Credentials 등록-e46fa6e3c340/index.md
legacy_category: CI/CD
source_url: https://beautiful-college-c84.notion.site/227eda9b0fe180feb656e46fa6e3c340
---
<a id="227eda9b0fe180a4a26fca829b8dd734"></a>

##  Github에 Secret값 설정

---

> ⚠️ 
> 
> <a id="227eda9b0fe1807c8659d51eda4ce412"></a>
> 
> environment를 설정하는 경우, workflows 내에서 해당하는 scope 설정을 추가 해야한다&#46;
> 
> <details>
> <summary>ex)</summary>
> 
> <a id="227eda9b0fe1800592ebda6b24195b3e"></a>
> 
> ```yaml
> name: Deploy To EC2
> 
> on:
>   push:
>     branches:
>       - main
> 
> jobs:
>   deploy:
>     runs-on: ubuntu-latest
>     environment: test
> 		steps:
> 		
> 				. . .
> ```
> 
> </details>

- 해당하는 github 프로젝트 &#45; Settings &#45; Secret and variables &#45; Actions &#45; <code>New repository secret</code> 클릭
    ![](9bff7c942846c433.webp)

- workflows에 필요한 secrets 값들 생성
    ![](98c302194b660a76.webp)
