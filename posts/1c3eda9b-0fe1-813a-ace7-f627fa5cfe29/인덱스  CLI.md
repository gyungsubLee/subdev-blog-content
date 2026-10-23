---
order: 11
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 1c3eda9b-0fe1-813a-ace7-f627fa5cfe29
title: 인덱스  CLI
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 1c3eda9b-0fe1-8114-a6f8-e8c2debc9fa0
    title: DBMS
  - id: 1c3eda9b-0fe1-81ef-9506-cdc300921ef3
    title: MySQL
  - id: 1c3eda9b-0fe1-813a-ace7-f627fa5cfe29
    title: 인덱스  CLI
excerpt: 페이지 0.1. 테이블 인덱스 적용 확인 sql SHOW INDEX FROM {테이블명}; ex) SHOW INDEX FROM article; 0.2. 인덱스 삭제 sql DROP INDEX {인덱스명} ex) DROP INDEX idxusersemail; 1. 기본 인덱스 (B-Tree Index) 생성 기본적으로 자주
cover: null
icon: null
notionProperties:
  상태: 완료
schema_version: 1
parent_id: 1c3eda9b-0fe1-81ef-9506-cdc300921ef3
created: 2025-03-27T07:47:52.775Z
updated: 2025-03-27T07:47:52.775Z
legacy_path: Main/DBMS-e8c2debc9fa0/MySQL-cdc300921ef3/인덱스  CLI-f627fa5cfe29/index.md
legacy_category: DBMS
source_url: https://beautiful-college-c84.notion.site/1c3eda9b0fe1813aace7f627fa5cfe29
---
<a id="1c3eda9b0fe1812faeb5cf453b9c0c48"></a>

<a href="#/post/1c3eda9b-0fe1-8107-a9c0-ecb1f77d962a">페이지</a> 

<a id="1c3eda9b0fe181ad8c33fd2a13ab4da9"></a>

### 0&#46;1&#46; 테이블 인덱스 적용 확인

<a id="1c3eda9b0fe181508398f641c1643edc"></a>

```sql
SHOW INDEX FROM {테이블명};

# ex)
SHOW INDEX FROM article;
```

<a id="1c3eda9b0fe18141aa8be8f40c4d64f8"></a>

### <strong>0&#46;2&#46; 인덱스 삭제</strong>

<a id="1c3eda9b0fe18198aceac19e1068a9f2"></a>

```sql
DROP INDEX {인덱스명}

# ex)
DROP INDEX idx_users_email;
```

<a id="1c3eda9b0fe181269a9de2208ca4a705"></a>

### <strong>1&#46; 기본 인덱스 (B&#45;Tree Index) 생성</strong>

> 기본적으로 자주 검색되는 컬럼에 인덱스를 생성할 때 사용

<a id="1c3eda9b0fe18107a3dfee41ded90d80"></a>

```sql
CREATE INDEX {인덱스명} ON 테이블(기준키(컬럼));

# ex)
CREATE INDEX idx_users_email 
ON users(email);
```

- users 테이블의 email 컬럼에 인덱스 생성

- 기준 컬럼을 조회 조건으로 사용 시, 조회 성능이 향상됨
    - <code>WHERE email = &#39;test&#64;example&#46;com&#39;</code> 같은 조회 시 성능 향상

<a id="1c3eda9b0fe1810b8c63e0df143790e8"></a>

### 2&#46; <strong>UNIQUE 인덱스</strong>

> 중복을 허용하지 않는 유니크 인덱스 생성

<a id="1c3eda9b0fe181088872e02cac8d7d23"></a>

```sql
CREATE UNIQUE INDEX idx_users_username 
ON users(username);
```

- users 테이블의 username 컬럼에 중복되지 않는 유니크 인덱스 적용

- UNIQUE CONSTRAINT와 같은 역할을 하지만 인덱스 형태로 관리됨

<a id="1c3eda9b0fe181a083fac20b975e64e1"></a>

### 3&#46; <strong>복합(Composite) 인덱스</strong>

> 두 개 이상의 컬럼에 대한 검색을 최적화할 때 사용

<a id="1c3eda9b0fe1816da62ac9b2c1c77f1c"></a>

```sql
CREATE INDEX {인덱스명} ON 테이블명{기준키1, 기준키2 ...}

# ex) 
CREATE INDEX idx_orders_customer_date 
ON orders(customer_id, order_date);
```

- 적용된 복합키를 함께 조회하는 경우, 조회 속도가 향상됨
    - <code>WHERE customer&#95;id = ? AND order&#95;date = ?</code> 조건을 자주 사용할 때 유리

<a id="1c3eda9b0fe1817ba16ae2b505a17b97"></a>

### <strong>4&#46; FULLTEXT 인덱스 (MySQL 전용)</strong>

> 텍스트 검색 최적화를 위해 사용

<a id="1c3eda9b0fe18139923ffdea1416fd57"></a>

```sql
CREATE FULLTEXT INDEX idx_posts_content ON posts(content);
```

- MATCH(content) AGAINST(&#39;keyword&#39;) 같은 검색에서 성능이 좋아짐

<a id="1c3eda9b0fe181b68187f1beedf58dd1"></a>

### <strong>5&#46; HASH 인덱스 (PostgreSQL 예시)</strong>

> 빠른 조회를 위해 해시 기반 인덱스를 사용 가능

<a id="1c3eda9b0fe1811dbbe7fabd4e3a1c7c"></a>

```sql
CREATE INDEX idx_users_hash_email ON users USING HASH (email);
```

- <code>=</code> 연산(정확한 값 비교)에 최적화되어 있음&#46;

- 범위 검색 (BETWEEN, &#60;, &#62;)에는 적합하지 않음

<a id="1c3eda9b0fe1817cb805cbd72b33447e"></a>

### <strong>6&#46; GiST 인덱스 (PostgreSQL 전용, 공간 검색)</strong>

> 지리 데이터 검색 최적화를 위해 사용

<a id="1c3eda9b0fe1814d8827d17e837aa161"></a>

```sql
CREATE INDEX idx_locations_geom ON locations USING GIST (geom);
```

- 공간 데이터(geometry, geography)를 빠르게 검색할 때 유리함&#46;

<a id="1c3eda9b0fe18160aa57ec614c3a9ad0"></a>

### <strong>7&#46; CLUSTERED / NONCLUSTERED 인덱스 (SQL Server 예시)</strong>

- <strong>① 클러스터형 인덱스</strong>
    > 데이터 자체가 인덱스 정렬 순서대로 저장됨

    <a id="1c3eda9b0fe18109b125d67b3ca4ef15"></a>

    ```sql
    CREATE CLUSTERED INDEX idx_users_id ON users(id);
    ```

    - 테이블의 기본 정렬 순서를 id 기준으로 변경

- <strong>② 비클러스터형 인덱스</strong>
    > 기본 데이터와 분리된 인덱스 구조를 가짐&#46;

    <a id="1c3eda9b0fe1811a817df8c2fc1abbcc"></a>

    ```sql
    CREATE NONCLUSTERED INDEX idx_users_name ON users(name);
    ```

    - 데이터 정렬에는 영향을 주지 않고 검색 속도만 향상시킴

<a id="1c3eda9b0fe181df8d49dcdb57c7dfa2"></a>

###
