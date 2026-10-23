---
order: 20
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1c3eda9b-0fe1-819c-a71f-e072ff165304
title: "[ 실습 ] MySQL, Redis"
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-8138-94e1-d1a8abd3203c
    title: Docker
  - id: 1c3eda9b-0fe1-8115-b158-c17d844ab16c
    title: 비전공자도 이해할 수 있는 Docker 입문/실전
  - id: 1c3eda9b-0fe1-819c-a71f-e072ff165304
    title: "[ 실습 ] MySQL, Redis"
excerpt: "[ 실습 ] MySQL, Redis --- 1. compose 파일 작성 - compose.yml yaml services: my-db: containername: my-db image: mysql environment: MYSQLROOTPASSWORD: pwd1234 volumes: - ~/Develop/docker-m"
cover: null
icon: null
notionProperties:
  Tags: Docker Compose 2
  중요도: No
  상태: 완료
schema_version: 1
parent_id: 1c3eda9b-0fe1-8115-b158-c17d844ab16c
created: 2025-03-27T07:47:52.767Z
updated: 2025-03-27T07:47:52.767Z
legacy_path: Main/Docker-d1a8abd3203c/비전공자도 이해할 수 있는 Docker 입문-실전-c17d844ab16c/[ 실습 ] MySQL, Redis-e072ff165304/index.md
legacy_category: Docker
source_url: https://beautiful-college-c84.notion.site/1c3eda9b0fe1819ca71fe072ff165304
---
<a id="1c3eda9b0fe1818ea633ca5450cc7148"></a>

## &#91; 실습 &#93; MySQL, Redis 

---

<details>
<summary>1&#46; compose 파일 작성</summary>

- compose&#46;yml
    <a id="1c3eda9b0fe1817080afe0ea28c20606"></a>

    ```yaml
    services:
      my-db:
        container_name: my-db
        image: mysql
        environment:
          MYSQL_ROOT_PASSWORD: pwd1234
        volumes:
          - ~/Develop/docker-mysql/mysql_data:/var/lib/mysql
        ports:
          - 3306:3306

      my-cache-server:
        container_name: my-redis
        image: redis
        ports:
          - 6379:6379
    ```

</details>

<details>
<summary>2&#46; compose 파일 실행</summary>

<a id="1c3eda9b0fe181ec99a8c841eea50be4"></a>

```bash
docker compose up -d 
```

![](0891c10117a7cdf0.webp)

</details>

<details>
<summary>3&#46; 실행 확인</summary>

<a id="1c3eda9b0fe18161884ad6b701aff0d0"></a>

```bash
docker compose ps 
```

![](4762486ec076aa9c.webp)

</details>

<details>
<summary>4&#46; 내부 컨테이너 접속</summary>

<details>
<summary>mysql</summary>

- mysql 접속
    <a id="1c3eda9b0fe1815b9d61fbcd8a192b3a"></a>

    ```bash
    # mysql 컨테이너 내부 bash 접속
    docker exec -it my-db bash 

    # mysql cli 접속
    mysql -u root -p
    	# password 입력
    ```

- DB 생성 및 테이블, 데이터 삽입
    <a id="1c3eda9b0fe181f1a161c71931eef521"></a>

    ```bash
    # DB 생성
    create database [DB명];

    # DB 생성 확인
    show databases;

    # 생성한 DB로 이동
    use [DB명] 

    # 테이블 생성
    create table [테이블명](
    		[필드 1 ... ],
    		[필드 2 ... ],
    		 . . .
    );

    # 테이블 생성 확인
    show tables

    # 데이터 삽입
    INSERT INTO [테이블명] (필드1, 필드2, ...)
    VALUES
    	('data1.1', 'date1.2', ...),
    	('data2.1', 'date2.2', ...),
      ('data3.1', 'date3.2', ...);
      
    # 테이블 데이터 확인
    SELECT * FROM [테이블명]
    ```

    <details>
    <summary>ex) users 테이블 생성 및 데이터 삽입 </summary>

    <a id="1c3eda9b0fe1817ba278cc9f1327ed18"></a>

    ```bash
    # DB 생성
    create database test;

    # DB 생성 확인
    show databases;

    # 생성한 DB로 이동
    use test; 

    # 테이블 생성
    CREATE TABLE users (
        id            INT AUTO_INCREMENT PRIMARY KEY,  -- 기본 키 (자동 증가)
        username      VARCHAR(50) NOT NULL UNIQUE,     -- 사용자 이름 (고유)
        email         VARCHAR(100) NOT NULL UNIQUE,    -- 이메일 (고유)
        password      VARCHAR(255) NOT NULL,           -- 비밀번호 (암호화 필요)
        created_at    TIMESTAMP DEFAULT CURRENT_TIMESTAMP, -- 생성 일자
        updated_at    TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP -- 업데이트 일자
    );

    # 테이블 생성 확인
    show tables

    # 데이터 삽입
    INSERT INTO users (username, email, password)
    VALUES 
        ('john_doe', 'john@example.com', 'hashed_password_1'),
        ('alice_smith', 'alice@example.com', 'hashed_password_2'),
        ('bob_jones', 'bob@example.com', 'hashed_password_3');
      
    # 테이블 데이터 확인
    SELECT * FROM users;
    ```

    ![](31c92d9b51fd94ab.webp)

    ![](4660a4fc996068a9.webp)

    ![](0796a8f7617eb092.webp)

    </details>

</details>

<details>
<summary>redis</summary>

<a id="1c3eda9b0fe1813e83dcdd014591f35f"></a>

```bash
# 실행 중인 compose 컨테이너 확인
docker compose ps

# 컨테이너 내부 redis-cli 접속
docker exec -it my-redis redis-cli

# redis 데이터 저장
set 1 test

# 확인
get 1
```

![](08203957d824072f.webp)

![](223748bad07c5974.webp)

</details>

</details>

<details>
<summary>5&#46; <strong>compose로 실행된 컨테이너 삭제</strong></summary>

<a id="1c3eda9b0fe18133a42bf7caad1901b5"></a>

```bash
docker compose down
```

</details>
