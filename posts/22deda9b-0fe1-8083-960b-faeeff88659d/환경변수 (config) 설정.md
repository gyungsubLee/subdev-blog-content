---
order: 7
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 22deda9b-0fe1-8083-960b-faeeff88659d
title: 환경변수 (config) 설정
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 226eda9b-0fe1-802b-a035-c3a886768c4d
    title: Nest.js
  - id: 227eda9b-0fe1-80e1-8036-d4fc3e106054
    title: 탄탄한 백엔드 NestJS, 기초부터 심화까지 ( 중지 )
  - id: 22deda9b-0fe1-8083-960b-faeeff88659d
    title: 환경변수 (config) 설정
excerpt: 목차 - 환경변수 설정 - 1. 패키지 설치 - 2. 루트 모듈(AppModule)에 ConfigModule import - 3. 루트 경로에 .env 파일 정의 - 4. 루트 모듈(AppModule)에서 MongoDB 연결에 환경변수 사용 - 4.2 특정 클래스에서 사용 [Documentation | NestJS - A
cover: b177c3dbe712a575.webp
icon: null
notionProperties: {}
schema_version: 1
parent_id: 227eda9b-0fe1-80e1-8036-d4fc3e106054
created: 2025-07-11T09:52:17.908Z
updated: 2025-08-15T06:46:39.704Z
legacy_path: Main/Nest.js-c3a886768c4d/탄탄한 백엔드 NestJS, 기초부터 심화까지 ( 중지 )-d4fc3e106054/환경변수 (config) 설정-faeeff88659d/index.md
legacy_category: Nest.js
source_url: https://beautiful-college-c84.notion.site/22deda9b0fe18083960bfaeeff88659d
---
> 
> 
> <a id="22deda9b0fe180fdb1ebd13eb1b812c7"></a>
> 
> <strong>목차</strong>
> 
> - [환경변수 설정](#22deda9b0fe180909c58d563af5881fe)
> - [1. 패키지 설치](#22deda9b0fe180c3b02be266f07a90a8)
> - [2. 루트 모듈(AppModule)에 ConfigModule import](#22deda9b0fe180bb969ecf3709734ff1)
> - [3. 루트 경로에 .env 파일 정의](#22deda9b0fe1802d8ac8f972170121a0)
> - [4. 루트 모듈(AppModule)에서 MongoDB 연결에 환경변수 사용](#22deda9b0fe1801bbd0defec370d22a7)
> - [4.2  특정 클래스에서 사용](#235eda9b0fe180478423d23497f4cf49)

[Documentation &#124; NestJS &#45; A progressive Node&#46;js framework]()

<a id="22deda9b0fe180909c58d563af5881fe"></a>

## <strong>환경변수 설정</strong>

---

<a id="22deda9b0fe180c3b02be266f07a90a8"></a>

### 1&#46; 패키지 설치

> ✏️ 
> 
> <a id="22deda9b0fe1805f8396ddd5581ba56c"></a>
> 
> <code>dotenv</code> 패키지를 기본적으로 설치 해준다&#46;

<a id="22deda9b0fe180baa0b6ee0e7bf0b546"></a>

```bash
# npm
npm i --save @nestjs/config

# pnpm
pnpm add --save @nestjs/config
```

<a id="22deda9b0fe180bb969ecf3709734ff1"></a>

### 2&#46; 루트 모듈(<code>AppModule</code>)에 <code>ConfigModule</code> import

<a id="22deda9b0fe18036b6aecd6685732d12"></a>

```typescript
import { Module } from '@nestjs/common';
import { ConfigModule } from '@nestjs/config';

@Module({
  imports: [ConfigModule.forRoot({ 
	  isGlobal: true 
  })],
})


export class AppModule {}
```

- <code>isGlobal&#58; true</code>
    - ConfiModule을 Global(전역) Scope로 설정

    - 다른 모듈에서도 접근하여 ConfigModule을 통해 전역 변수를 가져올 수 있음

<a id="22deda9b0fe1802d8ac8f972170121a0"></a>

### 3&#46; 루트 경로에 <code>&#46;env</code> 파일 정의

<a id="22deda9b0fe1800e8bb8cb95d69ee1d3"></a>

```typescript
MONGODB_URL="mongodb://admin:admin123@localhost:27017/nest?authSource=admin"
```

<a id="22deda9b0fe1801bbd0defec370d22a7"></a>

### 4&#46; 루트 모듈(<code>AppModule</code>)에서 MongoDB 연결에 환경변수 사용

<details>
<summary><strong>&#91; 🤬 Bad Case &#93;</strong><strong>  </strong><strong>process&#46;env 직접 접근</strong></summary>

> ✏️ 
> 
> <a id="234eda9b0fe1806bbee9fe985f7bdf0c"></a>
> 
> NestJS는 의존성 주입(Dependency Injection, DI) 기반 아키텍처이다&#46; 하지만 <code>process&#46;env</code>는 <strong><u>Nest의 DI 시스템 외부에 있는 Node&#46;js 전역 객체</u></strong>이기 때문에 아래와 같은 문제가 있다&#46;
> 
> > <a href="#/post/233eda9b-0fe1-80c6-b90a-fca9411f535a">페이지</a> 
> 
> <details>
> <summary>문제점</summary>
> 
> - 테스트 어려움
>     - 단위 테스트 시, process&#46;env를 mocking해야 해서 복잡하고 깨지기 쉬움
> 
> - <strong>유연성 부족</strong>
>     - 환경에 따라 DB를 동적으로 변경하거나 외부 설정을 로드할 수 없음
> 
> - NestJS DI와 분리
>     - ConfigService 같은 NestJS 내부 설정 시스템과 연결되지 않음
> 
> - 타입 안정성 없음
>     - process&#46;env는 무조건 <code>string</code> 타입으로 간주된다&#46; 
> 
> </details>

<a id="22deda9b0fe18064987ff43f74ec7f99"></a>

```typescript
import { Module } from '@nestjs/common';
import { AppController } from './app.controller';
import { AppService } from './app.service';
import { MongooseModule } from '@nestjs/mongoose';
import { ConfigModule } from '@nestjs/config';

@Module({
  imports: [
    ConfigModule.forRoot(),
    MongooseModule.forRoot(
      process.env.MONGODB_URI || 'mongodb://localhost/nest',
    ),
  ],
  controllers: [AppController],
  providers: [AppService],
})
export class AppModule {}

```

</details>

<a id="22deda9b0fe180c78d2ec9a5f71550f0"></a>

```typescript
import { Module } from '@nestjs/common';
import { ConfigModule, ConfigService } from '@nestjs/config';
import { MongooseModule } from '@nestjs/mongoose';
import { AppController } from './app.controller';
import { AppService } from './app.service';

@Module({
  imports: [
    // .env를 전역으로 로드
    ConfigModule.forRoot({ isGlobal: true }),

    // 비동기 방식으로 ConfigService 사용
    MongooseModule.forRootAsync({
      imports: [ConfigModule],
      inject: [ConfigService],
      useFactory: (configService: ConfigService) => ({
        uri: configService.get<string>('MONGODB_URI') || 'mongodb://localhost/nest',
      }),
    }),
  ],
  controllers: [AppController],
  providers: [AppService],
})
export class AppModule {}
```

<a id="235eda9b0fe180478423d23497f4cf49"></a>

### 4&#46;2  특정 클래스에서 사용

> ✏️ 
> 
> <a id="235eda9b0fe180c88bdcff5362e2dc3c"></a>
> 
>  루트 경로에 정의한 <code>&#46;env</code> 파일 안의 값을 가져온다&#46;

<a id="231eda9b0fe1804d9544d58e5803e8ff"></a>

```typescript
// ex1) ConfigService
import { ConfigService } from '@nestjs/config';

@Injectable()
export class AwsService {
  private readonly awsS3: AWS.S3;
  public readonly S3_BUCKET_NAME: string;

  constructor(private readonly configService: ConfigService) {
    this.awsS3 = new AWS.S3({
      accessKeyId: configService.get('AWS_S3_ACCESS_KEY'),
      
      . . .
```
