---
order: 5
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 289eda9b-0fe1-80b0-baf8-c0d2a60a1ffd
title: "[ 이론 ] Query Builder"
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 226eda9b-0fe1-802b-a035-c3a886768c4d
    title: Nest.js
  - id: 260eda9b-0fe1-801b-836b-c2e229a88ff9
    title: 한 번에 끝내는 NestJS 패키지 - Part 1. 기초
  - id: 274eda9b-0fe1-8023-ba05-d84527f93ae0
    title: DB ( SQL, TypeORM, QueryBuilder, Transaction, Migration )
  - id: 289eda9b-0fe1-80b0-baf8-c0d2a60a1ffd
    title: "[ 이론 ] Query Builder"
excerpt: 목차 - Query Builder - Query Builder - CRUD - Query Builder - 기본 문법 ( 추가 조건 ) Query Builder --- 📖 간단한 쿼리의 경우 Repository를 사용하는 것이 편리하고 유지보수 측면에서도 좋다. 그러나 복잡한 쿼리 및 동적 쿼리 작성이 필요한 경우 Qu
cover: null
icon: null
notionProperties: {}
schema_version: 1
parent_id: 274eda9b-0fe1-8023-ba05-d84527f93ae0
created: 2025-10-11T07:08:46.073Z
updated: 2025-10-12T05:22:25.131Z
legacy_path: Main/Nest.js-c3a886768c4d/한 번에 끝내는 NestJS 패키지 - Part 1. 기초-c2e229a88ff9/DB ( SQL, TypeORM, QueryBuilder, Transaction,-d84527f93ae0/[ 이론 ] Query Builder-c0d2a60a1ffd/index.md
legacy_category: Nest.js
source_url: https://beautiful-college-c84.notion.site/289eda9b0fe180b0baf8c0d2a60a1ffd
---
> 
> 
> <a id="289eda9b0fe1805ea96dccf7e4ff3737"></a>
> 
> <strong>목차</strong>
> 
> - [Query Builder](#289eda9b0fe180cba8c1e3d67043d2be)
> - [Query Builder - CRUD ](#275eda9b0fe180338b5defae1100e66d)
> - [ Query Builder -  기본 문법 ( 추가 조건 )](#275eda9b0fe180e38970e222d13a7e0a)

<a id="289eda9b0fe180cba8c1e3d67043d2be"></a>

## Query Builder

---

> 📖 
> 
> <a id="275eda9b0fe1803b95fdc6fa05929419"></a>
> 
> 간단한 쿼리의 경우 Repository를 사용하는 것이 편리하고 유지보수 측면에서도 좋다&#46;
> 
> <a id="275eda9b0fe180ef96beeb2d1cc4654f"></a>
> 
> 그러나 <strong><u>복잡한 쿼리 및 동적 쿼리</u></strong> 작성이 필요한 경우 <code>Query Builder</code> 사용을 권장한다&#46;
> 
> > SQL 과 거의 유사한 형태이며 <strong><u>체이닝 메서드 형태로 Query 작성</u></strong><strong>을 </strong>한다&#46;
> > 
> > - Query →  <a href="#/post/1c3eda9b-0fe1-8196-ad8d-e7a04eac7b77">페이지</a> 사용
> 
> <details>
> <summary>ex )</summary>
> 
> <a id="275eda9b0fe1800e9a26c88b8420be40"></a>
> 
> ```typescript
> const users = await userRepository.createQueryBuilder("user")
> 		.leftJoinAndSelect("user.profile", "profile")
> 		.where("user.isActive = :isActive", { isActive: true })
> 		.orderBy("user.firstName", "ASC")
> 		.skip(10)
> 		.take(5)
> 		.getMany();
> ```
> 
> </details>

<a id="275eda9b0fe180338b5defae1100e66d"></a>

### Query Builder &#45; CRUD 

> ✏️ 
> 
> <a id="275eda9b0fe180c8a6b1dce666d5c80d"></a>
> 
> 쿼리 빌더 생성
> 
> - <code>await domainRepository&#46;createQueryBuilder(…)&#46;getOne() or getMany()</code>
> 
> - <code>await dataSource&#46;createQueryBuilder(…)&#46;execute()</code>
> 
> - <code>await connections&#46;getRepository(…)&#46;createQueryBuilder(…)&#46;getOne() or getMany()</code>

<details>
<summary><strong>SELECT</strong></summary>

<a id="275eda9b0fe180e18e27cad9a5ec2e06"></a>

```typescript
const movie = await dataSource
		.createQueryBuilder()
		.select("movie")
		.from(Movie, "movie")
		.leftJoinAndSelect("movie.detail", "detail")
		.leftJoinAndSelect("movie.director", "director")
		.leftJoinAndSelect("movie.genres", "genres")
		.where("movie.id = :id", { id: 1 })
		.getOne();
```

</details>

<details>
<summary><strong>INSERT</strong></summary>

<a id="275eda9b0fe180619e85c480c6a05edb"></a>

```typescript
await dataSource
		.createQueryBuilder()
		.insert()
		.into(Movie)
		.values([
			{
				title: "New Movie",
				genre: "Action",
				director: "director,
				genres: genres
			}
		])
		.execute();
```

</details>

<details>
<summary><strong>UPDATE</strong></summary>

<a id="275eda9b0fe18033abb3ca25b8e90221"></a>

```typescript
await dataSource
		.createQueryBuilder()
		.update(Movie)
		.set({ title: "Updated Title", genre: "Drama" })
		.where("id = :id", { id: 1 })
		.execute();
```

</details>

<details>
<summary><strong>DELETE</strong></summary>

<a id="275eda9b0fe1808090a0cd434fbd7b40"></a>

```typescript
await dataSource
		.createQueryBuilder()
		.delete()
		.from(Movie)
		.where("id = :id", { id: 1 })
		.execute();
```

</details>

<details>
<summary><strong>RELATIONS</strong></summary>

- ex)  movie id가 1인 여러 장르 데이터 조회
    <details>
    <summary>아래 relation 예제외  동일</summary>

    <a id="289eda9b0fe180f8bebef545f61b6b75"></a>

    ```typescript
    const genres = await dataSource
      .getRepository(Genre)
      .createQueryBuilder("g")
      .innerJoin("g.movies", "m", "m.id = :id", { id: 1 })
      .getMany();

    SELECT g.*
    FROM "genre" g
    INNER JOIN "movie_genres" mg ON mg."genre_id" = g."id"
    WHERE mg."movie_id" = 1;
    ```

    </details>

    <a id="275eda9b0fe180008a5ad742e5fd8dbf"></a>

    ```typescript
    const genres = await dataSource
    		.createQueryBuilder()
    		.relation(Movie, "genres")
    		.of(1)  // Movie id
    		.loadMany();
    ```

    - <code>add()</code>, <code>remove()</code>  사용 시 해당 데이터를 추가로 조작 가능하다&#46;

</details>

<a id="275eda9b0fe180e38970e222d13a7e0a"></a>

###  Query Builder &#45;  기본 문법 ( 추가 조건 )

<details>
<summary><strong>단일, 다수 &#45; </strong><strong><code>getOne()</code></strong><strong>, </strong><strong><code>getMany()</code></strong><strong> &#91; 조회&#58; Select &#93;</strong></summary>

> ✏️ 
> 
> - 1개의 Row(데이터) 조회&#58; <code>getOne()</code>
> 
> - 다수의 Row(데이터) 조회&#58; <code>getMany()</code>

- 단일 Row 조회&#58; <strong><code>getOne()</code></strong>
    <a id="275eda9b0fe1802fa872e3838be60a36"></a>

    ```typescript
    const users = await connection.getRepository(User)
    		.createQueryBuilder("user")
    		.select(["user.id", "user.firstName", "user.lastName"])
    		.getOne();
    ```

- 복수 Row 조회&#58; <strong><code>getMany()</code></strong>
    <a id="275eda9b0fe18017b7d6e4be132e4edf"></a>

    ```typescript
    const users = await connection.getRepository(User)
    		.createQueryBuilder("user")
    		.select(["user.id", "user.firstName", "user.lastName"])
    		.getMany();
    ```

</details>

<details>
<summary><strong>필터링 &#45; </strong><strong><code>where()</code></strong><strong> </strong></summary>

> ✏️ 
> 
> 1. 단일 조건을 필터링할 경우 <code>where()</code> 함수 사용
> 
> 1. 다수의 조건을 필터링할 경우
>     - 동일하게 <code>where()</code>로 필터링하며
> 
>     - 이후 <code>addWhere()</code>를 필터링 조건을 추가한다&#46; 

- 하나의 필터링 조건 적용
    <a id="275eda9b0fe1808c8005e59c8aa3142a"></a>

    ```typescript
    const users = await connection.getRepository(User)
    		.createQueryBuilder("user")
    		.where("user.isActive = :isActive", { isActive: true })
    		.getMany();
    ```

- 다수의 필터링 조건 적용
    <a id="275eda9b0fe180079e63c6f7dac8359b"></a>

    ```typescript
    const users = await connection.getRepository(User)
    		.createQueryBuilder("user")
    		.where("user.firstName = :firstName", { isActive: "John" })
    		.andWhere("user.lastName = :lastName", { isActive: "Doe" })
    		.getMany();
    ```

</details>

<details>
<summary><strong>정렬 &#45; </strong><strong><code>orderBy()</code></strong><strong> </strong></summary>

> ✏️ 
> 
> 1. 단일 정렬 조건을 적용하는 경우 <code>orderBy()</code> 를 사용하여 <strong><u>조건 컬럼, 정렬 순서(ASC, DESC)</u></strong><strong> </strong>를 정의한다,
> 
> 1. 이후 정렬 조건을 추가하는 경우, <code>addOrderBy()</code>를 사용하여 추가한다&#46;

- 다수의 정렬 조건 적용
    <a id="275eda9b0fe180a091e6e1d35acc79fb"></a>

    ```typescript
    const users = await connection.getRepository(User)
    		.createQueryBuilder("user")
    		.orderBy("user.lastName", "ASC")
    		.addOrderBy("user.firstName:", "DESC")
    		.getMany();
    ```

</details>

<details>
<summary><strong>페이징 &#45; </strong><strong><code>skip()</code></strong><strong>, </strong><strong><code>take()</code></strong></summary>

> ✏️ 
> 
> <a id="275eda9b0fe1808fa32fc8c6781a8ee8"></a>
> 
> <strong><code>Pagination</code></strong>에서의 <code>LIMIT</code>, <strong><code>OFFSET</code></strong> 과 동일
> 
> - <code>skip</code>&#58;  <code>offset</code>, 즉 skip할 이전 페이지 데이터  ( <code>(page &#45; 1) &#42; size</code> )
> 
> - <code>take</code>&#58; <code>limit</code> 즉, 가져오는 데이터 크기를 지정

- ex) page&#58; 3, size&#58; 5
    <a id="275eda9b0fe180419648e32c3cb35ca3"></a>

    ```typescript
    const users = await connection.getRepository(User)
    		.createQueryBuilder("user")
    		.skip(10)
    		.take(5)
    		.getMany();
    ```

</details>

<details>
<summary><strong>조인 &#45; </strong><strong><code>join()</code></strong></summary>

> ✏️ 
> 
> - <strong>Inner Join&#58; </strong><strong><code>innerJoinAndSelect(&#46;&#46;&#46;)</code></strong>
> 
> - <strong>Left Join&#58; </strong><strong><code>leftJoinAndSelect(…)</code></strong> 
> 
> - <strong>Right Join&#58; </strong><strong><code>rightJoinAndSelect(…)</code></strong> 

- Inner Join
    <a id="275eda9b0fe18098b496f5a13faaea8c"></a>

    ```typescript
    const users = await connection.getRepository(User)
    		.createQueryBuilder("user")
    		.innerJoinAndSelect("user.profile", "profile")
    		.getMany();
    ```

- Left Join
    <a id="275eda9b0fe180a59d3ef8d3937bb344"></a>

    ```typescript
    const users = await connection.getRepository(User)
    		.createQueryBuilder("user")
    		.leftJoinAndSelect("user.photo", "photo")
    		.getMany();
    ```

- Right Join
    <a id="289eda9b0fe180dfbcabd18b8d7843c9"></a>

    ```typescript
    const users = await connection.getRepository(User)
    		.createQueryBuilder("user")
    		.rightJoinAndSelect("user.photo", "photo")
    		.getMany();
    ```

</details>

<details>
<summary>Aggregation ( 통계 ) &#45; <code>select(”COUNT(&#46;&#46;&#46;)&#34;,  “count”)</code></summary>

> ✏️ 
> 
> <a id="275eda9b0fe18004bb43fd7e27c48181"></a>
> 
> SQL 과 유사하게 select 컬럼에 적용

- <code>COUNT()</code>
    <a id="275eda9b0fe18029a4f7f583b9455894"></a>

    ```typescript
    const users = await connection.getRepository(User)
    		.createQueryBuilder("user")
    		.select("COUNT(user.id)", "count")
    		.getRawOne();
    ```

</details>

<details>
<summary><strong>Sub Query ( 서브 쿼리 )</strong></summary>

> ✏️ 
> 
> <a id="275eda9b0fe180eca0e7c168c523eba9"></a>
> 
> <code>where()</code> 함수 내부에 <strong><u>callback 형태로 정의</u></strong>한다&#46;
> 
> - <code>subQuery()</code> 메서드 및 체이닝 방식으로 Sub Query 정의

<a id="275eda9b0fe18060ad12dea4d06dd897"></a>

```typescript
const users = await connection.getRepository(User)
		.createQueryBuilder("user")
		.where(qb => {
			const subQuery = qb.subQuery()
				.select("subUser.id")
				.from(User, "subUser")
				.where("subUser.isActive = :isActive", { isActive: true })
				.getQuery();
			return "user.id IN " + subQuery;
		})
		.setParameter("isActive", true)
		.getMany();
```

</details>
