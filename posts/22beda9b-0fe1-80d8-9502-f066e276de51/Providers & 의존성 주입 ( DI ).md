---
order: 45
kind: article
summary: ""
tags: []
aliases: []
related_ids: []
source_ids: []
review_status: unreviewed
id: 22beda9b-0fe1-80d8-9502-f066e276de51
title: Providers & 의존성 주입 ( DI )
breadcrumbs:
  - id: 1c3eda9b-0fe1-8053-a02d-d27418c5a3fb
    title: Main
  - id: 226eda9b-0fe1-802b-a035-c3a886768c4d
    title: Nest.js
  - id: 227eda9b-0fe1-80e1-8036-d4fc3e106054
    title: 탄탄한 백엔드 NestJS, 기초부터 심화까지 ( 중지 )
  - id: 22beda9b-0fe1-80d8-9502-f066e276de51
    title: Providers & 의존성 주입 ( DI )
excerpt: "목차 - Providers - 실습용 코드 - 의존성 주입 ( Dependency injection ) - 생성자 주입 - NestJS 의존성 주입(DI) 흐름: CatsService 기준 - 코드 - Scope - Custom Provider - Provider 등록 - 수동 인스턴스화 ( Manual instantia"
cover: fb3b1ee7da4a15e0.webp
icon: 9bed2eae1e079b4b.avif
notionProperties: {}
schema_version: 1
parent_id: 227eda9b-0fe1-80e1-8036-d4fc3e106054
created: 2025-07-09T07:48:10.783Z
updated: 2025-07-10T04:15:08.854Z
legacy_path: Main/Nest.js-c3a886768c4d/탄탄한 백엔드 NestJS, 기초부터 심화까지 ( 중지 )-d4fc3e106054/Providers & 의존성 주입 ( DI )-f066e276de51/index.md
legacy_category: Nest.js
source_url: https://beautiful-college-c84.notion.site/22beda9b0fe180d89502f066e276de51
---
> 
> 
> <a id="22beda9b0fe18198a7cee6c01497fe23"></a>
> 
> <strong>목차</strong>
> 
> - [Providers](#22beda9b0fe181f19601f58455af4b0a)
> - [실습용 코드](#22beda9b0fe18062b098fede7ca71191)
> - [의존성 주입 ( Dependency injection ) - 생성자 주입](#22beda9b0fe180889958f4c239dd9d4e)
> - [NestJS 의존성 주입(DI) 흐름: CatsService 기준](#22beda9b0fe1802d9c9ad9152dc3a8c7)
> - [코드](#22beda9b0fe18059b701cf5c603000fd)
> - [Scope](#22beda9b0fe18069bccec834e4a0679a)
> - [Custom Provider](#22beda9b0fe18086af6bc6e08729f5a8)
> - [Provider 등록](#22beda9b0fe180b292a8d5c8a593435b)
> - [수동 인스턴스화 ( Manual instantiation )](#22beda9b0fe1801db976ebb08460104f)

[Documentation &#124; NestJS &#45; A progressive Node&#46;js framework]()

[Documentation &#124; NestJS &#45; A progressive Node&#46;js framework]()

<a id="22beda9b0fe181f19601f58455af4b0a"></a>

## <strong>Providers</strong>

---

> 📖 
> 
> <a id="22beda9b0fe18184b0e6d8ea73cd3201"></a>
> 
> Providers는 Nest의 핵심 개념 중 하나이다&#46;
> 
> <a id="22beda9b0fe180db9ee2ea9da278cb17"></a>
> 
> Providers의 핵심 아이디어는 <strong><u>종속성으로 주입</u></strong>될 수 있어<strong><u> 객체가 서로 다양한 관계를 형성</u></strong>할 수 있다는 것이다&#46; 
> 
> <a id="22beda9b0fe180dc82e2d50d121fdb53"></a>
> 
> 이러한 <u>객체의 의존관계 형성에 대한 책</u>임은 주로<strong> Nest 런타임 시스템에서 처리</strong>한다&#46;  ( <strong><u>Nest IoC 컨테이너를 통한 D</u></strong><u>I</u> )
> 
> <a id="22beda9b0fe1800cb291cc8f05738ac0"></a>
> 
> 이러한 방식을 통해 <strong><u>객체간의 느슨한 결합 관계를 형</u></strong>성하여 <strong><u>SOLID 원칙(OCP, SRP …)을 준수하는 코드 설계</u></strong>를 가능토록 한다&#46;
> 
> - Service, Repository, Factory, Helper 등 과 같은 많은 기본 Nest 클래스들은 Provider로  취급될 수 있다&#46;

> 💬 
> 
> <a id="22beda9b0fe180029a09d9e64feee253"></a>
> 
> Spring에서의 빈 등록과 유사한 내용이다&#46; 
> 
> <a id="22beda9b0fe1807eb0f1f0fb37946490"></a>
> 
> <code>&#64;Component</code> Annotation을 통해 자동으로 클래스를 빈으로 등록하여 ApplicatioContext(Spring IoC 컨테이너)를 통해 DI를 하는 것 처럼
> 
> <a id="22beda9b0fe180b4a8ecd3beea6bba5b"></a>
> 
> NestJS에서는 <code>&#64;Injectable()</code>, <code>&#64;Module(provider=&#46;&#46;&#46;)</code> 데코레이터를 통해 Service 레이어를  <strong><u>Nest IoC 컨테이너에 등록</u></strong>하여 <strong>외부에서 DI 가능</strong>하도록 한다&#46;

<a id="22beda9b0fe18062b098fede7ca71191"></a>

### 실습용 코드

<a id="22beda9b0fe180ef8939f28861b2e523"></a>

```bash
📁 src/
├── 📁 cats/                       # Cats 도메인 모듈
│   ├── 📁 dto/                    # 요청/응답용 DTO 정의
│   │   └── create-cat.dto.ts
│   ├── 📁 interfaces/             # 인터페이스 정의 (도메인 타입 명세)
│   │   └── cat.interface.ts
│   ├── cats.controller.ts         # 라우팅 및 요청 처리
│   ├── cats.service.ts            # 비즈니스 로직
│   └── cats.module.ts (옵션).      # 실제 구조에서는 보통 Cats 전용 모듈 존재
├── app.module.ts                  # 루트 모듈 (전체 앱 구성)
└── main.ts                        # 애플리케이션 진입점 (부트스트랩)
```

<details>
<summary>&#91; 코드 &#93; create&#45;cat&#46;dto&#46;ts</summary>

<a id="22beda9b0fe1809bbdbfed6fb61ac97f"></a>

```typescript
export class CreateCatDto {
  name: string;
  age: number;
  breed: string;
}
```

</details>

<details>
<summary>&#91; 코드 &#93; cats&#46;interface&#46;ts</summary>

<a id="22beda9b0fe180c09963f41e6830d713"></a>

```typescript

export interface Cat {
  name: string;
  age: number;
  breed: string;
}

```

</details>

<details>
<summary>&#91; 코드 &#93; cats&#46;controller&#46;ts</summary>

<a id="22beda9b0fe1805b8f71f0f505b040ec"></a>

```typescript

import { Controller, Get, Post, Body } from '@nestjs/common';
import { CreateCatDto } from './dto/create-cat.dto';
import { CatsService } from './cats.service';
import { Cat } from './interfaces/cat.interface';

@Controller('cats')
export class CatsController {
  constructor(private catsService: CatsService) {}

  @Post()
  async create(@Body() createCatDto: CreateCatDto) {
    this.catsService.create(createCatDto);
  }

  @Get()
  async findAll(): Promise<Cat[]> {
    return this.catsService.findAll();
  }
}
```

</details>

<details>
<summary>&#91; 코드 &#93; cats&#46;service&#46;ts</summary>

<a id="22beda9b0fe1800d98b2d28122fb9ed1"></a>

```typescript

import { Injectable } from '@nestjs/common';
import { Cat } from './interfaces/cat.interface';

@Injectable()
export class CatsService {
  private readonly cats: Cat[] = [];

  create(cat: Cat) {
    this.cats.push(cat);
  }

  findAll(): Cat[] {
    return this.cats;
  }
}

```

</details>

<details>
<summary>&#91; 코드 &#93; app&#46;module&#46;ts</summary>

<a id="22beda9b0fe180b58a0ddefdf4a50ef8"></a>

```typescript

import { Module } from '@nestjs/common';
import { CatsController } from './cats/cats.controller';
import { CatsService } from './cats/cats.service';

@Module({
  controllers: [CatsController],
  providers: [CatsService],
})
export class AppModule {}
```

</details>

<a id="22beda9b0fe180889958f4c239dd9d4e"></a>

### 의존성 주입 ( Dependency injection ) &#45; 생성자 주입

[Documentation &#124; NestJS &#45; A progressive Node&#46;js framework]()

> ✏️ 
> 
> <a id="22beda9b0fe18048b9a3d66d07d38f46"></a>
> 
> Nest는 <strong><u>의존성 주입</u></strong>이라는 강력한 디자인패턴을 기반으로 설계되었다&#46;
> 
> <a id="22beda9b0fe18089b6f0dff5f70798bc"></a>
> 
> 의존성 주입은 <strong><a href="https://en.wikipedia.org/wiki/Inversion_of_control">제어 역전(IoC)</a></strong> 기법으로, 직접 코드를 작성하여 <strong>종속성 인스턴스화</strong>를 수행하는 대신 <strong><u>IoC 컨테이너</u></strong><strong><u>(NestJS 런타임 시스템)</u></strong><strong><u>에 위임</u></strong>한다&#46;
> 
> <a id="22beda9b0fe180398fcfd58051d31e41"></a>
> 
> 이를 통해 각 클래스 간에 느슨한 결합(loosley coupled)을 형성하여 확장성이 용이한 코드 설계를 가능케 한다&#46;

<details>
<summary><strong>🧐 토큰 (token)</strong></summary>

<a id="22beda9b0fe180c58dcde3ecafafcb00"></a>

<a href="#/post/22beda9b-0fe1-802c-bbd0-f40fbd73d1dc">페이지</a> 

</details>

<a id="22beda9b0fe1802d9c9ad9152dc3a8c7"></a>

### <strong>NestJS 의존성 주입(DI) 흐름&#58; </strong><strong><code>CatsService</code></strong><strong> 기준</strong>

> ✏️ 
> 
> <a id="22beda9b0fe1805185fad86bf490ae21"></a>
> 
> NestJS에서 DI가 동작하기 위해 필요한 핵심 과정은 아래와 같다&#46;
> 
> - 해당 과정은 앱 부팅 시점(Bootstrapping)에 Nest가 자동으로 수행하며, 필요한 의존성 트리(Dependency Graph)를 재귀적으로 분석하여 순서대로 주입한다&#46;
>     - <strong><code>타입 → 메타데이터 → 토큰 → IoC 컨테이너 매핑</code></strong><strong> 흐름으로 동작</strong>

<details>
<summary><strong>1&#46; Service 레이어, </strong><strong><code>&#64;Injectable()</code></strong><strong>을 통해 의존성 주입 가능 대상으로 마킹</strong></summary>

<a id="22beda9b0fe18072b950c34f3047a7c0"></a>

```java
// cats.service.ts
@Injectable()
export class CatsService {
  private readonly cats: Cat[] = [];

  findAll(): Cat[] {
    return this.cats;
  }
}
```

- <code>&#64;Injectable()</code> 데코레이터는 Nest 런타임에게 이 클래스가 <strong>의존성 주입 대상이 될 수 있음을 알린다&#46;</strong>

- 이때 Nest는 reflect&#45;metadata를 통해 이 클래스에 대한 <strong>타입 메타데이터</strong>를 수집하고 저장한다&#46;

- 단, <code>&#64;Injectable()</code>만으로 IoC 컨테이너에 자동 등록되지는 않는다&#46;
    - 실제 등록은 <code>&#64;Module</code> 단계에서 이뤄진다&#46;<br>

</details>

<details>
<summary><strong>2&#46;  </strong><strong><code>생성자 주입</code></strong><strong> &#45; 생성자에서 의존성 요청 (DI 선언)</strong></summary>

<a id="22beda9b0fe1802aaef3ea4ef96330e8"></a>

```java
// cats.controller.ts
@Controller('cats')
export class CatsController {
  constructor(private catsService: CatsService) {}

  @Get()
  async findAll(): Promise<Cat[]> {
    return this.catsService.findAll();
  }
}
```

- 생성자를 통해 <strong><code>CatsService</code></strong><strong>를 </strong><strong><code>NestJS IoC 컨테이너</code></strong><strong>에 요청한다&#46; </strong>

- Nest는 이 생성자 인자를 보고, <strong><u>런타임에 design&#58;paramtypes 메타데이터를 읽</u></strong>어 <strong>D</strong><strong><u>I 토큰(CatsService) 으로 해석</u></strong>한다&#46;

</details>

<details>
<summary>3&#46; <strong><code>&#64;Module()</code></strong><strong>에서 DI 토큰 등록</strong></summary>

<a id="22beda9b0fe180d2bc9bcaaa0b232c18"></a>

```java
// app.module.ts
@Module({
  controllers: [CatsController],
  providers: [CatsService], // IoC 컨테이너에 등록
})
export class AppModule {}
```

- <code>providers&#58; &#91;CatsService&#93; </code>구문은 Nest IoC 컨테이너에 CatsService 클래스를 <strong>“토큰 = 클래스”</strong> 로 등록한다&#46;

- 등록된 이후 Nest는 해당 토큰을 가지고 의존성 주입을 처리할 수 있게 된다&#46;

</details>

<details>
<summary>4&#46; <strong>Nest 런타임의 의존성 해결 (DI Resolution)</strong></summary>

> Nest가 CatsController를 인스턴스화할 때 아래와 같이 동작한다&#46;

1. CatsController의 생성자 인자에서 DI 토큰 목록을 추출 (&#91;CatsService&#93;)

1. 등록된 IoC 컨테이너에서 CatsService 토큰을 찾음

1. 기본 스코프(SINGLETON 기준)로 CatsService 인스턴스를 한 번 생성

1. 이후 요청 시에는 <strong>캐시된 인스턴스를 재사용</strong>

</details>

<a id="22beda9b0fe18059b701cf5c603000fd"></a>

### 코드

<details>
<summary>&#91; 코드 &#93; cats&#46;service&#46;ts</summary>

> 
> 
> <a id="22beda9b0fe180c8891ce755bb3a9b34"></a>
> 
> <code>&#64;Injectable()</code> 데코레이터를 통해 <code>CatsService</code>를 Provider로 표시한다&#46;

<a id="22beda9b0fe180c7aa18dea8bb21cab0"></a>

```typescript

import { Injectable } from '@nestjs/common';
import { Cat } from './interfaces/cat.interface';

@Injectable()
export class CatsService {
  private readonly cats: Cat[] = [];

  findAll(): Cat[] {
    return this.cats;
  }
}
```

</details>

<details>
<summary>&#91; 코드 &#93; cats&#46;controller&#46;ts</summary>

> 
> 
> <a id="22beda9b0fe18058b8ecf686e1c4bda5"></a>
> 
> <strong><code>생성자 주입</code></strong>을 통해 Nest가 Provide(CatsService)를 컨트롤러 클래스에 주입하도록 요청한다&#46; 

<a id="22beda9b0fe180fb8948f5dd15399136"></a>

```typescript
import { Controller, Get } from '@nestjs/common';
import { CatsService } from './cats.service';
import { Cat } from './interfaces/cat.interface';

@Controller('cats')
export class CatsController {
  constructor(private catsService: CatsService) {}

  @Get()
  async findAll(): Promise<Cat[]> {
    return this.catsService.findAll();
  }
}
```

</details>

<details>
<summary>&#91; 코드 &#93; cats&#46;module&#46;ts</summary>

> 
> 
> <a id="22beda9b0fe180f7af61f351df0ff664"></a>
> 
> <code>&#64;Module</code> 데코레이터를 통해  <code>Nest IoC 컨테이너</code>에 <strong><u>Provider를 등록</u></strong>한다&#46;
> 
> <a id="22beda9b0fe180efbef3e7b0c20a30f4"></a>
> 
> 이를 통해 Nest IoC 컨테이너가 Provider를 인식하고 생성자 주입으로 요청한 클래스를 생성하여 넣어준다&#46;
> 
> - Spring의 수동 빈 등록과 유사 

<a id="22beda9b0fe1802aa140ca0329eb9680"></a>

```typescript

import { Module } from '@nestjs/common';
import { CatsController } from './cats/cats.controller';
import { CatsService } from './cats/cats.service';

@Module({
  controllers: [CatsController],
  providers: [CatsService],
})
export class AppModule {}
```

</details>

<a id="22beda9b0fe18069bccec834e4a0679a"></a>

### Scope

> ✏️ 
> 
> <a id="22beda9b0fe1807fad5cc555cd4d08c3"></a>
> 
> Provider는 일반적으로 애플리케이션 수명 주기와 일치라는 수명(”범위”)를 갖는다&#46;

- 애플리케이션이 부트스트랩(시작)될 때 각 종속성을 해결해야 하므로 모든 Provider가 인스턴스화(생성)된다&#46;

- 마찬가지로 애플리케이션이 종료되면 모든 Provider가 삭제된다&#46; 

- Provider의 수명(Scope)을 <strong><u>요청 범위로 지정</u></strong>할 수도 있다,
    - <strong>Provider 수명이 애플리케이션의 수명 주기가 아닌 특정 요청에 따라 결정된다&#46; &#45; </strong><strong><code>주입 스코프</code></strong>

    - <strong>자세한 내용은 아래 참조</strong>
        [Documentation &#124; NestJS &#45; A progressive Node&#46;js framework]()

<a id="22beda9b0fe18086af6bc6e08729f5a8"></a>

### Custom Provider

<a id="22beda9b0fe180329655f813dc735ed8"></a>

Nest에는 Provider 간의 관계를 관리하는 제어 역전(IoC) 컨테이너가 내장되어 있다&#46;

<a id="22beda9b0fe1803c98acf2f235f11906"></a>

해당 기능은 의존성 주입 방식이 기본 동작이지만, 세부적으로 다양한 유형의 Provider를 정의하여 사용 가능하다&#46;

- <strong><u>일반 값, 클래스, 비동기 or 동기 팩토리</u></strong>를 모두 사용할 수 있다&#46;

- Provider 정의에 대한 더 많은 예시는 아래 참조
    [Documentation &#124; NestJS &#45; A progressive Node&#46;js framework]()

<a id="22beda9b0fe180b292a8d5c8a593435b"></a>

### <strong>Provider 등록</strong>

> ✏️ 
> 
> <a id="22beda9b0fe1809aab57c03622b73b49"></a>
> 
> 공급자(<code>CatsService</code>)와 소비자(<code>CatsController</code>)를 정의했다면 <strong>Nest에 Service를 등록해 Nest IoC 컨테이너가 주입 처리</strong>할 수 있도록 해야한다&#46; 
> 
> - <code>&#64;Module()</code>의 providers에 Service(<code>CatsService</code>)를 추가한다&#46;

<a id="22beda9b0fe180aaa53ee25166ab0f63"></a>

```java

import { Module } from '@nestjs/common';
import { CatsController } from './cats/cats.controller';
import { CatsService } from './cats/cats.service';

@Module({
  controllers: [CatsController],
  providers: [CatsService],
})
export class AppModule {}

```

<a id="22beda9b0fe1801db976ebb08460104f"></a>

### <strong>수동 인스턴스화 ( Manual instantiation )</strong>

> 💬 
> 
> <a id="22beda9b0fe1804daf0dfe2beb99d3d4"></a>
> 
> Spring에서 자동 빈 등록이 아닌 수동 빈 등록 방법이 있는 것 처럼, <br>Nest에서도 이와 같이 Provider를 수동으로 등록하여 인스턴스화 하는 방법을 제공한다&#46; 

- 기존 인스턴스를 검색하거나 공급자를 동적으로 인스턴스화
    [Documentation &#124; NestJS &#45; A progressive Node&#46;js framework]()

- 함수 내에서 공급자 획득
    [Documentation &#124; NestJS &#45; A progressive Node&#46;js framework]()
