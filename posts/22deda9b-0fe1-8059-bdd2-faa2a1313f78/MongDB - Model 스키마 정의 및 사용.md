---
order: 15
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 22deda9b-0fe1-8059-bdd2-faa2a1313f78
title: MongDB - Model 스키마 정의 및 사용
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 226eda9b-0fe1-802b-a035-c3a886768c4d
    title: Nest.js
  - id: 227eda9b-0fe1-80e1-8036-d4fc3e106054
    title: 탄탄한 백엔드 NestJS, 기초부터 심화까지 ( 중지 )
  - id: 22deda9b-0fe1-8059-bdd2-faa2a1313f78
    title: MongDB - Model 스키마 정의 및 사용
excerpt: 목차 - 핵심 요약 - NestJS, MongoDB 연결 및 스키마 정의 - 1. MongoDB 로깅 설정 - 2. MongoDB 연결 - 3. 스키마 정의 - 4. 스키마, 모듈에 등록 - 5. 스키마 사용 [Documentation | NestJS - A progressive Node.js framework]() 핵심
cover: fb3b1ee7da4a15e0.webp
icon: 9bed2eae1e079b4b.avif
notionProperties: {}
schema_version: 1
parent_id: 227eda9b-0fe1-80e1-8036-d4fc3e106054
created: 2025-07-11T10:35:52.814Z
updated: 2025-07-21T08:00:26.569Z
legacy_path: Main/Nest.js-c3a886768c4d/탄탄한 백엔드 NestJS, 기초부터 심화까지 ( 중지 )-d4fc3e106054/MongDB - Model 스키마 정의 및 사용-faa2a1313f78/index.md
legacy_category: Nest.js
source_url: https://beautiful-college-c84.notion.site/22deda9b0fe18059bdd2faa2a1313f78
---
> 
> 
> <a id="22deda9b0fe18184b263e8efcd608940"></a>
> 
> <strong>목차</strong>
> 
> - [핵심 요약](#22feda9b0fe180b697d1dd9ff6c1e954)
> - [NestJS, MongoDB 연결 및 스키마 정의](#22deda9b0fe181df9e00cbee7e96d251)
> - [1. MongoDB 로깅 설정](#22deda9b0fe1804a9870f65f841219f3)
> - [2. MongoDB 연결](#22eeda9b0fe180698a44c1e30294e60d)
> - [3. 스키마 정의](#22eeda9b0fe18018a73dd5c728e6779e)
> - [4. 스키마, 모듈에 등록](#22deda9b0fe1809aac21cb389fc85e42)
> - [5. 스키마 사용](#22feda9b0fe1809b9a3bdb81eb249c41)

[Documentation &#124; NestJS &#45; A progressive Node&#46;js framework]()

<a id="22feda9b0fe180b697d1dd9ff6c1e954"></a>

### 핵심 요약

<a id="22feda9b0fe180399d3ec19f5a9cef3c"></a>

```typescript
// 1. schema 정의
@Schema()
export class Cat { ... }
export const CatSchema = SchemaFactory.createForClass(Cat);

// 2. module에 등록
@Module({
  imports: [
    MongooseModule.forFeature([
      { name: Cat.name, schema: CatSchema }
    ])
  ],
})
export class CatsModule {}

// 3. 서비스에서 사용
@Injectable()
export class CatsService {
  constructor(
    @InjectModel(Cat.name) private readonly catModel: Model<CatDocument>
  ) {}
}
```

<a id="22deda9b0fe181df9e00cbee7e96d251"></a>

## NestJS, MongoDB 연결 및 스키마 정의

---

<a id="22deda9b0fe1804a9870f65f841219f3"></a>

### 1&#46; MongoDB 로깅 설정

[feat: MongoDB(mongoose) 로깅 설정](https://github.com/gyungsubLee/NestJS_prac/commit/1752465f469f06cd08edf3e947070b8ee85c4036)

<a id="22feda9b0fe180509425dbd71cbf6155"></a>

```typescript
// app.module.ts
import { MongooseModule } from '@nestjs/mongoose';
import { ConfigModule } from '@nestjs/config';
import { LoggerMiddleware } from './common/middlewares/logger/logger.middleware';
import mongoose from 'mongoose';

@Module({
  imports: [
  providers: [AppService],
})
export class AppModule implements NestModule {
  private readonly isDev: boolean = process.env.MODE === 'dev' ? true : false;
  configure(consumer: MiddlewareConsumer) {
    consumer.apply(LoggerMiddleware).forRoutes('*');
    mongoose.set('debug', this.isDev); // Mongoose 디버그 모드 활성화
  }
}
```

<a id="22feda9b0fe180db86eaf17a648960f3"></a>

```typescript
// .env
MODE="dev"
```

<a id="22eeda9b0fe180698a44c1e30294e60d"></a>

### 2&#46; MongoDB 연결

> ✏️ 
> 
> - DB 연결&#58; <a href="#/post/22deda9b-0fe1-80bc-9069-ef853ac5fbf0">페이지</a> 
> 
> - 환경변수 설정&#58; <a href="#/post/22deda9b-0fe1-8083-960b-faeeff88659d">페이지</a> 

<a id="22eeda9b0fe1809a9584e33b0e47f2c0"></a>

```typescript
import { Module } from '@nestjs/common';
import { AppController } from './app.controller';
import { AppService } from './app.service';
import { MongooseModule } from '@nestjs/mongoose';
import { ConfigModule } from '@nestjs/config';

@Module({
  imports: [
		ConfigModule.forRoot({ isGlobal: true }),  // .env import 설정
    MongooseModule.forRoot(  // MongoDB connect 설정
      process.env.MONGODB_URI || 'mongodb://localhost/nest',
      {
        dbName: 'nest',
      },
    ),
  ],
  controllers: [AppController],
  providers: [AppService],
})
export class AppModule implements NestModule {
  private readonly isDev: boolean = process.env.MODE === 'dev' ? true : false;
  configure(consumer: MiddlewareConsumer) {
    consumer.apply(LoggerMiddleware).forRoutes('*');  // 로깅 미들웨어 설정
    mongoose.set('debug', this.isDev); // Mongoose 디버그 모드 활성화
  }
}
```

<a id="22eeda9b0fe18018a73dd5c728e6779e"></a>

### 3&#46; 스키마 정의

> ✏️ 
> 
> <a id="22feda9b0fe1802b80b3ecd16e330c53"></a>
> 
> <strong>MongDB의 데이터 식별자(Identifier)</strong>
> 
> ---
> 
> <a id="22eeda9b0fe1804d9753ef7fcf921caa"></a>
> 
> MongoDB와 같은 <strong>NoSQL</strong>에서는 <strong>RDBMS에서의 </strong><strong><code>PK(Primary Key)</code></strong> 개념과는 약간 다른 방식으로 <strong><code>데이터 식별자(Identifier)</code></strong>를 다룬다&#46;
> 
> - 모든 Document는 <code>&#95;id</code> 필드를 <strong>무조건 가져야 한다&#46;</strong>
> 
> - <strong>생략 시, MongoDB가 자동으로 </strong><strong><code>ObjectId()</code></strong><strong> 형태의 고유 값을 생성한다&#46;</strong>
> 
> <details>
> <summary>ex)</summary>
> 
> <a id="22eeda9b0fe1802c8afbd0a9ffaf9d2a"></a>
> 
> ```typescript
> {
>   "_id": "64dabc12345e6789012f3456", // 12바이트 ObjectId
>   "email": "example@test.com",
>   "name": "John"
> }
> ```
> 
> </details>

<a id="22feda9b0fe18057b3a2f2da1ea68f04"></a>

```typescript
import { Prop, Schema, SchemaFactory } from '@nestjs/mongoose';
import { IsEmail, IsNotEmpty, IsString } from 'class-validator';
import { HydratedDocument } from 'mongoose';

export type CatDocument = HydratedDocument<Cat>;

@Schema()
export class Cat {
	  @Prop({ required: true, unique: true })
	  @IsEmail()
	  @IsNotEmpty()
	  email: string;
	
	  @Prop({ required: true })
	  @IsString()
	  @IsNotEmpty()
	  name: string;
	
	  @Prop({ required: true })
	  @IsString()
	  @IsNotEmpty()
	  password: string;
	
	  @Prop()
	  @IsString()
	  imgUrl: string;
}

export const CatSchema = SchemaFactory.createForClass(Cat);
```

<details>
<summary>1&#46; 주요 의존성</summary>

| <strong>구문</strong> | <strong>설명</strong> |
| --- | --- |
| <code>&#64;nestjs/mongoose</code> | NestJS에서 Mongoose ODM(Object Document Mapper)을 쉽게 사용할 수 있게 해주는 공식 모듈 |
| <code>class&#45;validator</code> | 클래스 프로퍼티에 대해 유효성 검사 데코레이터를 제공하는 라이브러리 |
| <code>mongoose</code> | MongoDB와 상호작용하기 위한 ODM |

</details>

<details>
<summary>2&#46; 모델 정의</summary>

<a id="22feda9b0fe180d49606fc3f01ee10c1"></a>

```typescript
export type CatDocument = HydratedDocument<Cat>;
```

- <code>HydratedDocument&#60;T&#62;</code>&#58; Mongoose 문서를 NestJS 타입으로 변환할 때 사용하는 타입이다&#46;

- <code>CatDocument</code>&#58; Cat 스키마 기반으로 만들어진 문서 타입이며, CatModel의 반환값 또는 DB 결과에 주로 사용된다&#46;

</details>

<details>
<summary>3&#46; Cat 클래스와 데코레이터 설명</summary>

<a id="22feda9b0fe18063bc49e160abdb9290"></a>

```typescript
@Prop({ required: true, unique: true })
@IsEmail()
@IsNotEmpty()
email: string;

@Prop()
@IsString()
imgUrl: string;
```

- <code>&#64;Prop(&#46;&#46;&#46;)</code>&#58; Mongoose에서 사용하는 필드 스키마 정의 데코레이터

> 💬 
> 
> > <a href="#/post/22deda9b-0fe1-8094-ba57-ea4fa43986cf">페이지</a> 
> 
> <a id="22eeda9b0fe180ecabc8c5479da0732d"></a>
> 
> 유효성 검사를 DTO에 책임 분리를 하는 것이 좋다&#46;<br>따라서 이후 DTO 정의 시 리펙토링 진행
> 
> <details>
> <summary>ex) </summary>
> 
> <a id="22eeda9b0fe180fca606e0807273a08a"></a>
> 
> ```typescript
> import { Prop, Schema, SchemaFactory } from '@nestjs/mongoose';
> import { IsEmail, IsNotEmpty, IsString } from 'class-validator';
> import { HydratedDocument } from 'mongoose';
> 
> export type CatDocument = HydratedDocument<Cat>;
> 
> @Schema()
> export class Cat {
>   @Prop({ required: true, unique: true })
>   @IsEmail()
>   @IsNotEmpty()
>   email: string;
> 
>   @Prop({ required: true })
>   @IsString()
>   @IsNotEmpty()
>   name: string;
> 
>   @Prop({ required: true })
>   @IsString()
>   @IsNotEmpty()
>   password: string;
> 
>   @Prop()
>   @IsString()
>   imgUrl: string;
> }
> 
> export const CatSchema = SchemaFactory.createForClass(Cat);
> ```
> 
> - 위 내용 분리 필요
> 
> </details>

- <code>IsEamil()</code>&#58; 이메일 형태인지 검사 

- <code>&#64;IsString()</code>&#58; 문자열인지 검사

- <code>&#64;IsNotEmpty()</code>&#58; 비어있지 않은 값인지 검사

- …<br><br>

</details>

<details>
<summary>4&#46; Mongoose 스키마 생성</summary>

<a id="22feda9b0fe18043918dfaedfeacaa2d"></a>

```typescript
export const CatSchema = SchemaFactory.createForClass(Cat);
```

- <code>SchemaFactory&#46;createForClass(&#46;&#46;&#46;)</code>&#58; 클래스 기반으로 Mongoose 스키마를 생성

- 이 결과 <code>CatSchema</code>는  <code>MongooseModule&#46;forFeature(&#91;{ name&#58; Cat&#46;name, schema&#58; CatSchema }&#93;)</code> 처럼 해당 모듈에서 Nest 컨테이너에 등록하는 등에 사용한다&#46; <br><br>

</details>

<a id="22deda9b0fe1809aac21cb389fc85e42"></a>

### 4&#46; 스키마, 모듈에 등록

> ✏️ 
> 
> <a id="22feda9b0fe1808181a7f818b006fde6"></a>
> 
> NestJS는 내부적으로 Mongoose 모델을 Nest의 DI 컨테이너에서 관리하기 위해, <code>MongooseModule&#46;forFeature(&#46;&#46;&#46;)</code>를 통해 스키마를 등록해야 한다&#46;
> 
> <a id="22feda9b0fe180febf5ae914aa454b10"></a>
> 
> 따라서 스키마 정의 후, 필수적으로 아래와 같이 해당되는 모듈에 스키마를 등록해야 한다&#46;

<a id="22eeda9b0fe1806bb12ff02ccef7997c"></a>

```typescript

import { Module } from '@nestjs/common';
import { MongooseModule } from '@nestjs/mongoose';
import { CatsController } from './cats.controller';
import { CatsService } from './cats.service';
import { Cat, CatSchema } from './schemas/cat.schema';

@Module({
  imports: [MongooseModule.forFeature([{ name: Cat.name, schema: CatSchema }])],
  controllers: [CatsController],
  providers: [CatsService],
})
export class CatsModule {}

```

<a id="22feda9b0fe1809b9a3bdb81eb249c41"></a>

### 5&#46; 스키마 사용

<details>
<summary>서비스 계층에서 사용</summary>

<a id="22feda9b0fe180f6a53ae5be38d306da"></a>

```typescript
// cats.service.ts
import { Injectable } from '@nestjs/common';
import { InjectModel } from '@nestjs/mongoose';
import { Cat, CatDocument } from './schemas/cat.schema';
import { Model } from 'mongoose';

@Injectable()
export class CatsService {
	// Cat 모델 DI 
  constructor(
    @InjectModel(Cat.name)
    private readonly catModel: Model<CatDocument>,
  ) {}

  async createCat(name: string, email: string, password: string): Promise<Cat> {
    const newCat = new this.catModel({ name, email, password });
    return await newCat.save();
  }

  async findAll(): Promise<Cat[]> {
    return this.catModel.find().exec();
  }
}
```

</details>

<a id="22feda9b0fe18088a3b3d0a9d86b2780"></a>

<strong><br>Repository 레이어로 분리한 실무형 구조</strong>

<a id="22feda9b0fe180a0be14c2bc6033ba81"></a>

```typescript
CatsController
└── CatsService   ← 비즈니스 로직
     └── CatsRepository  ← DB 접근 로직
          └── Mongoose Model (Cat)
```

<details>
<summary>&#91; 코드 &#93; <code>cats&#46;module&#46;ts</code></summary>

<a id="22feda9b0fe1801394d8ca914c923b04"></a>

```typescript
// cats.module.ts
@Module({
  imports: [MongooseModule.forFeature([{ name: Cat.name, schema: CatSchema }])],
  providers: [CatsService, CatsRepository],
})
export class CatsModule {}
```

</details>

<details>
<summary>&#91; 코드 &#93; <code>cats&#46;service&#46;ts</code></summary>

<a id="22feda9b0fe1806b8207cbff951e2d0a"></a>

```typescript
// cats.service.ts
import { Injectable } from '@nestjs/common';
import { CatsRepository } from './cats.repository';
import { Cat } from './schemas/cat.schema';

@Injectable()
export class CatsService {
  constructor(private readonly catsRepository: CatsRepository) {}

  async registerCat(data: Partial<Cat>): Promise<Cat> {
    return this.catsRepository.create(data);
  }

  async getAllCats(): Promise<Cat[]> {
    return this.catsRepository.findAll();
  }
}
```

</details>

<details>
<summary>&#91; 코드 &#93; <code>cats&#46;repository&#46;ts</code></summary>

<a id="22feda9b0fe18061a848f0d84c0ceb4a"></a>

```typescript
// cats.repository.ts
import { Injectable } from '@nestjs/common';
import { InjectModel } from '@nestjs/mongoose';
import { Cat, CatDocument } from './schemas/cat.schema';
import { Model } from 'mongoose';

@Injectable()
export class CatsRepository {
  constructor(
    @InjectModel(Cat.name)
    private readonly catModel: Model<CatDocument>,
  ) {}

  async create(data: Partial<Cat>): Promise<Cat> {
    const cat = new this.catModel(data);
    return await cat.save();
  }

  async findAll(): Promise<Cat[]> {
    return this.catModel.find().exec();
  }

  async findByEmail(email: string): Promise<Cat | null> {
    return this.catModel.findOne({ email }).exec();
  }
}
```

</details>
