---
order: 6
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 22deda9b-0fe1-80bc-9069-ef853ac5fbf0
title: "기본 세팅: Nest 프로젝트 및  MongoDB 설정"
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 226eda9b-0fe1-802b-a035-c3a886768c4d
    title: Nest.js
  - id: 227eda9b-0fe1-80e1-8036-d4fc3e106054
    title: 탄탄한 백엔드 NestJS, 기초부터 심화까지 ( 중지 )
  - id: 22deda9b-0fe1-80bc-9069-ef853ac5fbf0
    title: "기본 세팅: Nest 프로젝트 및  MongoDB 설정"
excerpt: "목차 - 1. Nest 프로젝트 init - 2. MongoDB 세팅 - Mongoose - 3. Mongoose Docs 1. Nest 프로젝트 init 페이지 bash nest new . 2. MongoDB 세팅 - Mongoose [Documentation | NestJS - A progressive Node.js "
cover: 5ff6372aa1146e10.jpg
icon: ⚙
notionProperties: {}
schema_version: 1
parent_id: 227eda9b-0fe1-80e1-8036-d4fc3e106054
created: 2025-07-11T08:45:11.982Z
updated: 2025-08-15T06:48:31.003Z
legacy_path: Main/Nest.js-c3a886768c4d/탄탄한 백엔드 NestJS, 기초부터 심화까지 ( 중지 )-d4fc3e106054/기본 세팅- Nest 프로젝트 및  MongoDB 설정-ef853ac5fbf0/index.md
legacy_category: Nest.js
source_url: https://beautiful-college-c84.notion.site/22deda9b0fe180bc9069ef853ac5fbf0
---
> 
> 
> <a id="22deda9b0fe1801bada3cacb3cba44f9"></a>
> 
> <strong>목차</strong>
> 
> - [1. Nest 프로젝트 init](#22deda9b0fe1801fb50dc70c097b977b)
> - [2.  MongoDB 세팅 - Mongoose](#22deda9b0fe180958641ef5123f00cd7)
> - [3. Mongoose Docs](#22deda9b0fe18018a2f6cd936531a871)

<a id="22deda9b0fe1801fb50dc70c097b977b"></a>

### 1&#46; Nest 프로젝트 init

> <a href="#/post/22aeda9b-0fe1-8068-87b8-d9c3327f1247">페이지</a>

<a id="22deda9b0fe180baaa4cd70892ddda99"></a>

```bash
nest new .
```

<a id="22deda9b0fe180958641ef5123f00cd7"></a>

### 2&#46;  MongoDB 세팅 &#45; Mongoose

[Documentation &#124; NestJS &#45; A progressive Node&#46;js framework]()

<details>
<summary><strong>1&#46; mongoose 설치</strong></summary>

<a id="22deda9b0fe180c88ab1e192888c7c12"></a>

```bash
npm i @nestjs/mongoose mongoose
```

</details>

<details>
<summary><strong>2&#46; 로컬에서 MongoDB 서버 띄위기</strong></summary>

- doccker CLI
    <a id="22deda9b0fe1803ba15df5e974811215"></a>

    ```bash
    docker run -d \
      --name mongo \
      -p 27017:27017 \
      -e MONGO_INITDB_ROOT_USERNAME=admin \
      -e MONGO_INITDB_ROOT_PASSWORD=admin123 \
      mongo:latest
    ```

- docker compose
    <a id="22eeda9b0fe18007a631f792d32f6e9b"></a>

    ```yaml
    services:
      db:
        container_name: mongo
        image: mongo:latest
        ports:
          - '27017:27017'
        environment:
          - MONGO_INITDB_ROOT_USERNAME=admin
          - MONGO_INITDB_ROOT_PASSWORD=admin123
        volumes:
          - db_data:/data/db
    volumes:
      db_data:
    ```

</details>

<details>
<summary><strong>3&#46; DB 연결</strong></summary>

<details>
<summary>환경 변수 설정 전</summary>

<a id="22deda9b0fe180e78da1ee24f97025e9"></a>

<strong>app&#46;module&#46;ts</strong>

<a id="22deda9b0fe180bd9828fb1e61e5e0c4"></a>

```typescript
import { Module } from '@nestjs/common';
import { MongooseModule } from '@nestjs/mongoose';

@Module({
  imports: [
	  MongooseModule.forRoot('mongodb://localhost/nest')
  ],
})
export class AppModule {}
```

<a id="22deda9b0fe180419852f91e54254790"></a>

<strong><br>MongoDB 연결 URI</strong>

<a id="22deda9b0fe180ef9aedc9009f1b304d"></a>

```bash
MongooseModule.forRoot('mongodb://admin:admin123@localhost:27017/nest?authSource=admin')
```

- 인증 ( <code>사용자ID&#58;비밀번호</code> )&#58; <code>admin&#58;admin12</code>

- MongoDB 호스트/포트&#58; <code>localhost&#58;27017</code>

- 사용할 DB 이름 ( 없으면 자동 생성 )&#58; <code>/nest</code>

- 인증을 진행할 <strong>DB 이름</strong>&#58; <code>authSource=admin</code>

</details>

> ✏️ 
> 
> <a id="22deda9b0fe180b8a57bc5f7b917695d"></a>
> 
> DB 연결 URL은 유저에 대한 <strong><u>인증 정보를 포함</u></strong>하기 때문에, 환경변수 처리를 해야한다&#46; 

- DB URL 환경 변수 처리
    > <a href="#/post/22deda9b-0fe1-8083-960b-faeeff88659d">페이지</a> 참조

- 루트 모듈(<code>AppModule</code>) &#45; 환경변수 및 DB 연결 설정
    <a id="22deda9b0fe1804eb795e31f705bc9d0"></a>

    ```typescript
    import { Module } from '@nestjs/common';
    import { AppController } from './app.controller';
    import { AppService } from './app.service';
    import { MongooseModule } from '@nestjs/mongoose';
    import { ConfigModule } from '@nestjs/config';

    @Module({
      imports: [
        ConfigModule.forRoot(),  // 환경변수 import를 위한 설정
        MongooseModule.forRoot(  // DB 연동
          process.env.MONGODB_URI || 'mongodb://localhost/nest',
        ),
      ],
      controllers: [AppController],
      providers: [AppService],
    })
    export class AppModule {}
    ```

</details>

<a id="22deda9b0fe18018a2f6cd936531a871"></a>

### 3&#46; Mongoose Docs

[Mongoose ODM v8&#46;16&#46;1]()
