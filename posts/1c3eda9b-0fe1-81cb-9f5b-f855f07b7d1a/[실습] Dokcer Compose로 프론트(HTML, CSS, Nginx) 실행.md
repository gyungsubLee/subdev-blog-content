---
order: 25
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1c3eda9b-0fe1-81cb-9f5b-f855f07b7d1a
title: "[실습] Dokcer Compose로 프론트(HTML, CSS, Nginx) 실행"
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-8138-94e1-d1a8abd3203c
    title: Docker
  - id: 1c3eda9b-0fe1-8115-b158-c17d844ab16c
    title: 비전공자도 이해할 수 있는 Docker 입문/실전
  - id: 1c3eda9b-0fe1-81cb-9f5b-f855f07b7d1a
    title: "[실습] Dokcer Compose로 프론트(HTML, CSS, Nginx) 실행"
excerpt: "[실습] Dokcer Compose로 프론트(HTML, CSS, Nginx) 실행 --- 1. HTML, CSS 파일 생성 - idnex.html ⚠️ Nginx의 기본 설정에 의하면 메인 페이지(첫 페이지)의 파일명을 index.html이라고 지어야 한다. html My Web Page - style.css html {"
cover: null
icon: null
notionProperties:
  상태: 완료
schema_version: 1
parent_id: 1c3eda9b-0fe1-8115-b158-c17d844ab16c
created: 2025-03-27T07:47:52.766Z
updated: 2025-03-27T07:47:52.766Z
legacy_path: Main/Docker-d1a8abd3203c/비전공자도 이해할 수 있는 Docker 입문-실전-c17d844ab16c/[실습] Dokcer Compose로 프론트(HTML, CSS, Nginx) 실행-f855f07b7d1a/index.md
legacy_category: Docker
source_url: https://beautiful-college-c84.notion.site/1c3eda9b0fe181cb9f5bf855f07b7d1a
---
<a id="1c3eda9b0fe1810c8ae6c6fc1009a15c"></a>

## &#91;실습&#93; Dokcer Compose로 프론트(HTML, CSS, Nginx) 실행

---

<details>
<summary>1&#46; HTML, CSS 파일 생성</summary>

- idnex&#46;html
    > ⚠️ 
    > 
    > <a id="1c3eda9b0fe1817c8df9fba461b8983b"></a>
    > 
    > Nginx의 기본 설정에 의하면 메인 페이지(첫 페이지)의 파일명을 <code>index&#46;html</code>이라고 지어야 한다&#46; 

    <a id="1c3eda9b0fe181198d9dc9fdc2a2106b"></a>

    ```html
    <!DOCTYPE html>
    <head>
        <meta charset="UTF-8">
        <link rel="stylesheet" href="style.css">
    </head>
    <body>
        <h1>My Web Page</h1>
    </body>
    </html>
    ```

- style&#46;css
    <a id="1c3eda9b0fe18159961ac49c43d544e4"></a>

    ```html
    * {
      color: blue;
    }
    ```

</details>

<details>
<summary>2&#46; Dockerfile, <strong>compose 파일 작성</strong></summary>

- <strong>Dockerfile</strong>
    <a id="1c3eda9b0fe181c1b588ea1389279cf6"></a>

    ```docker
    FROM nginx 
    COPY ./ /usr/share/nginx/html
    ```

- compose&#46;yml
    <details>
    <summary>Docker CLI</summary>

    <a id="1c3eda9b0fe18190acfcd60532af0a4e"></a>

    ```bash
    docker build -t my-web-server .
    docker run -d -p 80:80 my-web-server
    ```

    </details>

    <a id="1c3eda9b0fe181bfbc42fda0f224c0d1"></a>

    ```yaml
    services:
      my-web-server:
        build: .
        ports:
          - 80:80
    ```

</details>

<details>
<summary>3&#46; compose 파일 실행</summary>

<a id="1c3eda9b0fe18176a5bcff161892f4a2"></a>

```bash
docker compose up -d --build
```

</details>

<details>
<summary>4&#46; compose 실행 현황</summary>

<a id="1c3eda9b0fe181c69641d2a199ff85e0"></a>

```bash
docker compose ps
docker ps
```

</details>

<details>
<summary>5&#46; <a href="http://localhost:80">localhost&#58;80</a> 호출</summary>

![](7014853ca60bc939.webp)

</details>

<details>
<summary>6&#46; compose로 실행된 컨테이너 삭제</summary>

<a id="1c3eda9b0fe18107ba75f1120c64720a"></a>

```bash
docker compose down
```

</details>
