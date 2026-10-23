---
order: 10
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: fffeda9b-0fe1-818e-b8b6-d0ddab386759
title: SQL 기초
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 108eda9b-0fe1-80a6-8a2b-c21df3ab9492
    title: 내일 배움 캠프 ( 백엔드 코스 7기)
  - id: 10aeda9b-0fe1-80c3-9114-e5ad96c892b3
    title: 1) SQL 문법 연습
  - id: fffeda9b-0fe1-818e-b8b6-d0ddab386759
    title: SQL 기초
excerpt: "1. 데이터베이스(Database)와 테이블(Table) - 데이터베이스(Database): 여러 테이블을 포함하는 큰 틀입니다. - 테이블(Table): 데이터가 행(row)과 열(column)로 구성된 구조로 저장되는 곳입니다. 각 행은 하나의 데이터 레코드를 나타내며, 각 열은 데이터의 속성을 나타냅니다. 2. SQ"
cover: null
icon: 🗝️
notionProperties: {}
schema_version: 1
parent_id: 10aeda9b-0fe1-80c3-9114-e5ad96c892b3
created: 2024-09-23T11:02:03.426Z
updated: 2024-09-23T11:02:50.472Z
legacy_path: Main/내일 배움 캠프 ( 백엔드 코스 7기)-c21df3ab9492/1) SQL 문법 연습-e5ad96c892b3/SQL 기초-d0ddab386759/index.md
legacy_category: 내일 배움 캠프 ( 백엔드 코스 7기)
source_url: https://beautiful-college-c84.notion.site/fffeda9b0fe1818eb8b6d0ddab386759
---
<a id="fffeda9b0fe18183bc3ed8f4e76d0584"></a>

## 1&#46; <strong>데이터베이스(Database)와 테이블(Table)</strong>

- <strong>데이터베이스(Database)</strong>&#58; 여러 테이블을 포함하는 큰 틀입니다&#46;

- <strong>테이블(Table)</strong>&#58; 데이터가 행(row)과 열(column)로 구성된 구조로 저장되는 곳입니다&#46; 각 행은 하나의 데이터 레코드를 나타내며, 각 열은 데이터의 속성을 나타냅니다&#46;

<a id="fffeda9b0fe18104a9d2d1d3daef09f4"></a>

## 2&#46; <strong>SQL 기본 명령어</strong>

<a id="fffeda9b0fe18133ba5df7d06705e9fd"></a>

SQL에서는 데이터베이스와 테이블을 생성하고, 데이터를 조회, 삽입, 수정, 삭제하는 등의 작업을 수행할 수 있습니다&#46;

<a id="fffeda9b0fe1819d8b76c464e694ec92"></a>

### 2&#46;1&#46; <strong>데이터베이스 생성</strong>

<a id="fffeda9b0fe181ae91d5e6c5244a7166"></a>

데이터베이스를 새로 생성할 때는 <code>CREATE DATABASE</code> 명령어를 사용합니다&#46;

<a id="fffeda9b0fe18126b7a9deb4b05c6d47"></a>

```sql
CREATE DATABASE 데이터베이스이름;
```

<a id="fffeda9b0fe181079111c3d3998fb349"></a>

### 2&#46;2&#46; <strong>테이블 생성</strong>

<a id="fffeda9b0fe18106a294ef78d9a67753"></a>

테이블을 생성할 때는 <code>CREATE TABLE</code> 명령어를 사용합니다&#46;

<a id="fffeda9b0fe1816f8f86d408966046c4"></a>

```sql
CREATE TABLE 테이블이름 (
    컬럼1 데이터타입,
    컬럼2 데이터타입,
    ...
);
```

<a id="fffeda9b0fe181f1b334c2808feb3469"></a>

예시&#58;

<a id="fffeda9b0fe181909050cbea9631b9a9"></a>

```sql
CREATE TABLE students (
    id INT,
    name VARCHAR(50),
    age INT
);
```

<a id="fffeda9b0fe1815e9091ef5e4bc74c18"></a>

<strong>해석 </strong>&#58; students 라는 이름의 테이블을 생성합니다&#46; 이 테이블에는 세 개의 열이 있습니다&#58;

- <code>id</code>&#58; 정수형 데이터를 저장하는 열 (<code>INT</code>)&#46;

- <code>name</code>&#58; 최대 50자까지의 문자열을 저장할 수 있는 열 (<code>VARCHAR(50)</code>)&#46;

- <code>age</code>&#58; 정수형 데이터를 저장하는 열 (<code>INT</code>)&#46;

<a id="fffeda9b0fe18100827dd7a7d898bb12"></a>

### 2&#46;3&#46; <strong>데이터 조회 (SELECT)</strong>

<a id="fffeda9b0fe18175ac6ce078afcc05bc"></a>

테이블에서 데이터를 조회할 때는 <code>SELECT</code> 명령어를 사용합니다&#46;

<a id="fffeda9b0fe181b894a9c427a7e6903e"></a>

```sql
SELECT 컬럼1, 컬럼2, ... FROM 테이블이름;
```

<a id="fffeda9b0fe181de9c8efd530ca9ce88"></a>

예시&#58;

<a id="fffeda9b0fe181ab9886d50c7613fd1a"></a>

```sql
SELECT name, age FROM students; 
//students 테이블에서 name과 age 열의 데이터를 조회합니다.
```

- <strong><code>WHERE</code></strong><strong> 절</strong>&#58; 특정 조건에 맞는 데이터만 조회합니다&#46;
    <a id="fffeda9b0fe1816b8884d9038d1223d3"></a>

    ```sql
    SELECT name, age FROM students WHERE age > 20;
    //students 테이블에서 age 값이 20보다 큰 학생들의 name과 age를 조회합니다.
    ```

- <strong><code>ORDER BY</code></strong><strong> 절</strong>&#58; 조회한 데이터를 정렬합니다&#46;
    <a id="fffeda9b0fe181ec81aed3202aa1050a"></a>

    ```sql
    SELECT name, age FROM students ORDER BY age DESC;
    //students 테이블에서 name과 age를 조회하되, age를 기준으로 내림차순(DESC)으로 정렬합니다. 즉, 나이가 많은 학생부터 순서대로 정렬됩니다.
    ```

- <strong><code>LIMIT</code></strong><strong> 절</strong>&#58; 조회할 데이터의 개수를 제한합니다&#46;
    <a id="fffeda9b0fe181cd8ab4e19e94274149"></a>

    ```sql
    SELECT name, age FROM students LIMIT 5;
    //students 테이블에서 name과 age를 조회하되, 최대 5개의 행만 조회합니다.
    ```

<a id="fffeda9b0fe181768421cd719666014b"></a>

### 2&#46;4&#46; <strong>데이터 삽입 (INSERT)</strong>

<a id="fffeda9b0fe181518bbceedd82f421fc"></a>

테이블에 새로운 데이터를 추가할 때는 <code>INSERT INTO</code> 명령어를 사용합니다&#46;

<a id="fffeda9b0fe18142945df7221eb467fb"></a>

```sql
INSERT INTO 테이블이름 (컬럼1, 컬럼2, ...) VALUES (값1, 값2, ...)
```

<a id="fffeda9b0fe181fe987cf6ce9ccdc2d4"></a>

```sql
//예시
INSERT INTO students (id, name, age) VALUES (1, 'Alice', 23);
```

<a id="fffeda9b0fe181e49d91ec49780fa4bf"></a>

### 2&#46;5&#46; <strong>데이터 수정 (UPDATE)</strong>

<a id="fffeda9b0fe181c0b57bd1fb429c9ff3"></a>

기존 데이터를 수정할 때는 <code>UPDATE</code> 명령어를 사용합니다&#46;

<a id="fffeda9b0fe181deb90ffb6974ed1b42"></a>

```sql
UPDATE 테이블이름 SET 컬럼1 = 값1, 컬럼2 = 값2 WHERE 조건;
```

<a id="fffeda9b0fe18173a1a4eb82cbd7d80e"></a>

```sql
//예시
UPDATE students SET age = 24 WHERE id = 1;
//students 테이블에서 id가 1인 학생의 age 값을 24로 수정
```

<a id="fffeda9b0fe181d090dfdc04bd2e6979"></a>

### 2&#46;6&#46; <strong>데이터 삭제 (DELETE)</strong>

<a id="fffeda9b0fe1811aafa0c2f1aa1d6ea2"></a>

테이블에서 데이터를 삭제할 때는 <code>DELETE FROM</code> 명령어를 사용합니다&#46;

<a id="fffeda9b0fe18196bb5bcbd6298d2d35"></a>

```sql
DELETE FROM 테이블이름 WHERE 조건;
```

<a id="fffeda9b0fe181469aede3eb0867aed7"></a>

예시&#58;

<a id="fffeda9b0fe18161be24c47cf03d2c2a"></a>

```sql
DELETE FROM students WHERE id = 1
//students 테이블에서 id가 1인 행을 삭제
```

<a id="fffeda9b0fe181d984b2df4deab5e349"></a>

## 3&#46; <strong>기본 키와 외래 키</strong>

- <strong>기본 키(Primary Key)</strong>&#58; 테이블에서 각 행을 고유하게 식별하는 열(또는 열의 조합)입니다&#46;

- <strong>외래 키(Foreign Key)</strong>&#58; 다른 테이블의 기본 키를 참조하는 열로, 테이블 간의 관계를 나타냅니다&#46;

<a id="fffeda9b0fe1819eb450d30c247df517"></a>

예시&#58;

<a id="fffeda9b0fe181f7b625f95810b07ab0"></a>

```sql
CREATE TABLE orders (
    order_id INT PRIMARY KEY,
    student_id INT,
    FOREIGN KEY (student_id) REFERENCES students(id)
);
```

<a id="fffeda9b0fe1813290efc6ba99a8561d"></a>

<strong>해석 </strong>&#58; orders 라는 이름의 테이블을 생성합니다&#46; 이 테이블에는 두 개의 열이 있습니다&#58;

- <code>order&#95;id</code>&#58; 정수형 데이터를 저장하는 열로, 이 열이 기본 키(<code>PRIMARY KEY</code>)입니다&#46; 즉, <code>orders</code> 테이블의 각 행을 고유하게 식별합니다&#46;

- <code>student&#95;id</code>&#58; 정수형 데이터를 저장하는 열로, <code>students</code> 테이블의 <code>id</code>를 참조하는 외래 키(<code>FOREIGN KEY</code>)입니다&#46; 이를 통해 <code>orders</code> 테이블의 각 주문이 어떤 학생과 관련이 있는지를 나타낼 수 있습니다&#46;

<a id="fffeda9b0fe181e4aabcedf3bb4dc2d7"></a>

## 4&#46; <strong>집계 함수(Aggregate Functions)</strong>

<a id="fffeda9b0fe181d6b4efc38d8833e9eb"></a>

집계 함수는 여러 행의 값을 계산하여 하나의 결과를 반환하는 함수입니다&#46;

- <strong>COUNT()</strong>&#58; 행의 개수를 셉니다&#46;
    <a id="fffeda9b0fe1814ca7ace7a4a3dec23b"></a>

    ```sql
    SELECT COUNT(*) FROM students;
    ```

- <strong>SUM()</strong>&#58; 숫자 값의 합을 계산합니다&#46;
    <a id="fffeda9b0fe18187859fc9a63c924204"></a>

    ```sql
    SELECT SUM(age) FROM students;
    ```

- <strong>AVG()</strong>&#58; 숫자 값의 평균을 계산합니다&#46;
    <a id="fffeda9b0fe181899924e6f936af447f"></a>

    ```sql
    SELECT AVG(age) FROM students;
    ```

- <strong>MAX()</strong>&#58; 최대 값을 찾습니다&#46;
    <a id="fffeda9b0fe1812f8874e1a96a3f33d2"></a>

    ```sql
    SELECT MAX(age) FROM students;
    ```

- <strong>MIN()</strong>&#58; 최소 값을 찾습니다&#46;
    <a id="fffeda9b0fe181e3bcccc4350bb2fbd5"></a>

    ```sql
    SELECT MIN(age) FROM students;
    ```

<a id="fffeda9b0fe181f8a38bc5eca7fd12d1"></a>

## 5&#46; <strong>SQL 조건문</strong>

- <strong>AND</strong>&#58; 두 조건이 모두 참일 때 사용합니다&#46;
    <a id="fffeda9b0fe1815c9d4af309dddeddb4"></a>

    ```sql
    SELECT * FROM students WHERE age > 20 AND name = 'Alice';
    ```

- <strong>OR</strong>&#58; 두 조건 중 하나만 참이면 사용합니다&#46;
    <a id="fffeda9b0fe181018b4ed3969f904adf"></a>

    ```sql
    SELECT * FROM students WHERE age > 20 OR name = 'Bob';
    ```

- <strong>NOT</strong>&#58; 조건이 거짓일 때 사용합니다&#46;
    <a id="fffeda9b0fe181ea8d6efc48fbb405d0"></a>

    ```sql
    SELECT * FROM students WHERE NOT age > 20;
    ```
