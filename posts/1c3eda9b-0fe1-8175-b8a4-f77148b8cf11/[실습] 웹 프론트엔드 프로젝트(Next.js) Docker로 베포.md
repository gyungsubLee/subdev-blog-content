---
order: 32
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1c3eda9b-0fe1-8175-b8a4-f77148b8cf11
title: "[실습] 웹 프론트엔드 프로젝트(Next.js) Docker로 베포"
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-8138-94e1-d1a8abd3203c
    title: Docker
  - id: 1c3eda9b-0fe1-8115-b158-c17d844ab16c
    title: 비전공자도 이해할 수 있는 Docker 입문/실전
  - id: 1c3eda9b-0fe1-8175-b8a4-f77148b8cf11
    title: "[실습] 웹 프론트엔드 프로젝트(Next.js) Docker로 베포"
excerpt: 웹 프론트엔드 프로젝트(Next.js) Docker로 배포 --- 1. Next.js 프로젝트 생성 bash npx create-next-app@latest 1. Dockerfile 작성 docker FROM node:20-alpine WORKDIR /app COPY . . RUN npm install RUN npm ru
cover: null
icon: null
notionProperties:
  중요도: Yes
  상태: 완료
schema_version: 1
parent_id: 1c3eda9b-0fe1-8115-b158-c17d844ab16c
created: 2025-03-27T07:47:52.764Z
updated: 2025-03-27T07:47:52.764Z
legacy_path: Main/Docker-d1a8abd3203c/비전공자도 이해할 수 있는 Docker 입문-실전-c17d844ab16c/[실습] 웹 프론트엔드 프로젝트(Next.js) Docker로 베포-f77148b8cf11/index.md
legacy_category: Docker
source_url: https://beautiful-college-c84.notion.site/1c3eda9b0fe18175b8a4f77148b8cf11
---
<a id="1c3eda9b0fe1818484acda64103fde3d"></a>

## 웹 프론트엔드 프로젝트(Next&#46;js) Docker로 배포

---

![](74c9ea71d9a655de.webp)

1. <strong>Next&#46;js 프로젝트 생성 </strong>
    <a id="1c3eda9b0fe181bb9067efdce3ea150b"></a>

    ```bash
    npx create-next-app@latest
    ```

1. <strong><code>Dockerfile</code></strong> 작성
    <a id="1c3eda9b0fe1811a9694d38023f67ab2"></a>

    ```docker
    FROM node:20-alpine

    WORKDIR /app

    COPY . .

    RUN npm install

    RUN npm run build

    EXPOSE 3000

    ENTRYPOINT [ "npm", "run", "start" ]
    ```

    - <code>alpine</code> 
        - 불필요한 프로그램을 포함하지 않고 이미지 크기를 최소화한 버전

        - 실제 배포 할 때도 되도록이면 <code>alpine</code> 버전을 사용한다&#46; 

1. &#46;<strong><code>dockerignore</code></strong> 작성
    <a id="1c3eda9b0fe18149917adbbb966e288a"></a>

    ```docker
    node_modules
    ```

    <a id="1c3eda9b0fe1819c808eeaa4974965e2"></a>

    이미지 생성 시, npm install을 통해 필요한 의존성을 설치한다&#46; <br>따라서 호스트 컴퓨터에 있는 <code>node&#95;modules</code>는 컨테이너로 복사할 필요가 없다&#46; 

1. 이미지 빌드, 실행
    <a id="1c3eda9b0fe181d69db8d588e44b6d09"></a>

    ```bash
    docker build -t my-web-server .

    docker image ls

    docker run -d -p 3000:3000 my-web-server

    docker ps
    ```

1. <strong><a href="http://localhost:80">localhost&#58;80</a></strong><strong> 접속</strong>
    ![](108c3c95c62b5235.webp)

1. <strong>실행시킨 컨테이너 중지 / 삭제, 이미지 삭제</strong>
    <a id="1c3eda9b0fe18132a139ee128978b819"></a>

    ```bash
    docker stop {컨테이너 ID}
    docker rm {컨테이너 ID}
    docker image rm {이미지 ID}
    ```
