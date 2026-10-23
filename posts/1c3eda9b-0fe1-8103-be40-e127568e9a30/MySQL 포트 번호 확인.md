---
order: 4
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1c3eda9b-0fe1-8103-be40-e127568e9a30
title: MySQL 포트 번호 확인
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-8114-a6f8-e8c2debc9fa0
    title: DBMS
  - id: 1c3eda9b-0fe1-81ef-9506-cdc300921ef3
    title: MySQL
  - id: 1c3eda9b-0fe1-8103-be40-e127568e9a30
    title: MySQL 포트 번호 확인
excerpt: "- shell mysql server status MySQL 쿼리로 확인 - MySQL 접속 shell mysql -u root -p - 글로벌 변수 ‘PORT’ 확인 shell SHOW GLOBAL VARIABLES LIKE 'PORT'; - MySQL 포트 번호 출력 확인"
cover: null
icon: null
notionProperties:
  상태: 완료
  Reference1: "[https://seyul.tistory.com/83](https://seyul.tistory.com/83)"
schema_version: 1
parent_id: 1c3eda9b-0fe1-81ef-9506-cdc300921ef3
created: 2025-03-27T07:47:52.776Z
updated: 2025-03-27T07:47:52.776Z
legacy_path: Main/DBMS-e8c2debc9fa0/MySQL-cdc300921ef3/MySQL 포트 번호 확인-e127568e9a30/index.md
legacy_category: DBMS
source_url: https://beautiful-college-c84.notion.site/1c3eda9b0fe18103be40e127568e9a30
---
- 
    <a id="1c3eda9b0fe181269c12d9d21bb6cba5"></a>

    ```shell
    mysql server status
    ```

<a id="1c3eda9b0fe181e28e26c542e0c7f577"></a>

### MySQL 쿼리로 확인 

- MySQL 접속
    <a id="1c3eda9b0fe181e5a0a2f0c633e83204"></a>

    ```shell
    mysql -u root -p
    ```

- 글로벌 변수 ‘PORT’ 확인
    <a id="1c3eda9b0fe18196a130eb9d13494a45"></a>

    ```shell
    SHOW GLOBAL VARIABLES LIKE 'PORT';
    ```

- MySQL 포트 번호 출력 확인
    ![](becf571bd63004ff.webp)
