---
order: 0
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: fffeda9b-0fe1-8185-880a-f461a42ef937
title: SQL 기초
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 108eda9b-0fe1-80a6-8a2b-c21df3ab9492
    title: 내일 배움 캠프 ( 백엔드 코스 7기)
  - id: 10aeda9b-0fe1-80df-a9e7-c0a68dc3edaa
    title: Spring 사전캠프 퀘스트 모음집
  - id: fffeda9b-0fe1-8185-880a-f461a42ef937
    title: SQL 기초
excerpt: "1. 데이터베이스(Database)와 테이블(Table) - 데이터베이스(Database): 여러 테이블을 포함하는 큰 틀입니다. - 테이블(Table): 데이터가 행(row)과 열(column)로 구성된 구조로 저장되는 곳입니다. 각 행은 하나의 데이터 레코드를 나타내며, 각 열은 데이터의 속성을 나타냅니다. 2. SQ"
cover: null
icon: 🗝️
notionProperties: {}
schema_version: 1
parent_id: 10aeda9b-0fe1-80df-a9e7-c0a68dc3edaa
created: 2024-09-23T10:56:26.503Z
updated: 2024-09-23T11:01:39.730Z
legacy_path: Main/내일 배움 캠프 ( 백엔드 코스 7기)-c21df3ab9492/Spring 사전캠프 퀘스트 모음집-c0a68dc3edaa/SQL 기초-f461a42ef937/index.md
legacy_category: 내일 배움 캠프 ( 백엔드 코스 7기)
source_url: https://beautiful-college-c84.notion.site/fffeda9b0fe18185880af461a42ef937
---
<a id="fffeda9b0fe1814fa01bddd536dda1c9"></a>

## 1&#46; <strong>데이터베이스(Database)와 테이블(Table)</strong>

- <strong>데이터베이스(Database)</strong>&#58; 여러 테이블을 포함하는 큰 틀입니다&#46;

- <strong>테이블(Table)</strong>&#58; 데이터가 행(row)과 열(column)로 구성된 구조로 저장되는 곳입니다&#46; 각 행은 하나의 데이터 레코드를 나타내며, 각 열은 데이터의 속성을 나타냅니다&#46;

<a id="fffeda9b0fe18100a84cc1d5c729a6c5"></a>

## 2&#46; <strong>SQL 기본 명령어</strong>

<a id="fffeda9b0fe1811a8f53dd99f874df24"></a>

SQL에서는 데이터베이스와 테이블을 생성하고, 데이터를 조회, 삽입, 수정, 삭제하는 등의 작업을 수행할 수 있습니다&#46;

<a id="fffeda9b0fe1810abcd6dc78bb55f05e"></a>

### 2&#46;1&#46; <strong>데이터베이스 생성</strong>

<a id="fffeda9b0fe1815498fefcde66a776fe"></a>

데이터베이스를 새로 생성할 때는 <code>CREATE DATABASE</code> 명령어를 사용합니다&#46;

<a id="fffeda9b0fe181229174f45485e18780"></a>

```sql
CREATE DATABASE 데이터베이스이름;
```

<a id="fffeda9b0fe18194bc5dfed5538ff77a"></a>

### 2&#46;2&#46; <strong>테이블 생성</strong>

<a id="fffeda9b0fe1813da3bbdb2dca7a5e77"></a>

테이블을 생성할 때는 <code>CREATE TABLE</code> 명령어를 사용합니다&#46;

<a id="fffeda9b0fe1814a9071f78eb229fec7"></a>

```sql
CREATE TABLE 테이블이름 (
    컬럼1 데이터타입,
    컬럼2 데이터타입,
    ...
);
```

<a id="fffeda9b0fe1812db384ff963dec8369"></a>

예시&#58;

<a id="fffeda9b0fe181acb1c5fff2cdbf31f0"></a>

```sql
CREATE TABLE students (
    id INT,
    name VARCHAR(50),
    age INT
);
```

<a id="fffeda9b0fe181778b51d9d96e08e9c1"></a>

<strong>해석 </strong>&#58; students 라는 이름의 테이블을 생성합니다&#46; 이 테이블에는 세 개의 열이 있습니다&#58;

- <code>id</code>&#58; 정수형 데이터를 저장하는 열 (<code>INT</code>)&#46;

- <code>name</code>&#58; 최대 50자까지의 문자열을 저장할 수 있는 열 (<code>VARCHAR(50)</code>)&#46;

- <code>age</code>&#58; 정수형 데이터를 저장하는 열 (<code>INT</code>)&#46;

<a id="fffeda9b0fe181b89b47d529920dc387"></a>

### 2&#46;3&#46; <strong>데이터 조회 (SELECT)</strong>

<a id="fffeda9b0fe1813da90ef3ecc46f315b"></a>

테이블에서 데이터를 조회할 때는 <code>SELECT</code> 명령어를 사용합니다&#46;

<a id="fffeda9b0fe1818fa3f3e22a831ed2c6"></a>

```sql
SELECT 컬럼1, 컬럼2, ... FROM 테이블이름;
```

<a id="fffeda9b0fe18191b8e7f22927a8dc3b"></a>

예시&#58;

<a id="fffeda9b0fe181a78b4efea714ad860e"></a>

```sql
SELECT name, age FROM students; 
//students 테이블에서 name과 age 열의 데이터를 조회합니다.
```

- <strong><code>WHERE</code></strong><strong> 절</strong>&#58; 특정 조건에 맞는 데이터만 조회합니다&#46;
    <a id="fffeda9b0fe181d7b783c38bc21ac3f1"></a>

    ```sql
    SELECT name, age FROM students WHERE age > 20;
    //students 테이블에서 age 값이 20보다 큰 학생들의 name과 age를 조회합니다.
    ```

- <strong><code>ORDER BY</code></strong><strong> 절</strong>&#58; 조회한 데이터를 정렬합니다&#46;
    <a id="fffeda9b0fe181ecb863c0e4d9496e59"></a>

    ```sql
    SELECT name, age FROM students ORDER BY age DESC;
    //students 테이블에서 name과 age를 조회하되, age를 기준으로 내림차순(DESC)으로 정렬합니다. 즉, 나이가 많은 학생부터 순서대로 정렬됩니다.
    ```

- <strong><code>LIMIT</code></strong><strong> 절</strong>&#58; 조회할 데이터의 개수를 제한합니다&#46;
    <a id="fffeda9b0fe181efb3add2e5c5512b5b"></a>

    ```sql
    SELECT name, age FROM students LIMIT 5;
    //students 테이블에서 name과 age를 조회하되, 최대 5개의 행만 조회합니다.
    ```

<a id="fffeda9b0fe181329c0ae466a3aaeb1d"></a>

### 2&#46;4&#46; <strong>데이터 삽입 (INSERT)</strong>

<a id="fffeda9b0fe1813391fcd1d08937036e"></a>

테이블에 새로운 데이터를 추가할 때는 <code>INSERT INTO</code> 명령어를 사용합니다&#46;

<a id="fffeda9b0fe181a5a7a0d7b95b10c145"></a>

```sql
INSERT INTO 테이블이름 (컬럼1, 컬럼2, ...) VALUES (값1, 값2, ...)
```

<a id="fffeda9b0fe18106ae8dc2f37e97e463"></a>

```sql
//예시
INSERT INTO students (id, name, age) VALUES (1, 'Alice', 23);
```

<a id="fffeda9b0fe1813ba6daf957dd5cb88a"></a>

### 2&#46;5&#46; <strong>데이터 수정 (UPDATE)</strong>

<a id="fffeda9b0fe1815dbc0be257059ecd2c"></a>

기존 데이터를 수정할 때는 <code>UPDATE</code> 명령어를 사용합니다&#46;

<a id="fffeda9b0fe18197870cf96009543477"></a>

```sql
UPDATE 테이블이름 SET 컬럼1 = 값1, 컬럼2 = 값2 WHERE 조건;
```

<a id="fffeda9b0fe181ee95f3f3a48b704d72"></a>

```sql
//예시
UPDATE students SET age = 24 WHERE id = 1;
//students 테이블에서 id가 1인 학생의 age 값을 24로 수정
```

<a id="fffeda9b0fe181c385e1cb51ef80b52e"></a>

### 2&#46;6&#46; <strong>데이터 삭제 (DELETE)</strong>

<a id="fffeda9b0fe181ad9a2ae4966f6ca684"></a>

테이블에서 데이터를 삭제할 때는 <code>DELETE FROM</code> 명령어를 사용합니다&#46;

<a id="fffeda9b0fe181a3bfb0e2e0892cc07e"></a>

```sql
DELETE FROM 테이블이름 WHERE 조건;
```

<a id="fffeda9b0fe1811e9fe0f107d8c7aa9c"></a>

예시&#58;

<a id="fffeda9b0fe181ccb296fe4c4e3bbf48"></a>

```sql
DELETE FROM students WHERE id = 1
//students 테이블에서 id가 1인 행을 삭제
```

<a id="fffeda9b0fe181249dfec63dc555024b"></a>

## 3&#46; <strong>기본 키와 외래 키</strong>

- <strong>기본 키(Primary Key)</strong>&#58; 테이블에서 각 행을 고유하게 식별하는 열(또는 열의 조합)입니다&#46;

- <strong>외래 키(Foreign Key)</strong>&#58; 다른 테이블의 기본 키를 참조하는 열로, 테이블 간의 관계를 나타냅니다&#46;

<a id="fffeda9b0fe18166ade5dc6f32d6523f"></a>

예시&#58;

<a id="fffeda9b0fe181768dd1cc84fa47a418"></a>

```sql
CREATE TABLE orders (
    order_id INT PRIMARY KEY,
    student_id INT,
    FOREIGN KEY (student_id) REFERENCES students(id)
);
```

<a id="fffeda9b0fe181d8aa71de2f4e41ba5b"></a>

<strong>해석 </strong>&#58; orders 라는 이름의 테이블을 생성합니다&#46; 이 테이블에는 두 개의 열이 있습니다&#58;

- <code>order&#95;id</code>&#58; 정수형 데이터를 저장하는 열로, 이 열이 기본 키(<code>PRIMARY KEY</code>)입니다&#46; 즉, <code>orders</code> 테이블의 각 행을 고유하게 식별합니다&#46;

- <code>student&#95;id</code>&#58; 정수형 데이터를 저장하는 열로, <code>students</code> 테이블의 <code>id</code>를 참조하는 외래 키(<code>FOREIGN KEY</code>)입니다&#46; 이를 통해 <code>orders</code> 테이블의 각 주문이 어떤 학생과 관련이 있는지를 나타낼 수 있습니다&#46;

<a id="fffeda9b0fe181a08eaae9fbc6154c13"></a>

## 4&#46; <strong>집계 함수(Aggregate Functions)</strong>

<a id="fffeda9b0fe181b4b2d1fde15b970d4a"></a>

집계 함수는 여러 행의 값을 계산하여 하나의 결과를 반환하는 함수입니다&#46;

- <strong>COUNT()</strong>&#58; 행의 개수를 셉니다&#46;
    <a id="fffeda9b0fe181d18c44df39b789aec8"></a>

    ```sql
    SELECT COUNT(*) FROM students;
    ```

- <strong>SUM()</strong>&#58; 숫자 값의 합을 계산합니다&#46;
    <a id="fffeda9b0fe181a58de8f2d57d5e8616"></a>

    ```sql
    SELECT SUM(age) FROM students;
    ```

- <strong>AVG()</strong>&#58; 숫자 값의 평균을 계산합니다&#46;
    <a id="fffeda9b0fe181939e6cfeac3fe6d23a"></a>

    ```sql
    SELECT AVG(age) FROM students;
    ```

- <strong>MAX()</strong>&#58; 최대 값을 찾습니다&#46;
    <a id="fffeda9b0fe1812cab5dfbe27a7ce210"></a>

    ```sql
    SELECT MAX(age) FROM students;
    ```

- <strong>MIN()</strong>&#58; 최소 값을 찾습니다&#46;
    <a id="fffeda9b0fe181f0a308d800aaeda85d"></a>

    ```sql
    SELECT MIN(age) FROM students;
    ```

<a id="fffeda9b0fe181338e8cc6a2a510fa8d"></a>

## 5&#46; <strong>SQL 조건문</strong>

- <strong>AND</strong>&#58; 두 조건이 모두 참일 때 사용합니다&#46;
    <a id="fffeda9b0fe181c18d3ec252f9788311"></a>

    ```sql
    SELECT * FROM students WHERE age > 20 AND name = 'Alice';
    ```

- <strong>OR</strong>&#58; 두 조건 중 하나만 참이면 사용합니다&#46;
    <a id="fffeda9b0fe18152b874e316bfc1f9fa"></a>

    ```sql
    SELECT * FROM students WHERE age > 20 OR name = 'Bob';
    ```

- <strong>NOT</strong>&#58; 조건이 거짓일 때 사용합니다&#46;
    <a id="fffeda9b0fe181989513e890b04cf8a3"></a>

    ```sql
    SELECT * FROM students WHERE NOT age > 20;
    ```
