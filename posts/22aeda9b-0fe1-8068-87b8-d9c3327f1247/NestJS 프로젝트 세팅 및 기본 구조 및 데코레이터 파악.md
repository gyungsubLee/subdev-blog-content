---
order: 28
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 22aeda9b-0fe1-8068-87b8-d9c3327f1247
title: NestJS 프로젝트 세팅 및 기본 구조 및 데코레이터 파악
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 226eda9b-0fe1-802b-a035-c3a886768c4d
    title: Nest.js
  - id: 227eda9b-0fe1-80e1-8036-d4fc3e106054
    title: 탄탄한 백엔드 NestJS, 기초부터 심화까지 ( 중지 )
  - id: 22aeda9b-0fe1-8068-87b8-d9c3327f1247
    title: NestJS 프로젝트 세팅 및 기본 구조 및 데코레이터 파악
excerpt: 목차 - NestJS 프로젝트 세팅 및 기본 구조 파악 - 1. NestJS 설치 및 서버 실행 - 2. NestJS 기본 구조 - 3. 데코레이터 NestJS 프로젝트 세팅 및 기본 구조 파악 --- 1. NestJS 설치 및 서버 실행 --- [Documentation | NestJS - A progressive No
cover: 3e244050612f7bd7.webp
icon: null
notionProperties: {}
schema_version: 1
parent_id: 227eda9b-0fe1-80e1-8036-d4fc3e106054
created: 2025-07-08T06:01:30.603Z
updated: 2025-07-15T08:02:00.120Z
legacy_path: Main/Nest.js-c3a886768c4d/탄탄한 백엔드 NestJS, 기초부터 심화까지 ( 중지 )-d4fc3e106054/NestJS 프로젝트 세팅 및 기본 구조 및 데코레이터 파악-d9c3327f1247/index.md
legacy_category: Nest.js
source_url: https://beautiful-college-c84.notion.site/22aeda9b0fe1806887b8d9c3327f1247
---
> 
> 
> <a id="22aeda9b0fe18115bb1ff2ca34771f27"></a>
> 
> <strong>목차</strong>
> 
> - [NestJS 프로젝트 세팅 및 기본 구조 파악](#22aeda9b0fe180da893ef3b0cea7ee3a)
> - [1. NestJS 설치 및 서버 실행](#22aeda9b0fe180f3bb8aca7460ae8eb2)
> - [2. NestJS 기본 구조](#22aeda9b0fe180c5bb4ce7cafe3a434d)
> - [3. 데코레이터](#22aeda9b0fe180fe986bd0e57ed50127)

<a id="22aeda9b0fe180da893ef3b0cea7ee3a"></a>

## NestJS 프로젝트 세팅 및 기본 구조 파악

---

<a id="22aeda9b0fe180f3bb8aca7460ae8eb2"></a>

### 1&#46; NestJS 설치 및 서버 실행

---

[Documentation &#124; NestJS &#45; A progressive Node&#46;js framework]()

<a id="22aeda9b0fe18088bb79e36dcc24c742"></a>

```bash
# nestJS 설치
npm i -g @nestjs/cli

# nest 프로젝트 생성
nest new {프로젝트명}

# 서버 시작
npm run start
```

<a id="22aeda9b0fe180c5bb4ce7cafe3a434d"></a>

### 2&#46; NestJS 기본 구조

---

> 💬 
> 
> <a id="22aeda9b0fe1809fbf85ccd1fbb93439"></a>
> 
> Spring 과 유사한 <code>3 layer architecture</code>를 갖는다&#46;
> 
> - controller
> 
> - service 
> 
> - module

<a id="22aeda9b0fe180399f52d8cbe8faf32d"></a>

```bash
📁 src/
    ├── 📑 app.controller.spec.ts   # AppController 테스트 코드 (Jest 기반)
    ├── 📑 app.controller.ts        # 라우팅 및 요청 핸들링 담당
    ├── 📑 app.module.ts            # 루트 모듈 - 애플리케이션의 엔트리 포인트 모듈
    ├── 📑 app.service.ts           # 비즈니스 로직을 담은 서비스 계층
    └── 📑 main.ts                  # Nest 애플리케이션의 부트스트랩 (entry point)
    
📁 test/...                         # 테스트코드...
```

<details>
<summary>1&#46; <code>main&#46;ts</code> </summary>

> ✏️ 
> 
> <a id="22aeda9b0fe18096af16e2b2baa15c61"></a>
> 
> Nest 앱의 시작점
> 
> - Express 기반 Nest 앱을 실행시켜주는 entry point이다&#46; 

<a id="22aeda9b0fe180afb433e120b1a184a6"></a>

```typescript
// main.ts
import { NestFactory } from '@nestjs/core';
import { AppModule } from './app.module';

async function bootstrap() {
  const app = await NestFactory.create(AppModule);
  await app.listen(3000);
}
bootstrap();
```

</details>

<details>
<summary>2&#46; <code>app&#46;module&#46;ts</code></summary>

> ✏️ 
> 
> <a id="22aeda9b0fe18072badcf31af32f7138"></a>
> 
> NestJS에서 모든 컴포넌트를 묶는 <strong>루트 모듈</strong>
> 
> - <strong>모듈(</strong><strong><code>&#64;Module</code></strong><strong>)&#58;</strong> Nest에서 구성 요소를 그룹화하기 위한 핵심 단위

<a id="22aeda9b0fe1807c9835d08134ad1fd7"></a>

```typescript
// app.module.ts
import { Module } from '@nestjs/common';
import { AppController } from './app.controller';
import { AppService } from './app.service';

@Module({
  imports: [],           // 다른 모듈을 불러올 수 있음
  controllers: [AppController],
  providers: [AppService],
})
export class AppModule {}
```

</details>

<details>
<summary>3&#46; <code>app&#46;controller&#46;ts</code></summary>

> ✏️ 
> 
> <a id="22aeda9b0fe180698e65fae7cce5b530"></a>
> 
> 요청을 받아서 응답을 처리하는 컨트롤러
> 
> - <code>&#64;Controller()</code> 해당 클래스가 컨트롤러임을 나타내며, URL 경로와 HTTP 메서드를 매핑한다&#46;

<a id="22aeda9b0fe180c68d45e8489278d4f7"></a>

```typescript
// app.controller.ts
import { Controller, Get } from '@nestjs/common';
import { AppService } from './app.service';

@Controller()
export class AppController {
  constructor(private readonly appService: AppService) {}

  @Get()
  getHello(): string {
    return this.appService.getHello();
  }
}
```

</details>

<details>
<summary>4&#46; <code>app&#46;service&#46;ts</code></summary>

> ✏️ 
> 
> <a id="22aeda9b0fe180f69d17ea0ff8c8fb10"></a>
> 
> 요청을 받아서 응답을 처리하는 컨트롤러
> 
> - <code>&#64;Controller()</code> 해당 클래스가 컨트롤러임을 나타내며, URL 경로와 HTTP 메서드를 매핑한다&#46;

<a id="22aeda9b0fe180299badf795318d82e9"></a>

```typescript
import { Injectable } from '@nestjs/common';

@Injectable()
export class AppService {
  getHello(): string {
    return 'Hello World!';
  }
}
```

</details>

<details>
<summary>5&#46; <code>app&#46;controller&#46;spec&#46;ts</code></summary>

> ✏️ 
> 
> <a id="22aeda9b0fe180e1a81cf4e8f04190c0"></a>
> 
> NestJS는 기본적으로 <strong>Jest</strong>를 사용한 테스트 환경을 제공한다&#46;
> 
> - 해당 테스트 코드는 <code>getHello()</code> 함수가 “Hello World&#33;“ 반환하는지 검증한다&#46;

<a id="22aeda9b0fe18049b482ffa004da6138"></a>

```typescript
// app.controller.spec.ts
import { Test, TestingModule } from '@nestjs/testing';
import { AppController } from './app.controller';
import { AppService } from './app.service';

describe('AppController', () => {
  let appController: AppController;

  beforeEach(async () => {
    const app: TestingModule = await Test.createTestingModule({
      controllers: [AppController],
      providers: [AppService],
    }).compile();

    appController = app.get<AppController>(AppController);
  });

  describe('root', () => {
    it('should return "Hello World!"', () => {
      expect(appController.getHello()).toBe('Hello World!');
    });
  });
});
```

</details>

<a id="22aeda9b0fe180fe986bd0e57ed50127"></a>

### 3&#46; 데코레이터

---

> ✏️ 
> 
> <a id="22aeda9b0fe18019a487e48b248e2c1b"></a>
> 
> 스프링과 유사하게 <strong><u>데코레이터 패턴</u></strong>을 통한 데코레이터(<code>&#64;…</code>) 기반 구조를 갖는다&#46; 
> 
> - Spring에서의 Reflection &#43; Annotation 구조와 동일하다&#46; 

> ⚠️ 
> 
> <a id="22aeda9b0fe18009b5f5ea9932acfaa1"></a>
> 
> 리소스 경로를 구분하는 <code>/</code>는 생략하여 작성한다&#46;

<details>
<summary><strong><code>&#64;Controller()</code></strong></summary>

> ✏️ 
> 
> <a id="22aeda9b0fe180768fc0ea7100083751"></a>
> 
> 요청(Request)을 처리할 컨트롤러 클래스임을 선언하는 데코레이터
> 
> - 라우팅 경로(URL)와 요청 메서드(GET, POST 등)을 연결한다&#46; 
> 
> - 요청을 서비스(<code>&#64;Injectable()</code>)에 위임하여 처리 결과를 응답(Response)한다&#46;

<a id="22aeda9b0fe180ddba1bdd534f2439b9"></a>

```typescript
import { Controller, Get } from '@nestjs/common';

@Controller('cats')  // => http://localhost:3000/cats
export class CatsController {
  @Get()  // => GET /cats
  findAll(): string {
    return '모든 고양이를 반환합니다';
  }
}
```

</details>

<details>
<summary><strong>HTTP 메서드 데코레이터&#58; </strong><strong><code>&#64;Get()</code></strong><strong>, </strong><strong><code>&#64;Post</code></strong><strong>&#46;&#46;&#46;</strong></summary>

> ✏️ 
> 
> <a id="22aeda9b0fe18039bc9cffc08b671f5e"></a>
> 
> <strong>HTTP METHOD 요청 처리하는 핸들러 함수</strong>
> 
> - <code>&#64;Get</code>, <code>&#64;Post</code>&#46;&#46;&#46;
> 
> - 특정 라우트의 HTTP Method 요청에 반응
> 
> - <code>&#64;Controller()</code> 내부의 메서드 위에 붙여서 사용
> 
> <details>
> <summary>&#91; 코드 &#93; RequestMappingMetadata</summary>
> 
> <a id="22aeda9b0fe180de82e1fd46ac87f220"></a>
> 
> ```typescript
> import { RequestMethod } from '../../enums/request-method.enum';
> export interface RequestMappingMetadata {
>     path?: string | string[];
>     method?: RequestMethod;
> }
> export declare const RequestMapping: (metadata?: RequestMappingMetadata) => MethodDecorator;
> /**
>  * Route handler (method) Decorator. Routes HTTP POST requests to the specified path.
>  *
>  * @see [Routing](https://docs.nestjs.com/controllers#routing)
>  *
>  * @publicApi
>  */
> export declare const Post: (path?: string | string[]) => MethodDecorator;
> /**
>  * Route handler (method) Decorator. Routes HTTP GET requests to the specified path.
>  *
>  * @see [Routing](https://docs.nestjs.com/controllers#routing)
>  *
>  * @publicApi
>  */
> export declare const Get: (path?: string | string[]) => MethodDecorator;
> /**
>  * Route handler (method) Decorator. Routes HTTP DELETE requests to the specified path.
>  *
>  * @see [Routing](https://docs.nestjs.com/controllers#routing)
>  *
>  * @publicApi
>  */
> export declare const Delete: (path?: string | string[]) => MethodDecorator;
> /**
>  * Route handler (method) Decorator. Routes HTTP PUT requests to the specified path.
>  *
>  * @see [Routing](https://docs.nestjs.com/controllers#routing)
>  *
>  * @publicApi
>  */
> export declare const Put: (path?: string | string[]) => MethodDecorator;
> /**
>  * Route handler (method) Decorator. Routes HTTP PATCH requests to the specified path.
>  *
>  * @see [Routing](https://docs.nestjs.com/controllers#routing)
>  *
>  * @publicApi
>  */
> export declare const Patch: (path?: string | string[]) => MethodDecorator;
> /**
>  * Route handler (method) Decorator. Routes HTTP OPTIONS requests to the specified path.
>  *
>  * @see [Routing](https://docs.nestjs.com/controllers#routing)
>  *
>  * @publicApi
>  */
> export declare const Options: (path?: string | string[]) => MethodDecorator;
> /**
>  * Route handler (method) Decorator. Routes HTTP HEAD requests to the specified path.
>  *
>  * @see [Routing](https://docs.nestjs.com/controllers#routing)
>  *
>  * @publicApi
>  */
> export declare const Head: (path?: string | string[]) => MethodDecorator;
> /**
>  * Route handler (method) Decorator. Routes all HTTP requests to the specified path.
>  *
>  * @see [Routing](https://docs.nestjs.com/controllers#routing)
>  *
>  * @publicApi
>  */
> export declare const All: (path?: string | string[]) => MethodDecorator;
> /**
>  * Route handler (method) Decorator. Routes HTTP SEARCH requests to the specified path.
>  *
>  * @see [Routing](https://docs.nestjs.com/controllers#routing)
>  *
>  * @publicApi
>  */
> export declare const Search: (path?: string | string[]) => MethodDecorator;
> /**
>  * Route handler (method) Decorator. Routes Webdav PROPFIND requests to the specified path.
>  *
>  * @see [Routing](https://docs.nestjs.com/controllers#routing)
>  *
>  * @publicApi
>  */
> export declare const Propfind: (path?: string | string[]) => MethodDecorator;
> /**
>  * Route handler (method) Decorator. Routes Webdav PROPPATCH requests to the specified path.
>  *
>  * @see [Routing](https://docs.nestjs.com/controllers#routing)
>  *
>  * @publicApi
>  */
> export declare const Proppatch: (path?: string | string[]) => MethodDecorator;
> /**
>  * Route handler (method) Decorator. Routes Webdav MKCOL requests to the specified path.
>  *
>  * @see [Routing](https://docs.nestjs.com/controllers#routing)
>  *
>  * @publicApi
>  */
> export declare const Mkcol: (path?: string | string[]) => MethodDecorator;
> /**
>  * Route handler (method) Decorator. Routes Webdav COPY requests to the specified path.
>  *
>  * @see [Routing](https://docs.nestjs.com/controllers#routing)
>  *
>  * @publicApi
>  */
> export declare const Copy: (path?: string | string[]) => MethodDecorator;
> /**
>  * Route handler (method) Decorator. Routes Webdav MOVE requests to the specified path.
>  *
>  * @see [Routing](https://docs.nestjs.com/controllers#routing)
>  *
>  * @publicApi
>  */
> export declare const Move: (path?: string | string[]) => MethodDecorator;
> /**
>  * Route handler (method) Decorator. Routes Webdav LOCK requests to the specified path.
>  *
>  * @see [Routing](https://docs.nestjs.com/controllers#routing)
>  *
>  * @publicApi
>  */
> export declare const Lock: (path?: string | string[]) => MethodDecorator;
> /**
>  * Route handler (method) Decorator. Routes Webdav UNLOCK requests to the specified path.
>  *
>  * @see [Routing](https://docs.nestjs.com/controllers#routing)
>  *
>  * @publicApi
>  */
> export declare const Unlock: (path?: string | string[]) => MethodDecorator;
> ```
> 
> </details>

<a id="22aeda9b0fe1804b9fd3e71e8efc4105"></a>

```typescript
import { Controller, Get } from '@nestjs/common';

@Controller('dogs') // GET /dogs
export class DogsController {
  @Get()          // GET /dogs
  getAllDogs() {
    return ['푸들', '말티즈', '리트리버'];
  }

  @Get('random')  // GET /dogs/random
  getRandomDog() {
    return '말티즈';
  }
}
```

</details>

<details>
<summary><strong><code>&#64;Module({&#46;&#46;&#46;})</code></strong></summary>

> ✏️ 
> 
> <a id="22aeda9b0fe180edaaf2e466968fc924"></a>
> 
> <strong>NestJS에서 하나의 기능 단위를 나타내는 모듈</strong>을 정의하는 데코레이터
> 
> -  관련된 <strong>Controller</strong>, <strong>Service</strong>, <strong>다른 모듈</strong>들을 하나로 묶어 매핑
> 
> - Nest는 이 구조를 통해<strong><u> DI(의존성 주입) 컨테이너를 구성</u></strong>한다&#46;
> 
> - 하나의 도메인(예&#58; Users, Auth, Cats)에 대해서<br><code>3 layer architecture<br>&#91; module &#43; controller &#43; service &#93;</code><br>로  구한다&#46; 

<a id="22aeda9b0fe180f2b346c98de60f5d88"></a>

```typescript
import { Module } from '@nestjs/common';
import { CatsController } from './cats.controller';
import { CatsService } from './cats.service';

@Module({
  controllers: [CatsController],  // 요청 처리
  providers: [CatsService],       // 비즈니스 로직
})
export class CatsModule {}
```

</details>

<details>
<summary><strong><code>&#64;Injectable()</code></strong></summary>

> ✏️ 
> 
> <a id="22aeda9b0fe180829cefd9c6be925de9"></a>
> 
> <strong>서비스 클래스 또는 의존성 주입 대상 클래스임을 선언</strong>하는 데코레이터
> 
> - Nest의 DI 컨테이너에 등록된다&#46;
> 
> - 다른 클래스에서 생성자 주입으로 사용 가능하다&#46; 

<a id="22aeda9b0fe18017a9d3cb83cdec08c4"></a>

```typescript
// server.ts
import { Injectable } from '@nestjs/common';

@Injectable()
export class CatsService {
  getAllCats(): string[] {
    return ['고양이1', '고양이2'];
  }
}

// controller.ts
@Controller('cats')
export class CatsController {
  // DI - 생성자 주입 
  constructor(private readonly catsService: CatsService) {}

  @Get()
  getCats() {
    return this.catsService.getAllCats();
  }
}
```

</details>
