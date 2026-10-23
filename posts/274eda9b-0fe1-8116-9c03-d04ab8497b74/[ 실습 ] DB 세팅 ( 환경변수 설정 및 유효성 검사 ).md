---
order: 7
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 274eda9b-0fe1-8116-9c03-d04ab8497b74
title: "[ 실습 ] DB 세팅 ( 환경변수 설정 및 유효성 검사 )"
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 226eda9b-0fe1-802b-a035-c3a886768c4d
    title: Nest.js
  - id: 260eda9b-0fe1-801b-836b-c2e229a88ff9
    title: 한 번에 끝내는 NestJS 패키지 - Part 1. 기초
  - id: 274eda9b-0fe1-8023-ba05-d84527f93ae0
    title: DB ( SQL, TypeORM, QueryBuilder, Transaction, Migration )
  - id: 274eda9b-0fe1-8116-9c03-d04ab8497b74
    title: "[ 실습 ] DB 세팅 ( 환경변수 설정 및 유효성 검사 )"
excerpt: "목차 - DB 세팅 ( 환경변수 설정 및 유효성 검사 ) - 1. 의존성 설치 - 2. DB 연동 - 3. 환경변수 처리 - 4. 환경변수 유효성 검사 - 5. 비동기로 TypeOrmModule 등록 DB 세팅 ( 환경변수 설정 및 유효성 검사 ) --- 1. 의존성 설치 ✏️ - @nestjs/config, joi: N"
cover: null
icon: null
notionProperties: {}
schema_version: 1
parent_id: 274eda9b-0fe1-8023-ba05-d84527f93ae0
created: 2025-09-20T04:08:15.787Z
updated: 2025-09-27T09:16:01.776Z
legacy_path: Main/Nest.js-c3a886768c4d/한 번에 끝내는 NestJS 패키지 - Part 1. 기초-c2e229a88ff9/DB ( SQL, TypeORM, QueryBuilder, Transaction,-d84527f93ae0/[ 실습 ] DB 세팅 ( 환경변수 설정 및 유효성 검사 )-d04ab8497b74/index.md
legacy_category: Nest.js
source_url: https://beautiful-college-c84.notion.site/274eda9b0fe181169c03d04ab8497b74
---
> 
> 
> <a id="274eda9b0fe18194afd5e8546a4a1434"></a>
> 
> <strong>목차</strong>
> 
> - [DB 세팅 ( 환경변수 설정 및 유효성 검사 )](#274eda9b0fe1811dae71d7c443baf55d)
> - [1. 의존성 설치 ](#274eda9b0fe18128b4f5c09b3cdf191d)
> - [2. DB 연동](#274eda9b0fe1811d99d1c0dbe0b4df79)
> - [3.  환경변수 처리](#27beda9b0fe180c9b6f3e71f4625748e)
> - [4.  환경변수 유효성 검사](#27beda9b0fe180a6b6e0ca9f53f173fd)
> - [5. 비동기로 TypeOrmModule 등록](#27beda9b0fe1804b9870c6de14ea807f)

<a id="274eda9b0fe1811dae71d7c443baf55d"></a>

## DB 세팅 ( 환경변수 설정 및 유효성 검사 )

---

<a id="274eda9b0fe18128b4f5c09b3cdf191d"></a>

### 1&#46; 의존성 설치 

> ✏️ 
> 
> - <code>&#64;nestjs/config</code>, <code>joi</code>&#58; NestJS 환경변수 설정
> 
> - <code>&#64;nestjs/typeorm</code>&#58; NestJS typeorm 
> 
> - <code>pg</code>&#58; postgreSQL 연동을 위한 모듈

<details>
<summary><code>&#64;nestjs/config</code>, <code>joi</code>, <code>&#64;nestjs/typeorm</code>, <code>pg</code></summary>

<a id="274eda9b0fe1817fba4dc4658e212fc6"></a>

```typescript
pnpm i @nestjs/config joi @nestjs/typeorm typeorm pg
```

</details>

<a id="274eda9b0fe1811d99d1c0dbe0b4df79"></a>

### 2&#46; DB 연동

> ❗ 
> 
> <a id="27beda9b0fe180fb8167e2816ddd9dde"></a>
> 
> <strong>&#91; 주의 &#93; 옵션 </strong><strong><code>synchronize</code></strong>
> 
> <a id="27beda9b0fe180159ab1e0b0a8c6f9d8"></a>
> 
> <code>synchronize&#58; true</code> 시 코드와 맞게 데이터베이스 싱크를 맞춘다&#46; 
> 
> <a id="27beda9b0fe18042adf1c12fcdd3f20c"></a>
> 
> 따라서 <strong>실제 프로덕션(운영) 상황의 경우 </strong><strong><u>DB의 데이터가 날아갈 수 있</u></strong><strong>다&#46;</strong>
> 
> <a id="27beda9b0fe180f99eb2d34e4afe1362"></a>
> 
> 그러므로 <strong><u>프로덕션(운영) 상황에서는 무조건 </u></strong><strong><u><code>false</code></u></strong><strong><u>로 설정</u></strong>해야 한다&#46; 
> 
> - <strong>&#91;권장&#93; 환경변수로 dev 설정 시만 true 값이 되도록 세팅</strong>

> ✅ 
> 
> <a id="27beda9b0fe180fbac03df8da7f9b822"></a>
> 
> 일반적으로 데이터베이스의 싱크를 맞추는 즉, 상태를 변경하는 방식은 마이그레이션을 통해서 진행한다&#46;  ( 이후 학습 진행, 링크 추가하기 )

<details>
<summary>1&#46;  DB 연동 ( 기본 )</summary>

<a id="274eda9b0fe181ef8fdcfc06b637a04f"></a>

```typescript
import { Module } from '@nestjs/common';
import { TypeOrmMoudle } from '@nestjs/typeorm';
import { MovieModule } from './movie/movie.module';

@Module({
	imports: [
		TypeOrmModule.forRoot({
			type: "postgres",
			hosts: "localhost",
			port: 5555,
			username: "postgres",
			password: "postgres",
			database: "postgres",
			entities: [],
			synchronize: true,  // 주의
		}),
		MoviceModule
	]
})
export class AppModule {}
```

</details>

<a id="27beda9b0fe180c9b6f3e71f4625748e"></a>

### 3&#46;  환경변수 처리

<details>
<summary><code>&#46;env</code> 파일 생성 및 환경변수 정의</summary>

> ✏️ 
> 
> <a id="27beda9b0fe180a7aeaae25ebdf11ae1"></a>
> 
> <code>&#46;env</code> 명칭이 아니어도 상관없으나, 자동으로 인지되는 네이밍은 &#46;<code>env</code> 이다&#46; 

<a id="27beda9b0fe18073bb99ff44921b6b86"></a>

```bash
# 개발환경 { dev: 개발 환경, prod: 베포 환경 }
ENV=dev

# DB
DB_TYPE=postgres
DB_HOST=localhost
DB_PORT=5555
DB_USERNAME=postgres
DB_PASSWORD=postgres
DB_DATABASE=postgres
```

</details>

<details>
<summary>환경변수 적용</summary>

<a id="27beda9b0fe1801ab1fec096e07558b0"></a>

```typescript
import { Module } from '@nestjs/common';
import { TypeOrmMoudle } from '@nestjs/typeorm';
import { ConfigModule } from '@nestjs/config';
import { MovieModule } from './movie/movie.module';

@Module({
	imports: [
		ConfigModule.forRoot(),
		TypeOrmModule.forRoot({
			type: process.env.DB_TYPE as "postgres",
			hosts: process.env.DB_HOST, 
			port: parseInt(process.env.DB_PORT),
			username: process.env.DB_USERNAME,
			password: process.env.DB_PASSWORD,
			database: process.env.DB_DATABASE,
			entities: [],
			synchronize: true,
		}),
		MoviceModule
	]
})
export class AppModule {}
```

</details>

<a id="27beda9b0fe180a6b6e0ca9f53f173fd"></a>

### 4&#46;  환경변수 유효성 검사

> 📖 
> 
> <a id="27beda9b0fe1808ba459e1232ead6c38"></a>
> 
> 환경변수 값에 대해서<strong><u> 유효성검사(validation)</u></strong>을 진행하는 것은 매우 중요하다&#46; 
> 
> <a id="27beda9b0fe1805ab177d7176a2393e1"></a>
> 
> 이를 <code>Joi</code> 라이브러를 통해 진행한다&#46;
> 
> - 오류를 던지지 않는 환경변수 값들도 있기 때문에 디버깅이 매우 번거롭다&#46;

<details>
<summary><code>Joi</code>를 사용한 스키마 validation 처리</summary>

> ✏️ 
> 
> <a id="27beda9b0fe1802b99fef11cf056e106"></a>
> 
> <code>ConfigModule</code>에 <code>isGlobal&#58; true</code> 설정 시 환경변수를 global 하게 선언하여 어떤 모듈에서든 가져와 사용할 수 있다&#46; 

<a id="27beda9b0fe180a1ba87e6038dfc7d8a"></a>

```typescript
import { Module } from '@nestjs/common';
import { TypeOrmMoudle } from '@nestjs/typeorm';
import { ConfigModule } from '@nestjs/config';
import { MovieModule } from './movie/movie.module';
import * as Joi from 'joi';

@Module({
	imports: [
		ConfigModule.forRoot({
			isGlobal: true,
			validationSchema: Joi.object({
				ENV: Joi.string().required(),
				DB_TYPE: Joi.string().required(),
				DB_HOST: Joi.string().required(),
				DB_PORT: Joi.number().required(),
				DB_USERNAME: Joi.string().required(),
				DB_PASSWORD: Joi.string().required(),
				DB_DATABASE: Joi.string().required()
			}),
		}),
		TypeOrmModule.forRoot({
			type: process.env.DB_TYPE as "postgres",
			hosts: process.env.DB_HOST, 
			port: parseInt(process.env.DB_PORT),
			username: process.env.DB_USERNAME,
			password: process.env.DB_PASSWORD,
			database: process.env.DB_DATABASE,
			entities: [],
			synchronize: true,
		}),
		MoviceModule
	]
})
export class AppModule {}
```

</details>

<details>
<summary>실습1)  변수 검증</summary>

- 환경변수 설정 시 오타 발생
    <a id="27beda9b0fe18032b362f9068ba67c55"></a>

    ```bash
    # 개발환경 { dev: 개발 환경, prod: 베포 환경 }
    ENV=dev

    # DB
    DB_TYPE=postgres
    DB_HOST=localhost
    DB_PORT=5555
    DB_USERNAME=postgres
    DB_PASSWORD=postgres
    DB_DATABAS=postgres # 변수 오타
    ```

- 아래와 같이 런타임 환경에서 오류 체크 가능하다&#46;
    ![](736dd1fd0c0e0bad.webp)

</details>

<details>
<summary>실습2)  값 검증 &#45; <code>&#46;valid(값)</code> </summary>

- Joi로 특정 값 검증
    <a id="27beda9b0fe180dd948bec32b3a1a1e4"></a>

    ```typescript
    import { Module } from '@nestjs/common';
    import { TypeOrmMoudle } from '@nestjs/typeorm';
    import { ConfigModule } from '@nestjs/config';
    import { MovieModule } from './movie/movie.module';
    import * as Joi from 'joi';

    @Module({
    	imports: [
    		ConfigModule.forRoot({
    			isGlobal: true,
    			validationSchema: Joi.object({
    				ENV: Joi.string().required(),
    				DB_TYPE: Joi.string().valid('postgress').required(),
    				DB_HOST: Joi.string().required(),
    				DB_PORT: Joi.number().required(),
    				DB_USERNAME: Joi.string().required(),
    				DB_PASSWORD: Joi.string().required(),
    				DB_DATABASE: Joi.string().required()
    			}),
    		}),
    			. . .
    	]
    })
    export class AppModule {}
    ```

- 환경변수 설정 시 다른 타입의 DB로 세팅
    <a id="27beda9b0fe18084af69cbf44eaa4c13"></a>

    ```bash
    # 개발환경 { dev: 개발 환경, prod: 베포 환경 }
    ENV=dev

    # DB
    DB_TYPE=mysql # 다른 DB 타입으로 세팅
    DB_HOST=localhost
    DB_PORT=5555
    DB_USERNAME=postgres
    DB_PASSWORD=postgres
    DB_DATABASE=postgres
    ```

- 아래와 같이 런타임 환경에서 오류 체크 가능하다&#46;
    ![](c2f7b8aa737e57f6.webp)

</details>

<a id="27beda9b0fe1804b9870c6de14ea807f"></a>

### 5&#46; <strong><u>비동기</u></strong>로 <code>TypeOrmModule</code> 등록

> 📖 
> 
> <a id="27beda9b0fe1804f8b1ce47d5882e720"></a>
> 
> <code>TypeORM 인스턴스</code>를 <u><code>ConfigModule</code></u><strong><u> 환경변수 기반으로 생성</u></strong>하려면, <strong><u>NestJS의 DI 시스템</u></strong>을 통해 <code>ConfigModule(ConfigService)</code>이 주입되어야 한다&#46;
> 
> <a id="27beda9b0fe1809bbb3dced7da531190"></a>
> 
> 즉, <strong><u> IoC 컨테이너가 초기화가 이뤄지고 난 후</u></strong> DI를 통해 <u><code>ConfigModule(ConfigService)</code></u><strong><u>를 주입 받</u></strong>는다&#46;  따라서 이를 기다리기 위해<strong><u> 비동기 방식(</u></strong><strong><u><code>forRootAsync</code></u></strong><strong><u>)으로 </u></strong><strong><u><code>TypeOrmModule</code></u></strong><strong><u> 인스턴스를 생성</u></strong>한다&#46; 

> ✏️ 
> 
> <a id="27beda9b0fe18051b7dcf9ab254ee3f4"></a>
> 
> <strong>IoC와 ConfigService의 주입 및 TypeOrm 비동기 생성 과정</strong>
> 
> 1. NestJS는 <strong><u>IoC 컨테이너</u></strong>를 활용해 <code>ConfigModule</code>을 먼저 등록하고, <code>ConfigService</code>를 DI로 제공한다&#46;
> 
> 1. <code>TypeOrmModule&#46;forRootAsync</code>는 <strong><u>비동기 팩토리(useFactory</u></strong>)를 이용해 <code>ConfigService</code>를 inject받으며, <code>ConfigService</code>를 통해 <strong><u>환경변수를 동적으로 처리</u></strong>한다&#46;
> 
> 1. <code>ConfigService</code>의 <strong><u>초기화가 완료되어야 데이터베이스 환경변수 값을 안전하게 읽</u></strong>을 수 있기 때문에, <code>TypeOrmModule</code>은 <code>forRootAsync</code>를 사용하여 <strong><u>DI 대상의 초기화를 비동기로 기다린다&#46;</u></strong>

<details>
<summary>TypeOrmModule 비동기로 등록 &#45; <code>forRootAsync</code>, <code>useFactory</code></summary>

> ✏️ 
> 
> <a id="27beda9b0fe180f7a196f3781bc77f51"></a>
> 
> <code>ConfigModule</code>이 IoC 컨테이너에 등록되고 Injection 시 <code>ConfigService</code>로 주입된다&#46; 

<a id="27beda9b0fe18091bc77e49fab197c9d"></a>

```typescript
import { Module } from '@nestjs/common';
import { TypeOrmMoudle } from '@nestjs/typeorm';
import { ConfigModule } from '@nestjs/config';
import { MovieModule } from './movie/movie.module';
import * as Joi from 'joi';

@Module({
	imports: [
		ConfigModule.forRoot({
			isGlobal: true,
			validationSchema: Joi.object({
				ENV: Joi.string().required(),
				DB_TYPE: Joi.string().required(),
				DB_HOST: Joi.string().required(),
				DB_PORT: Joi.number().required(),
				DB_USERNAME: Joi.string().required(),
				DB_PASSWORD: Joi.string().required(),
				DB_DATABASE: Joi.string().required()
			}),
		}),
		TypeOrmModule.forRootAsync({
			useFactory: async (config: ConfigService) => ({
				type: config.get<string>('DB_TYPE') as "postgres",
				hosts: config.get<string>('DB_HOST'), 
				port: config.get<number>('DB_PORT'),
				username: config.get<string>('DB_USERNAME'),
				password: config.get('DB_PASSWORD'),
				database: config.get('DB_DATABASE'),
				entities: [],
				synchronize: true,
			}),
			inject: [ConfigService],
		}),
		MoviceModule
	]
})
export class AppModule {}
```

</details>
