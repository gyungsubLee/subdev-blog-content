---
order: 52
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 229eda9b-0fe1-8055-9084-d4caa4cd4466
title: MongoDB 클라우드 구축
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 226eda9b-0fe1-802b-a035-c3a886768c4d
    title: Nest.js
  - id: 227eda9b-0fe1-80e1-8036-d4fc3e106054
    title: 탄탄한 백엔드 NestJS, 기초부터 심화까지 ( 중지 )
  - id: 229eda9b-0fe1-8055-9084-d4caa4cd4466
    title: MongoDB 클라우드 구축
excerpt: "목차 - 1. Clusters 생성 - 2. Network Access 허용 - 3. Database Access 허용 - 4. DB 연결 [MongoDB Atlas: Cloud Document Database]() 1. Clusters 생성 ✏️ 처음 회원가입 시, Free 요금제 사용 가능하다. ( 이후 안됨 ) - "
cover: null
icon: null
notionProperties: {}
schema_version: 1
parent_id: 227eda9b-0fe1-80e1-8036-d4fc3e106054
created: 2025-07-07T11:35:43.360Z
updated: 2025-07-09T09:03:28.866Z
legacy_path: Main/Nest.js-c3a886768c4d/탄탄한 백엔드 NestJS, 기초부터 심화까지 ( 중지 )-d4fc3e106054/MongoDB 클라우드 구축-d4caa4cd4466/index.md
legacy_category: Nest.js
source_url: https://beautiful-college-c84.notion.site/229eda9b0fe180559084d4caa4cd4466
---
> 
> 
> <a id="229eda9b0fe18094a0f6c0d607bbe033"></a>
> 
> <strong>목차</strong>
> 
> - [1. Clusters 생성](#229eda9b0fe180bc91dfd21e04dca606)
> - [2. Network Access 허용](#229eda9b0fe180b3958bdb570dd39ac3)
> - [3. Database Access 허용](#229eda9b0fe180918e4cc85b025b6d8e)
> - [4. DB 연결](#229eda9b0fe180688d32dabdd5cd4588)

[MongoDB Atlas&#58; Cloud Document Database]()

<a id="229eda9b0fe180bc91dfd21e04dca606"></a>

### 1&#46; Clusters 생성

> ✏️ 
> 
> <a id="229eda9b0fe180aea3f4ed5386beaf8d"></a>
> 
> 처음 회원가입 시, Free 요금제 사용 가능하다&#46; ( 이후 안됨 )

- 옵션 선택 후 클러스터 생성 &#45; AWS로 진행
    ![](95a1fd1fe572cf4e.webp)

- 생성 확인
    ![](8b644168049cd8b5.webp)

<a id="229eda9b0fe180b3958bdb570dd39ac3"></a>

### 2&#46; Network Access 허용

> 
> 
> <a id="229eda9b0fe1802fac60e284928b1767"></a>
> 
> mongoDB에 접근 가능하도록 인바운드 규칙(<code>IP 주소</code>)을 추가한다&#46; 
> 
> - 실습&#58; 로컬 컴퓨터 IP 주소
> 
> - 베포&#58; 베포 서버 IP 주소

![](afb6543cea5c11b3.webp)

![](ee9de23956b8e61c.webp)

![](0b98fc5b5ca322c4.webp)

<a id="229eda9b0fe180918e4cc85b025b6d8e"></a>

### 3&#46; Database Access 허용

- 왼쪽 메뉴 &#45; Database Access &#45; Add new Database User
    ![](d444ef99076882ef.webp)

- Database 유저 생성
    > 
    > 
    > - Authentication Method&#58;  <code>Password</code>
    > 
    > - username&#58; 입력 필요
    > 
    > - password&#58; 자동 생성
    >     - 처음 생성 시에만 확인 가능, 따라서 보관 필요
    > 
    > - Built&#45;in Role&#58; <code>Read and Write to any database</code>
    >     - 상황에 따라 보안 scope 설정
    > 
    > - Temporary User&#58; 인증 정보 유효기간 설정

    ![](e0503145c70aed0d.webp)

    ![](2565c810a4d34c25.webp)

- Access 유저 생성 확인
    ![](08c39cecf5057388.webp)

<a id="229eda9b0fe180688d32dabdd5cd4588"></a>

### 4&#46; DB 연결

- 왼쪽 메뉴 &#45; Cluster &#45; Connect 클릭
    ![](4514c88826d5eb8a.webp)

- 연결 유형 선택
    ![](b48a27323e4fbfa0.webp)

    - Shell 로 진행

- mongsh 로 DB 연결
    ![](6415274771bdd3dc.webp)

    <a id="229eda9b0fe180e48664ff011090e658"></a>

    ```bash
    # mongosh 설치
    brew install mongosh

    # mongosh 연결
    mongosh "mongodb+srv://subdev.kzmznlq.mongodb.net/" --apiVersion 1 --username subdev
     # 비밀번호 입력: 09uVKqfRQBenQPry
    ```

    <details>
    <summary>비밀번호 새로 발급</summary>

    > ✏️ 비밀번호가 기억나지 않는 경우, 새로 발급 가능하다&#46; 

    - Database Access &#45; 유저 대시보드 &#45; Edit 클릭
        ![](08c39cecf5057388.webp)

    - 비밀번호 새로 설정
        ![](c0005e0d8ec560d1.webp)

        ![](884dde9e047dc8be.webp)

        - <code>update User</code>를 통해 수정해야 적용된다&#46;

    </details>

- 정상 연결 확인
    ![](668ed220c8e264f5.webp)
