---
order: 0
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 233eda9b-0fe1-80c6-b90a-fca9411f535a
title: 환경변수 설정 - process.env 직접 접근 시 단점
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 226eda9b-0fe1-802b-a035-c3a886768c4d
    title: Nest.js
  - id: 227eda9b-0fe1-80e1-8036-d4fc3e106054
    title: 탄탄한 백엔드 NestJS, 기초부터 심화까지 ( 중지 )
  - id: 231eda9b-0fe1-804c-9de8-d632d6f144d4
    title: TypeORM
  - id: 233eda9b-0fe1-80c6-b90a-fca9411f535a
    title: 환경변수 설정 - process.env 직접 접근 시 단점
excerpt: "목차 - 🤬 Bad Case: forRoot() + process.env 직접 접근 - 코드 - 문제점 - ✅ Best Case: forRootAsync() + ConfigService - 코드 - 개선점 - 결론 🤬 Bad Case: forRoot() + process.env 직접 접근 --- 코드 typescrip"
cover: null
icon: null
notionProperties: {}
schema_version: 1
parent_id: 231eda9b-0fe1-804c-9de8-d632d6f144d4
created: 2025-07-17T11:08:22.431Z
updated: 2025-07-17T11:59:02.449Z
legacy_path: Main/Nest.js-c3a886768c4d/탄탄한 백엔드 NestJS, 기초부터 심화까지 ( 중지 )-d4fc3e106054/TypeORM-d632d6f144d4/환경변수 설정 - process.env 직접 접근 시 단점-fca9411f535a/index.md
legacy_category: Nest.js
source_url: https://beautiful-college-c84.notion.site/233eda9b0fe180c6b90afca9411f535a
---
> 
> 
> <a id="233eda9b0fe1809e896de1306ab120a5"></a>
> 
> 목차
> 
> - [🤬 Bad Case: forRoot() + process.env 직접 접근](#233eda9b0fe18062aef6fd67eeb5590d)
> - [코드](#233eda9b0fe180d19c3ed762365d68b2)
> - [ 문제점](#233eda9b0fe180d4ac28fb2d33f3c991)
> - [✅ Best Case: forRootAsync() + ConfigService](#233eda9b0fe180f7a02bfb9b2c43d2a8)
> - [ 코드](#233eda9b0fe1807091f6d57d9665689f)
> - [ 개선점](#233eda9b0fe180a6a1ccdbf8728b5d65)
> - [결론](#233eda9b0fe180fcb8cec0e54843efb9)

<a id="233eda9b0fe18062aef6fd67eeb5590d"></a>

## 🤬 Bad Case&#58; <code>forRoot()</code> &#43; <code>process&#46;env</code> 직접 접근

---

<a id="233eda9b0fe180d19c3ed762365d68b2"></a>

### 코드

<a id="233eda9b0fe1801cb666c7015442a684"></a>

```typescript
@Module({
  imports: [
    ConfigModule.forRoot({ isGlobal: true }), // 환경 변수 자동 로드
    TypeOrmModule.forRoot({
      type: 'mysql',
      host: process.env.MYSQL_HOST,
      port: parseInt(process.env.MYSQL_PORT ?? '3306', 10),
      username: process.env.MYSQL_USER,
      password: process.env.MYSQL_PASSWORD,
      database: process.env.MYSQL_DATABASE,
      entities: [],
      synchronize: true,
    }),
  ],
})
export class AppModule {}
```

<a id="233eda9b0fe180d4ac28fb2d33f3c991"></a>

### <strong> 문제점</strong>

<a id="233eda9b0fe180a88929c50ac694a2c2"></a>

Node&#46;js는  <code>dotenv</code> (혹은 <code>ConfigModule&#46;forRoot()</code>)를 통해 <code>&#46;env</code> 파일을 <code>process&#46;env</code>에 올려놓는다&#46; 

<a id="233eda9b0fe180779a6bf98a59da5a1f"></a>

즉,  <strong><u>Node 레벨에서 환경변수를 직접 읽</u></strong>는 것이라<strong><u> Nest 구조 외부에서 처리</u></strong>된다&#46; 

- NestJS가 실행될 때 <code>process&#46;env&#46;MYSQL&#95;PORT</code> 같은 값을 읽어올 수 있다&#46;

<a id="233eda9b0fe180ea81ddf7373c496c2e"></a>

따라서 process&#46;env는 Nest의 DI 시스템 밖에 존재하게 되고, 이는 NestJS 구조와의 불일치가 발생되어 아래와 문제를 발생시킨다&#46; 

- 유닛 테스트 불가능

- 모듈 재사용 불편

- <code>• env</code>를 <strong>비동기 로드하는 경우(예&#58; AWS Secrets Manager 등)</strong> 문제가 생길 수 있음

- Nest의 환경 기반 시스템(ConfigService)과 <strong>전혀 통합되어 있지 않음</strong><br>

<a id="233eda9b0fe180f7a02bfb9b2c43d2a8"></a>

## ✅ Best Case&#58; <strong><code>forRootAsync()</code></strong><strong> &#43; </strong><strong><code>ConfigService</code></strong>

---

<a id="233eda9b0fe1807091f6d57d9665689f"></a>

###  코드

<a id="233eda9b0fe180ee84f4e5985f5e57ac"></a>

```typescript
// app.module.ts
import { Module } from '@nestjs/common';
import { ConfigModule } from '@nestjs/config';
import { TypeOrmModule } from '@nestjs/typeorm';


@Module({
  imports: [
    ConfigModule.forRoot({ isGlobal: true }),
    TypeOrmModule.forRootAsync({
      useFactory: (config: ConfigService) => ({
        type: 'mysql',
        host: config.get('DB_HOST'),
        port: parseInt(config.get('DB_PORT')),
        username: config.get('DB_USER'),
        password: config.get('DB_PASS'),
        database: config.get('DB_NAME'),
        entities: [User], // 엔티티 등록
        synchronize: true,
      }),
      inject: [ConfigService],
    }),
  ],
})
export class AppModule {}
```

<a id="233eda9b0fe180a6a1ccdbf8728b5d65"></a>

###  개선점

| <strong>항목</strong> | <strong>설명</strong> |
| --- | --- |
| <strong>NestJS DI 통합</strong> | ConfigService를 통해 환경 변수 접근<br>&#45; 테스트 가능, 모듈화 용이 |
| <strong>비동기 로딩 지원</strong> | AWS SSM, 외부 API, 파일, DB 등에서 설정 값을 불러올 수 있음 |
| <strong>모듈 간 의존성 주입</strong> | 예&#58; 환경에 따라 동적 DB 선택, 멀티테넌시 구성도 가능 |
| <strong>Nest 공식 권장 방식</strong> | forRootAsync()는 실무 환경에서 유일하게 확장성 있는 방식 |

<details>
<summary>ex) <strong>비동기 외부 설정</strong></summary>

<a id="233eda9b0fe1806f9008e09d21e9766e"></a>

```typescript
TypeOrmModule.forRootAsync({
  useFactory: async () => {
    const configFromSSM = await fetchFromAwsSsm();
    return {
      type: 'mysql',
      host: configFromSSM.host,
      ...
    };
  },
})
```

- 비동기 방식으로 외부 환경설정을 로드하려면 반드시 forRootAsync()가 필요하다&#46;

- process&#46;env 방식은 위 방법을 지원하지 못한다&#46; 

</details>

<a id="233eda9b0fe180fcb8cec0e54843efb9"></a>

## 결론

| <strong>질문</strong> | <strong>답변</strong> |
| --- | --- |
| ❓ process&#46;env 방식도 왜 동작하는가? | Nest가 실행되기 전에 Node가 &#46;env를 로드해서 전역으로 접근 가능하기 때문이다&#46; |
| ❓ 그럼 왜 forRootAsync()가 더 나은가? | Nest의 DI와 설정 시스템에 통합되며, 더 유연하고 테스트 가능하기 때문이다&#46; |
| ❓ Nest 공식에서는 어떤 걸 권장하는가? | NestJS <a href="https://docs.nestjs.com/techniques/configuration">공식 문서</a>에서 forRootAsync() &#43; ConfigService 조합을 권장한다&#46; |

| <strong>상황</strong> | <strong>추천 방식</strong> |
| --- | --- |
| 간단한 테스트/샘플 프로젝트 | process&#46;env도 OK |
| 실무 서비스, 협업 환경, 환경 분리(dev/prod/test) | ✅ 반드시 ConfigService &#43; forRootAsync() 사용 |
