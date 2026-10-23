---
order: 18
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1c3eda9b-0fe1-810d-bffd-db686e061b22
title: "[ 실습 ] AWS EC2 - Spring Boot, MySQL, Redis 베포"
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-8138-94e1-d1a8abd3203c
    title: Docker
  - id: 1c3eda9b-0fe1-8115-b158-c17d844ab16c
    title: 비전공자도 이해할 수 있는 Docker 입문/실전
  - id: 1c3eda9b-0fe1-810d-bffd-db686e061b22
    title: "[ 실습 ] AWS EC2 - Spring Boot, MySQL, Redis 베포"
excerpt: EC2 콘솔 접속 --- - 해당하는 인스턴스 클릭 - 연결 클릭 - 해당 EC2의 콘솔 창으로 접속 ✏️ 브라우저에서 aws 콘솔로 접속하는 것 보다는, SSH로 터미널에서 접속하는 것이 더 자주 사용되고 편리하다. - 강의에서는 해당 내용을 다루지 않으니 추가 자료 조사 후 적용이 필요하다. - 코드 변경 시, pus
cover: 13d1152c95243081.webp
icon: null
notionProperties:
  중요도: Yes
  상태: 완료
schema_version: 1
parent_id: 1c3eda9b-0fe1-8115-b158-c17d844ab16c
created: 2025-03-27T07:47:52.768Z
updated: 2025-03-27T07:47:52.768Z
legacy_path: Main/Docker-d1a8abd3203c/비전공자도 이해할 수 있는 Docker 입문-실전-c17d844ab16c/[ 실습 ] AWS EC2 - Spring Boot, MySQL, Redis 베포-db686e061b22/index.md
legacy_category: Docker
source_url: https://beautiful-college-c84.notion.site/1c3eda9b0fe1810dbffddb686e061b22
---
<details>
<summary>EC2 콘솔 접속</summary>

---

- 해당하는 인스턴스 클릭
    ![](1d4d6ff3fb722084.webp)

- 연결 클릭
    ![](eb83c69c6cfba2c1.webp)

    ![](12218d4932fafd2b.webp)

- 해당 EC2의 콘솔 창으로 접속 
    ![](f4708eb9509c87a6.webp)

</details>

> ✏️ 
> 
> <a id="1c3eda9b0fe1813c9653d58931d80c26"></a>
> 
> 브라우저에서 aws 콘솔로 접속하는 것 보다는, SSH로 터미널에서 접속하는 것이 더 자주 사용되고 편리하다&#46; 
> 
> - 강의에서는 해당 내용을 다루지 않으니 추가 자료 조사 후 적용이 필요하다&#46; 

- 코드 변경 시, push &#45; 이전과 동일
    <a id="1c3eda9b0fe181b6bbaeea56af1cbe0e"></a>

    <a href="#/post/1c3eda9b-0fe1-81dc-87e3-e396c635e23c">페이지</a> 

- <code>compose&#46;yml</code>
    - Mysql, Redis 설정 정보 추가 

    <a id="1c3eda9b0fe18118b225df7c989fb0bf"></a>

    ```yaml
    services:
      instagram-server:
        image: 002177417362.dkr.ecr.ap-northeast-2.amazonaws.com/instagram-server:latest
        ports:
          - 8080:8080
        depends_on:
          my-db:
            condition: service_healthy
          my-cache-server:
            condition: service_healthy
      my-db:
        image: mysql
        environment:
          MYSQL_ROOT_PASSWORD: pwd1234
          MYSQL_DATABASE: mydb
        volumes:
          - ./mysql_data:/var/lib/mysql
        ports:
          - 3306:3306
        healthcheck:
          test: [ "CMD", "mysqladmin", "ping" ]
          interval: 5s
          retries: 10
      my-cache-server:
        image: redis
        ports:
          - 6379:6379
        healthcheck:
          test: [ "CMD", "redis-cli", "ping" ]
          interval: 5s
          retries: 10
    ```

- compose 실행
    <a id="1c3eda9b0fe181bda109d7b54828e1c2"></a>

    ```bash
    # compose 실행
    docker compose up -d --build

    # 실행 확인
    docker compose ps

    # 종료 
    docker compose down
    ```

- 확인
    ![](2a86230ad60c8584.webp)

    - redis
        ![](f9ee8feeaa536862.webp)
