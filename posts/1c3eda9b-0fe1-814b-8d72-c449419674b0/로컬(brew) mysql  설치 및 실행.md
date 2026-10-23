---
order: 9
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1c3eda9b-0fe1-814b-8d72-c449419674b0
title: 로컬(brew) mysql  설치 및 실행
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-8114-a6f8-e8c2debc9fa0
    title: DBMS
  - id: 1c3eda9b-0fe1-81ef-9506-cdc300921ef3
    title: MySQL
  - id: 1c3eda9b-0fe1-814b-8d72-c449419674b0
    title: 로컬(brew) mysql  설치 및 실행
excerpt: 🧐 데몬 MySQL 데몬으로 실행 plaintext brew services start mysql 데몬으로 실행되고있는 MySQL 종료 plaintext brew services stop mysql 데몬으로 실행되고 있는 프로그램 목록 확인 plaintext brew services list - Homebrew 를 통한
cover: null
icon: null
notionProperties:
  상태: 완료
schema_version: 1
parent_id: 1c3eda9b-0fe1-81ef-9506-cdc300921ef3
created: 2025-03-27T07:47:52.775Z
updated: 2025-03-27T07:47:52.775Z
legacy_path: Main/DBMS-e8c2debc9fa0/MySQL-cdc300921ef3/로컬(brew) mysql  설치 및 실행-c449419674b0/index.md
legacy_category: DBMS
source_url: https://beautiful-college-c84.notion.site/1c3eda9b0fe1814b8d72c449419674b0
---
<details>
<summary>🧐 데몬 </summary>

<details>
<summary>MySQL 데몬으로 실행</summary>

<a id="1c3eda9b0fe1815e8c8be001a6238ecf"></a>

```plaintext
brew services start mysql
```

</details>

<details>
<summary>데몬으로 실행되고있는 MySQL 종료</summary>

<a id="1c3eda9b0fe18100a898ee31c5d27c62"></a>

```plaintext
brew services stop mysql
```

</details>

<details>
<summary>데몬으로 실행되고 있는 프로그램 목록 확인</summary>

<a id="1c3eda9b0fe181cbb244dcfdd6f19320"></a>

```plaintext
brew services list
```

</details>

</details>

- <strong>Homebrew 를 통한 MySQL 설치</strong>
    <a id="1c3eda9b0fe18182bb19c89539d8f3d2"></a>

    <strong>설치</strong>

    <a id="1c3eda9b0fe1819e95dbe20c1d185c69"></a>

    ```plaintext
    brew install mysql
    ```

    <a id="1c3eda9b0fe181fe9881e69dc6cc477e"></a>

    설치 경로 확인

    <a id="1c3eda9b0fe181eea090c6c85fbedcd1"></a>

    ```plaintext
    which mysql
    ```

- 서비스 재시작
    <a id="1c3eda9b0fe1818b9adff50654627356"></a>

    ```bash
    brew services restart mysql
    ```

- MySQL 서버 실행
    <a id="1c3eda9b0fe18189abd5ed0c8f26e414"></a>

    ```plaintext
    mysql.server start
    ```

- MySQL 서버 종료
    <a id="1c3eda9b0fe181839c74d1ffa78d8e0d"></a>

    ```plaintext
    mysql.server stop
    ```

- MySQL 접속
    > <code>&#45;p</code> &#58; password, 비밀번호가 없는 경우 생략함

    - 초기 설정&#58; 비번 ❌
        <a id="1c3eda9b0fe181c3842ffb827102d9c8"></a>

        ```shell
        mysql -u root
        ```

    - 비번 설정 후 
        <a id="1c3eda9b0fe1815e8962d97b4d2aaca9"></a>

        ```plaintext
        mysql -u root -p
        ```

- MySQL 접속 종료
    <a id="1c3eda9b0fe181c493c1e0181e0ad240"></a>

    <code>quit</code> or <code>exit</code> 입력 후 종료
