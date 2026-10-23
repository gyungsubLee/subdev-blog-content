---
order: 5
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1c3eda9b-0fe1-81fb-87c7-c36547cf72ef
title: mysql 최초 비밀번호 설청
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-8114-a6f8-e8c2debc9fa0
    title: DBMS
  - id: 1c3eda9b-0fe1-81ef-9506-cdc300921ef3
    title: MySQL
  - id: 1c3eda9b-0fe1-81fb-87c7-c36547cf72ef
    title: mysql 최초 비밀번호 설청
excerpt: 1. MySQL 접속 java mysql -u root Or java mysql -u root -p // Enter 1. mysql db 사용 shell mysql use mysql; 1. 현재 패스워드 설정 관련 내용 리스트 shell mysql select host,user,authenticationstring fro
cover: null
icon: null
notionProperties:
  상태: 완료
  Reference1: "[https://indienote.tistory.com/585](https://indienote.tistory.com/585)"
schema_version: 1
parent_id: 1c3eda9b-0fe1-81ef-9506-cdc300921ef3
created: 2025-03-27T07:47:52.776Z
updated: 2025-03-27T07:47:52.776Z
legacy_path: Main/DBMS-e8c2debc9fa0/MySQL-cdc300921ef3/mysql 최초 비밀번호 설청-c36547cf72ef/index.md
legacy_category: DBMS
source_url: https://beautiful-college-c84.notion.site/1c3eda9b0fe181fb87c7c36547cf72ef
---
1. <strong>MySQL 접속</strong>
    <a id="1c3eda9b0fe1815f81fee1e548497a46"></a>

    ```java
    mysql -u root 
    ```

    <a id="1c3eda9b0fe181478e1ec080d18446ef"></a>

    Or

    <a id="1c3eda9b0fe181bc9328c867c743cca0"></a>

    ```java
    mysql -u root -p
    // Enter
    ```

1. <strong>mysql db 사용</strong>
    <a id="1c3eda9b0fe1813497fdd21665b56359"></a>

    ```shell
    mysql> use mysql;
    ```

1. <strong> 현재 패스워드 설정 관련 내용 리스트</strong>
    <a id="1c3eda9b0fe181a48e21ef02a2d4bca5"></a>

    ```shell
    mysql> 
    		select host,user,authentication_string from user;
    ```

1. <strong>새로운 패스워드 설정</strong>
    <details>
    <summary><code>mysql&#95;native&#95;password</code> 플러그인이 더이상 사용되지 않음</summary>

    <a id="1c3eda9b0fe181c7822ef5db6c67720b"></a>

    ```shell
    alter user 'root'@'localhost' identified with mysql_native_password by '패스워드 입력';
    ```

    </details>

    - MySQL 8&#46;4이상 부터 <code>mysql&#95;native&#95;password</code> 플러그인을 더 이상 로드하지 않도록 변경되었음

    - <code>caching&#95;sha2&#95;password</code>  사용한 인증

    <a id="1c3eda9b0fe181f682adc511c004e266"></a>

    ```bash
    ALTER USER '<USERNAME>'@'<HOST>' IDENTIFIED WITH caching_sha2_password BY '<PASSWORD>';
    ```

    <details>
    <summary>ex) </summary>

    <a id="1c3eda9b0fe181cc9fc7e5cb57e3bbe1"></a>

    ```bash
    ALTER USER 'root'@'localhost' IDENTIFIED WITH caching_sha2_password BY '12345678'
    ```

    </details>

- 외부에서 들어오는 계정을 생성할 필요가 있다면
    > 해당 접속이 들어오는 MySQL 서버 IP 주소와 매핑

    <a id="1c3eda9b0fe18153b685e1bc10ce4fbe"></a>

    ```shell
    mysql> create user 'root'@'192.168.0.100' identified with mysql_native_password by 'new_password_you_want';
    ```
