---
order: 31
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1c3eda9b-0fe1-811c-bd2b-fbe6ee063202
title: "[실습] 백엔트 프로젝트(Nest.js) Docker로 실행"
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-8138-94e1-d1a8abd3203c
    title: Docker
  - id: 1c3eda9b-0fe1-8115-b158-c17d844ab16c
    title: 비전공자도 이해할 수 있는 Docker 입문/실전
  - id: 1c3eda9b-0fe1-811c-bd2b-fbe6ee063202
    title: "[실습] 백엔트 프로젝트(Nest.js) Docker로 실행"
excerpt: 백엔드 프로젝트(Nest.js)를 Docker로 실행 --- 1. Next.js 프로젝트 생성 bash Nest CLI 설치 npm i -g @nestjs/cli nest new {프로젝트명} nest new my-server 1. Dockerfile 작성 docker FROM node WORKDIR /app COPY .
cover: null
icon: null
notionProperties:
  중요도: Yes
  상태: 완료
schema_version: 1
parent_id: 1c3eda9b-0fe1-8115-b158-c17d844ab16c
created: 2025-03-27T07:47:52.764Z
updated: 2025-03-27T07:47:52.764Z
legacy_path: Main/Docker-d1a8abd3203c/비전공자도 이해할 수 있는 Docker 입문-실전-c17d844ab16c/[실습] 백엔트 프로젝트(Nest.js) Docker로 실행-fbe6ee063202/index.md
legacy_category: Docker
source_url: https://beautiful-college-c84.notion.site/1c3eda9b0fe1811cbd2bfbe6ee063202
---
<a id="1c3eda9b0fe181948ba8d675290abe23"></a>

## 백엔드 프로젝트(Nest&#46;js)를 Docker로 실행

---

![](289a0686f75e8278.webp)

1. Next&#46;js 프로젝트 생성
    <a id="1c3eda9b0fe1812b8240e74f3ee51b9a"></a>

    ```bash
    # Nest CLI 설치
    npm i -g @nestjs/cli

    # nest new {프로젝트명}
    nest new my-server
    ```

1. Dockerfile 작성
    ![](1880f798402493f3.webp)

    <a id="1c3eda9b0fe181189a7be9fd66008327"></a>

    ```docker
    FROM node

    WORKDIR /app

    COPY . .

    RUN npm install

    RUN npm run build

    EXPOSE 3000

    ENTRYPOINT [ "node", "dist/main.js" ]
    ```

1. <strong>&#46;dockerignore 작성</strong>
    ![](38ee4be90c8b29d6.webp)

    <a id="1c3eda9b0fe1811ca29ad017ee0caa2f"></a>

    ```docker
    node_modules
    ```

    <a id="1c3eda9b0fe181b0a9e3d7365066983d"></a>

    이미지를 생성할 때 <code>npm install</code>을 통해, 필요한 의존성만 설치한다&#46;

    <a id="1c3eda9b0fe1818bbdbac80fe239dac1"></a>

     → 호스트 컴퓨터에 있는 <code>node&#95;modules</code>는 컨테이너로 복사할 필요가 없다&#46; 

1. 이미지 build
    <a id="1c3eda9b0fe181e19618c689cc15883d"></a>

    ```bash
    docker build -t my-server .

    # 이미지 생성 확인 
    docker image ls
    ```

1. <strong>생성한 이미지를 컨테이너로 실행</strong>
    <a id="1c3eda9b0fe181f4a1ece0cf7c6d1a15"></a>

    ```bash
    docker run -d -p 3000:3000 my-server

    # 컨테이너 실행 확인
    docker ps
    ```

1. <a href="http://localhost:3000">localhost&#58;3000</a> 호출
    <a id="1c3eda9b0fe1816eacc2fd2957977069"></a>

    ```bash
    curl -X GET "http://localhost:3000"
    ```

    ![](3951a1ae1972d051.webp)

1. 실행 컨테이너 중지/삭제, 이미지 삭제
    <a id="1c3eda9b0fe181248184f6a1934349b8"></a>

    ```bash
    docker stop {컨테이너 ID}
    docker rm {컨테이너 ID}
    docker image rm {이미지 ID}
    ```
